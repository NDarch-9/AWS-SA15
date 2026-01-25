  # High-Availability Scalable Web Application on AWS

## Table of Contents
- [Project Overview](#-project-overview)
- [Architecture Diagram](#-architecture-diagram)
- [Key Features](#-key-features)
- [Tech Stack](#-tech-stack)
- [Request Flow (Technical Path)](#-request-flow-technical-path)
- [How to Deploy (Quick Steps)](#-how-to-deploy-quick-steps)
- [Final Resulte](-Final-Resulte)
-  [Conclusion](-Conclusion)
- [Contact](#-contact)

---

##  Project Overview

The **Ink Cloud** solution helps users create, store, and manage digital notes through a web-based application designed to replace traditional paper notebooks. It enables users to securely access their notes from anywhere while maintaining simplicity and ease of use.

A key idea behind Ink Cloud is high availability — your notes are always available and never lost. To achieve this, the solution uses a **scalable AWS architecture** built on **Amazon EC2**, **Auto Scaling Groups**, and an **Application Load Balancer**, ensuring continuous access to user data even during infrastructure failures.

This solution automatically operates in a highly available, fault-tolerant environment across multiple Availability Zones. Notes are stored and retrieved dynamically, allowing users to write and view content in real time. By leveraging AWS managed services, Ink Cloud provides secure cloud storage, elastic compute

---

## Architecture Diagram


<img width="6525" height="4950" alt="مشروعي (1)" src="https://github.com/user-attachments/assets/f268ca66-d34b-444a-804e-409c27319f48" />


*Note: The architecture follows AWS best practices by separating public and private resources, ensuring security, scalability, and reliability.*

---

## Key Features

- **Scalability**: Automatically scales EC2 instances based on traffic demand using Auto Scaling policies.
- **High Availability**: Deployed across multiple Availability Zones to ensure application resilience.
- **Security**:
  - Workloads run inside **private subnets**.
  - Fine-grained **Security Groups** control traffic flow.
  - **NAT Gateway** enables secure outbound internet access.
- **Database Reliability**: Amazon RDS deployed in **Multi-AZ** mode for automatic failover.
- **Monitoring & Alerts**: Amazon CloudWatch monitors system health, with **SNS notifications** for scaling events.

---

## Tech Stack

- **Cloud Provider**: AWS (Amazon Web Services)
- **Compute**: EC2, Auto Scaling Group, Launch Templates
- **Networking**: VPC, Public & Private Subnets, ALB, Internet Gateway
- **Database**: Amazon RDS (MySQL (
- **Security**: IAM Roles, Security Groups
- **Monitoring & Management**: CloudWatch, SNS

---

## Request Flow (Technical Path)

1. User sends an HTTP request via the Internet.
2. The request enters the VPC through the Internet Gateway.
3. The Application Load Balancer (ALB) receives the request and performs health checks.
4. The ALB forwards the request to a healthy EC2 instance in a private subnet via the Target Group.
5. The EC2 instance processes the request and reads/writes data to the Amazon RDS database.
6. The response is returned back to the user through the ALB.


## Monitoring & Scaling
- Amazon CloudWatch monitors EC2 metrics and ALB request counts.
- CloudWatch alarms trigger Auto Scaling policies when thresholds are exceeded.
- The Auto Scaling Group launches or terminates EC2 instances accordingly.

---

## How to Deploy (Quick Steps)

1. Create a **VPC** with public and private subnets across at least two Availability Zones.
 ---
<img width="1640" height="732" alt="Screenshot (427)" src="https://github.com/user-attachments/assets/bb3aa711-da59-4e07-aa9d-0c612da77c90" />

<img width="1825" height="570" alt="Screenshot (429)" src="https://github.com/user-attachments/assets/ce414814-3f28-4eae-bfc6-5642674ff041" />

2. Configure an **Internet Gateway**
  <img width="1613" height="400" alt="Screenshot (426)" src="https://github.com/user-attachments/assets/c0796f83-a102-4e8a-81ac-ed8a9ec93dd8" />

---
3. Create **Security Groups** for RDS , WebSerever, ALb

## ALB-SG
Allow public HTTP traffic from the internet to the Load Balancer.

<img width="1595" height="603" alt="Screenshot (434)" src="https://github.com/user-attachments/assets/ab86c1e2-44e4-4cd8-ab74-be90f20b0461" />

## DB-SG
Allow RDS access only from the WebServer Security Group.

<img width="1567" height="636" alt="Screenshot (432)" src="https://github.com/user-attachments/assets/df2d4f21-00fb-4de0-9382-80b3f57dfc6c" />

## Web-SG
Allow HTTP traffic only from the Application Load Balancer (ALB-SG)

<img width="1583" height="607" alt="Screenshot (433)" src="https://github.com/user-attachments/assets/3125a3e4-55a6-452e-bae3-176cec91a624" />

##  IAM Roles
<img width="1484" height="380" alt="Screenshot (446)" src="https://github.com/user-attachments/assets/a9d72a0f-58ed-4d2a-a105-1725c0333839" />
<img width="911" height="387" alt="Screenshot (447)" src="https://github.com/user-attachments/assets/7a1b8776-69d2-48ae-8ab2-71d0c4b840fc" />


 ---
4. Deploy an **Amazon RDS Mysql** instance in private subnets.
## Creat Database

<img width="1490" height="271" alt="Screenshot (435)" src="https://github.com/user-attachments/assets/f1b7819e-4736-439e-a301-898420c1cd0f" />
<img width="1119" height="588" alt="Screenshot (438)" src="https://github.com/user-attachments/assets/93cb4a1d-8819-49b9-97a7-9666d6a7ebc5" />
     
NOTE:Based on the architecture diagram, the Availability Zones should be two. However, due to the limitations of the AWS Free Tier, it is not possible to distribute the databases across two Availability Zones.

  
 ## Subnet group
**Why DB Subnet Groups Matter?**
A DB Subnet Group defines the network boundaries for RDS instances. 

High Availability (Multi-AZ) : It maps subnets across multiple Availability Zones, ensuring the infrastructure is "failover-ready" even if one data center goes down.

Strict Security Isolation : It confines the database to Private Subnets, removing any direct route to the public internet and drastically reducing the attack surface.

Scalable Networking : It pre-organizes internal IP addressing, allowing for seamless scaling, updates, and maintenance without reconfiguring the VPC architecture.
 <img width="1508" height="686" alt="Screenshot (425)" src="https://github.com/user-attachments/assets/b6d21f78-cb18-47e9-95cf-497d51c63b04" />
 
<img width="1503" height="306" alt="Screenshot (424)" src="https://github.com/user-attachments/assets/0cdb837e-7ce1-4d22-b62e-4f2349018bdc" />

## Security group rules

<img width="1507" height="283" alt="Screenshot (437)" src="https://github.com/user-attachments/assets/e8582884-c480-41ba-ae84-b95af20128a6" />

   ---
5. Create a **Launch Template** containing the application setup.
<img width="1905" height="724" alt="Screenshot (442)" src="https://github.com/user-attachments/assets/a0b33272-03bf-4c4b-8d22-3a4e5d509671" />

## User Data 
Here, I am only showing the most important parts of the code related to connecting the HTML page to the servers, not the entire code.

 **1. Setting up the software environment**
        
        #!/bin/bash yum update -y
        yum install -y httpd php php-mysqli
  **2. Starting the server**    

           systemctl start httpd
           systemctl enable httpd
  **3. Database Configuration**
          
           http_response_code(200); 
           $host = "my-web-db.ccl8iy6uimed.us-east-1.rds.amazonaws.com";
             $user = " user name";
             $pass = " ";
              $db   = "mydb"; // database intitil name
  ---
6. Configure an **Auto Scaling Group** and attach it to an **Application Load Balancer**.
## ALB 

<img width="1516" height="475" alt="Screenshot (407)" src="https://github.com/user-attachments/assets/9af9477c-6d99-468e-ac07-bd5e239fc1c6" />


## ASG
 We notice in the image below, highlighted in green, that the storage capacity is set as follows: **Desired = 2**, **Minimum = 1**, and **Maximum = 3**.
This represents the number of instances we want to add when distributing the load across the servers. It depends on the size of the project, and these numbers can be increased based on the capacity required by the project.
Here, I added **2**, which is suitable for my project.

<img width="1558" height="718" alt="Screenshot (443)" src="https://github.com/user-attachments/assets/ab441747-ac6e-4463-935c-5c513612f336" />

## Target Group
 
  <img width="1599" height="682" alt="Screenshot (444)" src="https://github.com/user-attachments/assets/bd7727d5-df31-4a54-8de4-68ab1731e03e" />

<img width="1572" height="363" alt="Screenshot (445)" src="https://github.com/user-attachments/assets/91b2974d-0603-4448-9c25-01f3a349c816" />
 

  ---
7. Set up **CloudWatch Alarms** to alerts.
    
<img width="1913" height="500" alt="Screenshot (398)" src="https://github.com/user-attachments/assets/d8096183-6dd6-4740-858e-3b7b1aa1c042" />


<img width="1207" height="446" alt="Screenshot (400)" src="https://github.com/user-attachments/assets/e0dc14e2-27c2-4aad-83ee-b4362872d26b" />

<img width="1515" height="634" alt="Screenshot (401)" src="https://github.com/user-attachments/assets/7a09ff77-d200-4c0a-9ddb-7af03393e0d5" />

<img width="1515" height="634" alt="Screenshot (401)" src="https://github.com/user-attachments/assets/e61a34f2-30a8-42b8-bd51-e920a853d0f4" />

<img width="1538" height="648" alt="Screenshot (416)" src="https://github.com/user-attachments/assets/4abb8c1b-85f8-4992-82d1-f5b52984489a" />

<img width="1500" height="473" alt="Screenshot (449)" src="https://github.com/user-attachments/assets/50e8f782-cc74-4ce4-be35-6f62de9afa1e" />

---
___

## Final Resulte 
A simple website through which you can write your ideas, save them, and also delete them. I added a database connectivity feature so that when the site is accessible, I can verify whether the connection is successful. If a green color appears, it means the connection is established and the data is saved in a database table; otherwise, an error will be displayed. I added this note for technical details related to system testing and ensuring that the data is directed to the correct destination. When I refresh the page, the data remains, and if there is heavy load on an instance, the server will route traffic to the second Availability Zone to identify another instance.

     URL: MyProject-ALB-384035755.us-east-1.elb.amazonaws.com

https://github.com/user-attachments/assets/ae38c000-137f-46a0-9a97-b87f3f42995d

## Conclusion

This project represents my first hands-on experience with cloud computing and the practical implementation of scalable cloud architecture on AWS. While there may be areas for improvement and potential mistakes, the overall process has been a valuable learning journey that strengthened my understanding of cloud services, scalability, and system design. Through continuous practice, experimentation, and guidance, I am confident that I will further enhance my technical skills over time.
I welcome any feedback or observations, as they will contribute significantly to my professional growth and the improvement of future projects.


**Nada**  
 [https://www.linkedin.com](https://www.linkedin.com/in/nada-mesfer?lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_contact_details%3B%2BrqkfnfNS6KHXv9%2FC2kMjg%3D%3D)

Email: [nd9arch@gmail.com](mailto:nd9arch@gmail.com)
