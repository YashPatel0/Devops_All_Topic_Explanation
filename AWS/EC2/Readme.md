# ☁️ AWS EC2 Complete Guide – DevOps Edition

> A complete and practical guide to Amazon EC2 for Cloud & DevOps Engineers.

---

# 📌 Table of Contents

- What is Amazon EC2?
- Why EC2 is Important
- EC2 Architecture
- EC2 Instance Types
- EC2 Pricing Models
- Launching an EC2 Instance
- Security Groups
- Key Pairs
- EBS Volumes
- Elastic IP
- EC2 Storage Options
- Monitoring with CloudWatch
- Auto Scaling
- Load Balancer Integration
- EC2 Best Practices
- Important Interview Questions

---

# 🚀 What is Amazon EC2?

Amazon Elastic Compute Cloud (EC2) is a web service that provides **resizable virtual servers (instances)** in the cloud.

It allows you to:
- Launch virtual machines
- Scale compute capacity
- Pay only for what you use
- Deploy applications globally

---

# 📦 In Simple Words

EC2 is like renting a virtual computer in the AWS cloud.

You can:
- Choose CPU & RAM
- Select operating system
- Configure storage
- Control networking
- Scale up or down anytime

---

# 🏗 EC2 Architecture Components

EC2 works with multiple AWS services:

- **AMI (Amazon Machine Image)** → OS template
- **Instance Type** → CPU & Memory configuration
- **EBS** → Storage
- **Security Group** → Firewall rules
- **Key Pair** → Secure login
- **VPC** → Network isolation
- **Elastic IP** → Static public IP

---

# 🖥 EC2 Instance Types

EC2 instances are grouped by use case.

## 1️⃣ General Purpose
Balanced compute, memory, networking  
Example: `t3`, `t4g`, `m5`

## 2️⃣ Compute Optimized
High CPU performance  
Example: `c5`, `c6`

## 3️⃣ Memory Optimized
High RAM workloads  
Example: `r5`, `r6`

## 4️⃣ Storage Optimized
High disk throughput  
Example: `i3`, `d2`

## 5️⃣ GPU Instances
Machine learning, AI  
Example: `p3`, `g4`

---

# 💰 EC2 Pricing Models

## 1️⃣ On-Demand
- Pay per hour/second
- No commitment
- Best for short-term usage

## 2️⃣ Reserved Instances
- 1 or 3-year commitment
- Up to 75% discount

## 3️⃣ Spot Instances
- Cheapest option
- Can be terminated anytime
- Good for batch jobs

## 4️⃣ Savings Plans
- Flexible pricing model
- Commit to consistent usage

---

# 🚀 Steps to Launch an EC2 Instance

1. Go to AWS Console → EC2
2. Click **Launch Instance**
3. Choose AMI (Amazon Linux / Ubuntu)
4. Select Instance Type
5. Configure Instance Details
6. Add Storage
7. Configure Security Group
8. Create or Select Key Pair
9. Launch Instance

---

# 🔐 Security Groups

Security Groups act as a **virtual firewall** for EC2.

- Control inbound traffic
- Control outbound traffic
- Stateful (return traffic automatically allowed)

### Example Rules

| Type | Port | Purpose |
|------|------|---------|
| SSH  | 22   | Remote login |
| HTTP | 80   | Web traffic |
| HTTPS| 443  | Secure web |

---

# 🔑 Key Pair

Key pairs are used for secure SSH access.

- Public key → Stored in AWS
- Private key → Download and keep safe

Connect to EC2:

```bash
chmod 400 mykey.pem
ssh -i mykey.pem ec2-user@public-ip
```

---

# 💾 EBS (Elastic Block Store)

EBS provides persistent storage for EC2.

## Types of EBS

- gp3 → General purpose SSD
- io1/io2 → High performance SSD
- st1 → Throughput optimized HDD
- sc1 → Cold HDD

### Important Notes

- EBS is persistent
- Can be attached/detached
- Supports snapshots (backup)

---

# 🌍 Elastic IP

Elastic IP is a static public IP address.

- Used to avoid IP change after restart
- Can be remapped to another instance
- Charged if not attached to running instance

---

# 📦 EC2 Storage Options

| Storage Type | Description |
|-------------|------------|
| EBS | Persistent block storage |
| Instance Store | Temporary storage |
| EFS | Shared file system |
| S3 | Object storage |

---

# 📊 Monitoring with CloudWatch

Amazon CloudWatch monitors:

- CPU utilization
- Memory usage (custom)
- Network traffic
- Disk I/O

Basic monitoring → 5-minute intervals  
Detailed monitoring → 1-minute intervals

---

# ⚖ Auto Scaling

Auto Scaling automatically adjusts EC2 capacity based on demand.

Components:
- Launch Template
- Auto Scaling Group
- Scaling Policy

Types of Scaling:
- Target Tracking
- Step Scaling
- Scheduled Scaling

---

# 🌐 Load Balancer Integration

Elastic Load Balancer (ELB) distributes traffic across EC2 instances.

Types:
- Application Load Balancer (ALB)
- Network Load Balancer (NLB)
- Gateway Load Balancer (GWLB)

Benefits:
- High availability
- Fault tolerance
- Automatic traffic distribution

---

# 🔐 EC2 Best Practices (DevOps Focus)

✔ Use IAM roles instead of access keys  
✔ Restrict Security Group access (Never open 0.0.0.0/0 for SSH)  
✔ Use Auto Scaling for high availability  
✔ Enable CloudWatch monitoring  
✔ Take regular EBS snapshots  
✔ Use Elastic IP only when required  
✔ Use Reserved Instances for long-term projects  

---

# 🎯 Important EC2 Interview Questions

1. What is EC2?
2. Difference between Security Group and NACL?
3. What is AMI?
4. Difference between EBS and Instance Store?
5. What is Spot Instance?
6. How does Auto Scaling work?
7. How to secure EC2?
8. What is Elastic IP?
9. How does Load Balancer work with EC2?
10. What happens when EC2 is stopped vs terminated?

---

# 🧠 Quick Concept Summary

- EC2 = Virtual machine in AWS
- AMI = OS template
- Security Group = Firewall
- EBS = Persistent storage
- Elastic IP = Static public IP
- Auto Scaling = Automatic scaling
- ELB = Traffic distribution

---


⭐ If this helped you, consider starring the repository!
