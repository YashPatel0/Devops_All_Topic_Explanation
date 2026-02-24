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

# 💾 Attach a 10GB EBS Volume and Permanently Mount It to an EC2 Instance

> Step-by-step guide to create a 10GB EBS volume, attach it to an EC2 instance, format it, and configure permanent mounting using `/etc/fstab`.

---

# 📌 Overview

In AWS, additional storage can be attached to an EC2 instance using **EBS (Elastic Block Store)**.

This guide will help you:

- Create a 10GB EBS volume
- Attach it to EC2
- Partition and format it
- Mount it permanently
- Ensure data persists after reboot

---

# ✅ Prerequisites

- AWS Account
- Running Linux EC2 instance
- SSH access to instance
- EC2 and EBS in the same Availability Zone

---

# 🚀 Step 1: Create a 10GB EBS Volume

1. Go to **AWS Console**
2. Navigate to **EC2 Dashboard**
3. Click **Elastic Block Store → Volumes**
4. Click **Create Volume**
5. Configure:
   - Size: **10 GB**
   - Volume Type: gp3 (Recommended)
   - Availability Zone: Same as EC2 instance
6. Click **Create Volume**

---

# 🔗 Step 2: Attach Volume to EC2 Instance

1. Select the created volume
2. Click **Actions → Attach Volume**
3. Choose your EC2 instance
4. Set Device Name:

```
/dev/xvdf
```

5. Click **Attach**

---

# 🔐 Step 3: Connect to EC2

```bash
ssh -i key.pem ec2-user@<public-ip>
```

---

# 🔍 Step 4: Verify the Attached Volume

```bash
lsblk
```

Example Output:

```
nvme0n1   8:0    0   20G  0 disk
└─nvme0n1p1
nvme1n1   8:16   0   10G  0 disk
```

Your new volume will appear as:

- `/dev/xvdf` (older instances)
- `/dev/nvme1n1` (Nitro-based instances)

---

# 🧱 Step 5: Create Partition (Optional but Recommended)

```bash
sudo fdisk /dev/nvme1n1
```

Inside `fdisk`:

- Press `n` → Create new partition
- Press `p` → Primary
- Press `Enter` → Default
- Press `Enter` → Use full disk (or type `+5G` if partial)
- Press `w` → Write changes

Verify:

```bash
lsblk
```

You should see something like:

```
nvme1n1p1
```

---

# 🗂 Step 6: Format the Partition

For XFS (recommended for Amazon Linux):

```bash
sudo mkfs.xfs /dev/nvme1n1p1
```

For EXT4:

```bash
sudo mkfs.ext4 /dev/nvme1n1p1
```

---

# 📁 Step 7: Create Mount Directory

```bash
sudo mkdir /mnt/data
```

---

# 📌 Step 8: Mount the Volume

```bash
sudo mount /dev/nvme1n1p1 /mnt/data
```

Verify:

```bash
df -h
```

---

# 🔑 Step 9: Get UUID (Best Practice for Permanent Mount)

```bash
sudo blkid
```

Example Output:

```
/dev/nvme1n1p1: UUID="abcd-1234" TYPE="xfs"
```

Copy the UUID.

---

# 📝 Step 10: Configure Permanent Mount

Edit `/etc/fstab`:

```bash
sudo vim /etc/fstab
```

Add the following line:

```
UUID=abcd-1234   /mnt/data   xfs   defaults,nofail   0 2
```

⚠ Always use UUID instead of device name because device names may change after reboot.

---

# 🔄 Step 11: Test fstab Entry

Before rebooting, test:

```bash
sudo mount -a
```

If no error appears, configuration is correct.

---

# 🔁 Step 12: Reboot and Verify

```bash
sudo reboot
```

After reboot:

```bash
lsblk
df -h
```

Your volume should be mounted automatically.

---

# 🛡 Important Notes (DevOps Best Practices)

✔ Always use UUID in `/etc/fstab`  
✔ Use `nofail` option to prevent boot failure  
✔ Ensure correct Availability Zone  
✔ Take EBS snapshots regularly  
✔ Use gp3 for better performance and cost efficiency  
✔ Avoid editing `/etc/fstab` without testing using `mount -a`  

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