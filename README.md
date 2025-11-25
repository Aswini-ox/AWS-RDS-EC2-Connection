# AWS Project: RDS Database Connected to EC2 Instance

**Name:** Aswini Aswini  
**Course:** AWS Cloud Computing  
**Date:** 25-Nov-2025  

---

## 1️⃣ Project Overview
This project demonstrates how to create a **MySQL RDS database** and connect it securely to an **EC2 instance** within the same VPC.  
It includes setting up security groups, launching an EC2 instance, creating an RDS database, and verifying connectivity.

---

## 2️⃣ Architecture Diagram

+----------------+          +----------------+
|                |  Port 3306  |                |
|   EC2 Instance |------------>|   RDS MySQL    |
|  (Ubuntu/AL)   |             |   Database    |
+----------------+             +----------------+
        |                             |
        | SSH Port 22                  | MySQL Port 3306
        |                             |
     User PC                      VPC Security Group


**Diagram Description:**  
- EC2 instance (Amazon Linux t3.micro) connects to RDS MySQL (db.t3.micro)  
- EC2 uses SSH for management; RDS is private and accessed only through EC2  
- Security groups control inbound and outbound traffic

---

## 3️⃣ Steps Performed

### A. Security Group Creation
- EC2 security group (`ec2-sg`) allows SSH (22) from my IP  
- RDS security group (`rds-sg`) allows MySQL (3306) from EC2 only

### B. Launch EC2 Instance
- AMI: Amazon Linux 2023  
- Instance type: t3.micro (Free Tier)  
- Key pair: `my-key.pem`  
- Security group: `ec2-sg`

### C. Create RDS MySQL Database
- DB identifier: `mydb`  
- Engine: MySQL 8.0  
- Instance type: db.t3.micro (Free Tier)  
- Security group: `rds-sg`  
- Public access: No

### D. Install MySQL Client on EC2
```bash
sudo dnf update -y
sudo dnf install -y mariadb
. Connect EC2 to RDS
mysql -h <RDS-endpoint> -u admin -p
