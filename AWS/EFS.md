# 📂 AWS EFS Complete Guide – DevOps Edition

> A complete and practical guide to Amazon Elastic File System (EFS) for Cloud & DevOps Engineers.

---

# 📌 Table of Contents

- What is Amazon EFS?
- Why Use EFS?
- How EFS Works
- EFS Architecture
- EFS vs EBS vs S3
- Performance Modes
- Throughput Modes
- Storage Classes
- Creating an EFS File System
- Mounting EFS to EC2
- Security in EFS
- Monitoring & Backup
- Use Cases
- Best Practices
- Important Interview Questions

---

# 🚀 What is Amazon EFS?

Amazon Elastic File System (EFS) is a **fully managed, scalable, and elastic NFS file storage service** for use with AWS Cloud services and on-premises resources.

It provides:

- Shared file storage
- Automatic scaling
- High availability
- Managed infrastructure

---

# 📦 In Simple Words

EFS is like a **shared network drive in the cloud**.

Multiple EC2 instances can:
- Read data
- Write data
- Access the same files simultaneously

---

# 🏗 How EFS Works

- Uses **NFS protocol (Network File System)**
- Automatically scales storage up and down
- Accessible from multiple EC2 instances
- Regional service (multi-AZ)

---

# 🏛 EFS Architecture

Components:

- **EFS File System**
- **Mount Targets** (one per Availability Zone)
- **Security Groups**
- **EC2 Instances**
- **VPC**

Each AZ has a mount target that allows EC2 instances to connect to EFS.

---

# 📊 EFS vs EBS vs S3

| Feature | EFS | EBS | S3 |
|----------|-----|-----|----|
| Type | File Storage | Block Storage | Object Storage |
| Shared Access | Yes | No (single instance) | Yes |
| Protocol | NFS | Attached disk | HTTP |
| Use Case | Shared data | Database storage | Backup & static files |
| Multi-AZ | Yes | No (Single AZ) | Yes |

---

# ⚡ Performance Modes

## 1️⃣ General Purpose (Default)

- Low latency
- Best for web servers
- Ideal for most applications

## 2️⃣ Max I/O

- Higher throughput
- Slightly higher latency
- Big data & parallel workloads

---

# 🚀 Throughput Modes

## 1️⃣ Bursting Throughput

- Scales automatically
- Good for unpredictable workloads

## 2️⃣ Provisioned Throughput

- Manually set throughput
- Suitable for consistent workloads

## 3️⃣ Elastic Throughput

- Automatically adjusts based on workload
- Best for dynamic applications

---

# 📦 Storage Classes

## 1️⃣ Standard

- Frequently accessed data
- Higher performance

## 2️⃣ Infrequent Access (EFS-IA)

- Lower cost
- Ideal for backup and archive
- Lifecycle policies available

---

# 🚀 Steps to Create an EFS File System

1. Go to AWS Console → EFS
2. Click **Create File System**
3. Select VPC
4. Configure mount targets (AZs)
5. Choose performance & throughput mode
6. Configure security groups
7. Create file system

---

# 🔗 Mounting EFS to EC2

### Step 1: Install NFS Client

Amazon Linux:

```bash
sudo yum install -y amazon-efs-utils
```

Ubuntu:

```bash
sudo apt install -y nfs-common
```

---

### Step 2: Mount EFS

```bash
sudo mount -t efs fs-12345678:/ /mnt/efs
```

Or using NFS:

```bash
sudo mount -t nfs4 -o nfsvers=4.1 fs-12345678.efs.ap-south-1.amazonaws.com:/ /mnt
```

---

# 🔐 Security in EFS

Security Layers:

1. **Security Groups** (Control network access)
2. **IAM Policies**
3. **Encryption at Rest**
4. **Encryption in Transit (TLS)**

Best Practice:
- Allow NFS port 2049 only within VPC
- Enable encryption

---

# 📊 Monitoring & Backup

Monitoring via:

- Amazon CloudWatch
- Metrics: throughput, IOPS, connections

Backup options:

- AWS Backup
- Lifecycle policies
- EFS replication

---

# 🎯 Common Use Cases

✔ Shared web content across EC2 instances  
✔ Container storage (EKS / ECS)  
✔ WordPress shared uploads  
✔ CI/CD artifact storage  
✔ Big data & analytics workloads  
✔ Machine learning workloads  

---

# 🔐 EFS Best Practices

✔ Use lifecycle policies to reduce cost  
✔ Enable encryption at rest  
✔ Restrict security groups  
✔ Choose correct performance mode  
✔ Monitor burst credits  
✔ Use Elastic Throughput for dynamic apps  

---

# 🎯 Important Interview Questions

1. What is AWS EFS?
2. Difference between EFS and EBS?
3. Is EFS multi-AZ?
4. Which protocol does EFS use?
5. What is mount target?
6. What is bursting throughput?
7. Can multiple EC2 instances access EFS?
8. How is EFS secured?
9. When to use EFS over S3?
10. Difference between EFS and FSx?

---

# 🧠 Quick Summary

- EFS = Managed NFS file storage
- Multi-AZ & highly available
- Used for shared storage
- Scales automatically
- Secure & encrypted


---

⭐ If this helped you, consider starring the repository!