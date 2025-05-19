## 📌 Project Title
**Scalable Web Application with ALB and Auto Scaling – AWS Deployment**

---

## 🧠 Project Description

This project demonstrates the deployment of a scalable and highly available web application on AWS using EC2 instances, an Application Load Balancer (ALB), and Auto Scaling Groups (ASG). It follows AWS best practices for compute scalability, security, and cost optimization. The backend layer is supported by Amazon RDS in a Multi-AZ configuration.

---

## 🏗️ Solution Architecture

![Diagram](https://github.com/user-attachments/assets/73a16538-51fc-4cdb-9162-f63ce83e586a)


### 🧱 Key Components

| Component              | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| **EC2 (Auto Scaling)** | Hosts the web application, deployed across two AZs using an ASG             |
| **ALB**                | Distributes HTTP traffic across EC2 instances                               |
| **Internet Gateway**   | Enables access from the internet to ALB and EC2 (Public Subnets)            |
| **NAT Gateways**       | Two NAT Gateways (one per AZ) to allow outbound access from Private Subnets |
| **RDS (MySQL)**        | Multi-AZ relational DB deployed in Private Subnets                          |
| **CloudWatch**         | Collects logs and metrics from EC2 and ALB                                  |
| **SNS**                | Sends notifications based on CloudWatch alarms                              |

---

## 🔐 Security Groups

### EC2 Security Group:
- Allows inbound HTTP (Port 80) from ALB
- Allows SSH (Port 22) only from trusted IPs
- Outbound: All traffic allowed

### RDS Security Group:
- Allows MySQL (Port 3306) access only from EC2 Security Group

---

## 🚀 Deployment Overview

1. VPC with 2 Public and 2 Private Subnets
2. ALB set up in front of EC2 Auto Scaling Group
3. NAT Gateways deployed in each AZ for Private Subnets
4. EC2 Instances deployed using Launch Template
5. RDS (MySQL) deployed in Multi-AZ mode
6. IAM roles created for EC2 to access CloudWatch
7. CloudWatch Alarms + SNS notifications set up for CPU usage and health checks

---

## 📈 Monitoring & Alerts

- CloudWatch monitors EC2 instances, ALB, and RDS metrics.
- SNS sends email notifications on high CPU usage or instance failures.

---

## 🧪 Testing

- Access web app via ALB DNS name.
- Simulate load (using Apache Benchmark or similar).
- Check that Auto Scaling Group launches/removes instances.
- Validate DB connectivity and failover.

---


## 👨‍🎓 Learning Outcomes

- Build a secure, scalable, and highly available web infrastructure on AWS.
- Configure Auto Scaling policies and Load Balancing.
- Set up monitoring and alerts with CloudWatch & SNS.
- Apply cost-optimization strategies with NAT Gateway and ASG.
