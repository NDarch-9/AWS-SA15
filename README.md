# 🚀 High-Availability Scalable Web Application on AWS

## 📑 Table of Contents
- [📌 Project Overview](#-project-overview)
- [🏗 Architecture Diagram](#-architecture-diagram)
- [🚀 Key Features](#-key-features)
- [🛠 Tech Stack](#-tech-stack)
- [🛤 Request Flow (Technical Path)](#-request-flow-technical-path)
- [🔧 How to Deploy (Quick Steps)](#-how-to-deploy-quick-steps)
- [📧 Contact](#-contact)

---

## 📌 Project Overview

the **Ink Cloud** solution helps users create, store, and manage digital notes through a web-based application designed to replace traditional paper notebooks. It enables users to securely access their notes from anywhere while maintaining simplicity and ease of use.

A key idea behind Ink Cloud is high availability — your notes are always available and never lost. To achieve this, the solution uses a **scalable AWS architecture** built on **Amazon EC2**, **Auto Scaling Groups**, and an **Application Load Balancer**, ensuring continuous access to user data even during infrastructure failures.

This solution automatically operates in a highly available, fault-tolerant environment across multiple Availability Zones. Notes are stored and retrieved dynamically, allowing users to write and view content in real time. By leveraging AWS managed services, Ink Cloud provides secure cloud storage, elastic compute

---

## 🏗 Architecture Diagram

<img width="6525" height="4950" alt="مشروعي" src="https://github.com/user-attachments/assets/9cd604f3-547d-4027-8278-35bc07c44566" />


*Note: The architecture follows AWS best practices by separating public and private resources, ensuring security, scalability, and reliability.*

---

## 🚀 Key Features

- **Scalability**: Automatically scales EC2 instances based on traffic demand using Auto Scaling policies.
- **High Availability**: Deployed across multiple Availability Zones to ensure application resilience.
- **Security**:
  - Workloads run inside **private subnets**.
  - Fine-grained **Security Groups** control traffic flow.
  - **NAT Gateway** enables secure outbound internet access.
- **Database Reliability**: Amazon RDS deployed in **Multi-AZ** mode for automatic failover.
- **Monitoring & Alerts**: Amazon CloudWatch monitors system health, with **SNS notifications** for scaling events.

---

## 🛠 Tech Stack

- **Cloud Provider**: AWS (Amazon Web Services)
- **Compute**: EC2, Auto Scaling Group, Launch Templates
- **Networking**: VPC, Public & Private Subnets, ALB, NAT Gateway, Internet Gateway
- **Database**: Amazon RDS (MySQL / PostgreSQL)
- **Security**: IAM Roles, Security Groups
- **Monitoring & Management**: CloudWatch, SNS

---

## 🛤 Request Flow (Technical Path)

1. **User** sends a request through the **Internet Gateway**.
2. The **Application Load Balancer (ALB)** receives traffic and performs health checks.
3. The **Target Group** forwards the request to a healthy **EC2 instance** in a private subnet.
4. The **EC2 instance** processes the request and communicates with the **primary RDS** instance.
5. **CloudWatch** monitors the Auto Scaling Group and triggers scaling actions when thresholds are exceeded.

---

## 🔧 How to Deploy (Quick Steps)

1. Create a **VPC** with public and private subnets across at least two Availability Zones.
<img width="1640" height="732" alt="Screenshot (427)" src="https://github.com/user-attachments/assets/bb3aa711-da59-4e07-aa9d-0c612da77c90" />
** **
<img width="1825" height="570" alt="Screenshot (429)" src="https://github.com/user-attachments/assets/ce414814-3f28-4eae-bfc6-5642674ff041" />

3. Configure an **Internet Gateway**
  <img width="1613" height="400" alt="Screenshot (426)" src="https://github.com/user-attachments/assets/c0796f83-a102-4e8a-81ac-ed8a9ec93dd8" />

---
Create **Security Groups** for RDS , WebSerever, ALP

## ALB-SG
Allow public HTTP traffic from the internet to the Load Balancer.

<img width="1595" height="603" alt="Screenshot (434)" src="https://github.com/user-attachments/assets/ab86c1e2-44e4-4cd8-ab74-be90f20b0461" />

## DB-SG
Allow RDS access only from the WebServer Security Group.

<img width="1567" height="636" alt="Screenshot (432)" src="https://github.com/user-attachments/assets/df2d4f21-00fb-4de0-9382-80b3f57dfc6c" />

## Web-SG
Allow HTTP traffic only from the Application Load Balancer (ALB-SG)

<img width="1583" height="607" alt="Screenshot (433)" src="https://github.com/user-attachments/assets/3125a3e4-55a6-452e-bae3-176cec91a624" />

 ---
5. Deploy an **Amazon RDS Mysql** instance in private subnets.
## Creat Database
<img width="1490" height="271" alt="Screenshot (435)" src="https://github.com/user-attachments/assets/f1b7819e-4736-439e-a301-898420c1cd0f" />

<img width="1119" height="588" alt="Screenshot (438)" src="https://github.com/user-attachments/assets/93cb4a1d-8819-49b9-97a7-9666d6a7ebc5" />
     Note: 
     
## Security group rules

<img width="1507" height="283" alt="Screenshot (437)" src="https://github.com/user-attachments/assets/e8582884-c480-41ba-ae84-b95af20128a6" />

   ---
7. Create a **Launch Template** containing the application setup.

  ---
9. Configure an **Auto Scaling Group** and attach it to an **Application Load Balancer**.
  ---
11. Set up **CloudWatch Alarms** to alerts.
    
<img width="1913" height="500" alt="Screenshot (398)" src="https://github.com/user-attachments/assets/d8096183-6dd6-4740-858e-3b7b1aa1c042" />


<img width="1207" height="446" alt="Screenshot (400)" src="https://github.com/user-attachments/assets/e0dc14e2-27c2-4aad-83ee-b4362872d26b" />

<img width="1515" height="634" alt="Screenshot (401)" src="https://github.com/user-attachments/assets/7a09ff77-d200-4c0a-9ddb-7af03393e0d5" />


<img width="1920" height="1080" alt="Screenshot (402)" src="https://github.com/user-attachments/assets/26330c7d-b25e-4dc0-9811-75f5b83f0a32" />

<img width="1538" height="648" alt="Screenshot (416)" src="https://github.com/user-attachments/assets/17b645a4-57dc-4523-9acb-a4d5c51666d0" />


---

## 📧 Contact

**Your Name**  
🔗 https://www.linkedin.com
