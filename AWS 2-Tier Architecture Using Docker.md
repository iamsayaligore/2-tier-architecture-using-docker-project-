
# AWS 2-Tier Architecture Using Docker

## 📌 Project Overview
This project demonstrates how to build and deploy a **2-Tier Architecture on AWS using Docker**.  
The application is containerized and deployed on **AWS EC2**, separating the **Web/Application Tier** and **Database Tier** for better scalability and maintainability.

---

## 🏗 Architecture Overview
The architecture follows a **two-tier design**

## 1️⃣ Web / Application Tier
- Runs inside a **Docker container**
- Hosts a web application (Nginx / Apache / Node.js / PHP)
- Deployed on an **EC2 instance**
- Exposed to the internet via **Security Groups**

## 2️⃣ Database Tier
- Runs inside a **Docker container**
- Hosts a python application (Nginx / Apache / python )
- Deployed on a separate **EC2 instance**
- Accessible only from the Web Tier (private access)

---

## ☁ AWS Services Used
- **EC2** – Compute service to host Docker containers
- **VPC** – Isolated network
- **Security Groups** – Control inbound and outbound traffic
- **Elastic IP (Optional)** – Static public IP for web server
- **IAM (Optional)** – Secure access management

---

## 🐳 Docker Components
- Docker Engine
- Docker Images
- Docker Containers
- Docker Network (Bridge)
- `Dockerfile`
- `docker-compose.yml` (optional)

---

## 🔧 Prerequisites
Before starting, ensure you have:
- AWS Account
- EC2 Instances (Amazon Linux / Ubuntu)
- Docker installed
- Basic knowledge of AWS & Docker
- SSH access to EC2 instances

---

## 🚀Setup Steps


## **PART-1**

## Step 1: Launch EC2 Instances

- Create **EC2 instances**

      Docker

![alt text](<Screenshot 2026-01-14 235023.png>)

## Step 2: Install Docker

     sudo yum update -y
     sudo yum install docker -y

![alt text](<Screenshot 2026-01-14 233456.png>)

     sudo systemctl start docker
     sudo systemctl enable docker

![alt text](image.png)

## Step 3: Git Repository Clone Node App

           git clone https://github.com/amtruptimane/node-js-app-CICD.git

           cd node-js-app-CICD

![alt text](<Screenshot 2026-01-08 152454.png>)

## Step 4: Create Dockerfile

           vim dockerfile

![alt text](<Screenshot 2026-01-08 152733-1.png>)

## Step 5: Build Docker images
 
             docker build -t nodeimg .

![alt text](<Screenshot 2026-01-08 152929.png>)

 ## Step 6: check docker  images

            docker images

![alt text](<Screenshot 2026-01-08 153036-1.png>)


## Step 7: Run Node.js Container

           docker run -d --name nodeapp nodeimg
           check ps

![alt text](<Screenshot 2026-01-08 153316.png>)


## Step 8: NGINX is running as a reverse proxy server

            docker run -d -p 80:80 --name proxy --link nodeapp:nodeimg nginx
            docker ps

![alt text](<Screenshot 2026-01-08 153642.png>)


## Step 9:  Access Nginx Container 

           docker exec -it proxy /bin/bash

Navigate to Nginx config directory

          cd /etc/nginx
          ls

Edit Default Nginx config

Install editor

            apt update
            apt install vim -y

 Edit configuration:
  
             vim /etc/nginx/conf.d/default.conf

 ![alt text](<Screenshot 2026-01-08 154452.png>)

 ## Step 10: Nginx Reverse Proxy Configuration

![alt text](<Screenshot 2026-01-08 154721.png>)

## **Output**

![alt text](<Screenshot 2026-01-08 161606.png>)

## **PART-2**

## step 1: Git Repository Clone Pythonapp

         git clone https://github.com/amtruptimane/pythonapp.git
         cd pythonapp/

![alt text](<Screenshot 2026-01-08 162546.png>)

## Step 2: Create dockerfile
     
      vim dockerfile

![alt text](<Screenshot 2026-01-16 215330.png>)

![alt text](<Screenshot 2026-01-08 162608.png>)


## Step 3: Build Docker images
  
         docker build -t pythonimg .

![alt text](<Screenshot 2026-01-08 162902.png>)

## Step 4: check docker  images

            docker images

 ![alt text](<Screenshot 2026-01-08 163020.png>)    


## Step 5:  Run Node.js Container

           docker run -d --name pythonapp pythonimg
           check ps
           docker run -d -p 80:80 --name proxy --link nodeapp:nodeimg nginx
           docker ps

![alt text](<Screenshot 2026-01-08 163855.png>)

## Step 6: Access Nginx Container 

           docker exec -it proxy /bin/bash

Navigate to Nginx config directory

          cd /etc/nginx
          ls

Edit Default Nginx config

Install editor

            apt update
            apt install vim -y

 Edit configuration:
  
             vim /etc/nginx/conf.d/default.conf

![alt text](<Screenshot 2026-01-08 163921.png>)


## Step 7: **Output**

![alt text](<Screenshot 2026-01-08 164258.png>)

## 🔐 Security Best Practices

• Restrict database access using security groups

• Do not expose DB port publicly

• Use environment variables for credentials

• Enable IAM roles instead of hardcoded keys

## 📈 Benefits of 2-Tier Architecture

• Clear separation of concerns

• Easy container management

• Scalable and maintainable

• Improved security

• Cloud-ready deployment

