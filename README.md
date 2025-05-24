## 📌 Project Title
**Secure & Scalable Web Application with ALB and Auto Scaling on AWS**

---

## 🧠 Project Description  

This project showcases deploying a secure, scalable, and highly available web application on AWS. The architecture is optimized for performance and security by placing the front-end and back-end resources in separate private subnets, with only the Application Load Balancer and NAT Gateway residing in the public subnet. Amazon RDS (MySQL) is used for persistent data storage in a Multi-AZ deployment. Monitoring and alerting are handled through CloudWatch and SNS.

---

## 🏗️  Solution Architecture

![Architecture Diagram](images/8440fbf7-3220-487b-a88f-0dbca4806870.png)


### 🔁 Subnet Allocation

| Component                         | Subnet Type | Description                                                              |
|----------------------------------|-------------|--------------------------------------------------------------------------|
| **Application Load Balancer**    | Public      | Distributes traffic to private front-end EC2 instances                   |
| **NAT Gateway**                  | Public      | Provides outbound internet access for private subnet resources           |
| **Front-end EC2 Instances**      | Private     | Hosts the web application’s UI components                                |
| **Back-end EC2 Instances**       | Private     | Executes server-side application logic                                   |
| **Amazon RDS (MySQL)**           | Private     | Managed relational database deployed in Multi-AZ configuration           |

### 📍 Network Configuration

- **Region**: `eu-north-1 (Stockholm)`
- **VPC CIDR**: `10.10.0.0/16`

| Subnet Type | CIDR Range        | Availability Zone     |
|-------------|-------------------|------------------------|
| Public      | 10.10.1.0/24      | eu-north-1a            |
| Private FE  | 10.10.101.0/24    | eu-north-1a            |
| Private BE  | 10.10.102.0/24    | eu-north-1b            |

---

## 🔐 Security Enhancements

### Security Groups

- **ALB SG**: Allows HTTP (80) from the internet
- **Front-End EC2 SG**: Accepts HTTP from ALB only
- **Back-End EC2 SG**: Accepts traffic from Front-End EC2 SG on custom ports (e.g., 8080)
- **RDS SG**: Accepts MySQL (3306) only from Back-End EC2 SG

### IAM Roles

- Front-End EC2: Access to CloudWatch Logs
- Back-End EC2: Access to RDS, SSM, CloudWatch
- All roles follow **least privilege** principle

---

## 📈 Monitoring & Alerts

- **CloudWatch**: EC2, ALB, and RDS metrics monitored
- **Alarms**: High CPU, Unhealthy Host Count
- **SNS Topics**: Email alerts on critical metrics

---

## 🧪 Testing & Validation

- Access the application via the **ALB DNS name**
- Validate load balancing and failover
- Simulate CPU load and verify Auto Scaling triggers
- Verify back-end EC2 → RDS connectivity
- Ensure no direct internet access to private EC2 or RDS

---

## 👨‍🎓 Learning Outcomes

- Build a secure multi-tier architecture on AWS
- Configure public/private subnets and routing
- Use Auto Scaling and ALB for high availability
- Implement CloudWatch monitoring and SNS alerts
- Apply best practices for IAM and security groups
