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
2. Configure an **Internet Gateway** and **NAT Gateway**.
3. Deploy an **Amazon RDS** instance in private subnets.
4. Create a **Launch Template** containing the application setup.
5. Configure an **Auto Scaling Group** and attach it to an **Application Load Balancer**.
6. Set up **CloudWatch Alarms** to enable automatic scaling and alerts.

---

## 📧 Contact

**Your Name**  
🔗 https://www.linkedin.com
