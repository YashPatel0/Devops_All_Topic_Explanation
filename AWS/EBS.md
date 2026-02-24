# 💾 AWS EBS (Elastic Block Store) – Complete DevOps Guide

> A beginner-friendly yet production-ready guide to Amazon Elastic Block Store (EBS) for Cloud & DevOps Engineers.

---

# 📌 Table of Contents

- What is Amazon EBS?
- Why EBS is Important
- Key Features
- Types of EBS Volumes
- EBS vs Instance Store
- EBS Architecture
- Create & Attach EBS Volume
- Mount EBS in Linux
- Permanent Mount Configuration
- EBS Snapshots (Backup)
- EBS Encryption
- Resize EBS Volume
- Performance Factors
- Pricing Overview
- Real-World Use Cases
- Best Practices
- Important Interview Questions

---

# 🚀 What is Amazon EBS?

Amazon Elastic Block Store (EBS) is a **persistent block-level storage service** designed for use with Amazon EC2 instances.

Think of it as:

- 🖥 EC2 → Computer (CPU + RAM)
- 💾 EBS → Hard Disk (Storage)

Without EBS, your EC2 would not have permanent storage.

---

# 🎯 Why Do We Need EBS?

EBS is used to:

- Store Operating System files (Root volume)
- Store application data
- Store databases
- Store logs
- Keep data safe even after instance stop/start

✔ Data persists after reboot  
✔ Data persists after EC2 stop/start  
❌ Data is deleted only if volume is deleted

---

# 🔑 Key Features of EBS

- Persistent storage
- High durability (replicated within AZ)
- Snapshot support
- Encryption support (KMS)
- Resize anytime
- Attach/detach capability
- High performance options available

---

# 📦 Types of EBS Volumes

## 1️⃣ General Purpose SSD (gp3 / gp2)

- Balanced performance and cost
- Default choice for most workloads
- Ideal for web servers & small databases

👉 **Recommended: gp3**

---

## 2️⃣ Provisioned IOPS SSD (io1 / io2)

- High IOPS
- Low latency
- Used for large production databases

---

## 3️⃣ Throughput Optimized HDD (st1)

- Large sequential workloads
- Big data processing

---

## 4️⃣ Cold HDD (sc1)

- Lowest cost
- Infrequently accessed data

---

# 📊 EBS vs Instance Store

| Feature        | EBS | Instance Store |
|---------------|-----|----------------|
| Persistent    | Yes | No |
| Backup        | Yes (Snapshots) | No |
| Attach/Detach | Yes | No |
| AZ Bound      | Yes | Yes |
| Use Case      | Databases, Apps | Temporary cache |

---

# 🏗 EBS Architecture

- EBS volumes are **Availability Zone (AZ) specific**
- Must be in same AZ as EC2
- Automatically replicated within AZ

Example:

EC2 in `ap-south-1a`  
EBS must be in `ap-south-1a`

---

# 🚀 Step-by-Step: Create & Attach EBS Volume

## Step 1: Create Volume

1. Go to AWS Console
2. EC2 → Elastic Block Store → Volumes
3. Click **Create Volume**
4. Choose:
   - Volume type: gp3
   - Size: 10GB
   - Same AZ as EC2
5. Click **Create Volume**

---

## Step 2: Attach Volume

1. Select the volume
2. Click **Actions → Attach Volume**
3. Select EC2 instance
4. Device name:

```
/dev/xvdf
```

---

# 🔐 Mount EBS Volume in Linux (Amazon Linux / Ubuntu)

## Step 3: Verify Volume

```bash
lsblk
```

On Nitro instances, device may appear as:

```
/dev/nvme1n1
```

---

## Step 4: Format Volume

EXT4:

```bash
sudo mkfs.ext4 /dev/nvme1n1
```

XFS (Amazon Linux recommended):

```bash
sudo mkfs.xfs /dev/nvme1n1
```

---

## Step 5: Create Mount Directory

```bash
sudo mkdir /data
```

---

## Step 6: Mount Volume

```bash
sudo mount /dev/nvme1n1 /data
```

Verify:

```bash
df -h
```

---

# 🔁 Make EBS Persistent After Reboot (Best Practice Method)

⚠ Always use UUID instead of device name.

## Step 7: Get UUID

```bash
sudo blkid
```

Example:

```
UUID="abcd-1234"
```

---

## Step 8: Edit fstab

```bash
sudo nano /etc/fstab
```

Add:

```
UUID=abcd-1234   /data   ext4   defaults,nofail   0 2
```

---

## Step 9: Test Configuration

```bash
sudo mount -a
```

If no errors → safe to reboot.

---

# 📸 EBS Snapshots (Backup)

## What is Snapshot?

A snapshot is a **backup of an EBS volume stored in S3**.

- Incremental backup
- Can restore anytime
- Can create new volumes from snapshot

---

## Create Snapshot

EC2 → Volumes → Select Volume → Actions → Create Snapshot

---

## Restore Volume from Snapshot

EC2 → Snapshots → Select Snapshot → Create Volume

---

# 🔐 EBS Encryption

EBS supports encryption:

- Encryption at rest
- Encryption in transit
- Uses AWS KMS

✔ Enable encryption during creation  
✔ Cannot disable encryption after creation  

---

# 📈 Resize EBS Volume (Increase Size)

## Step 1: Modify Volume Size (Console)

Increase size from 10GB → 20GB

## Step 2: Resize File System in EC2

EXT4:

```bash
sudo resize2fs /dev/nvme1n1
```

XFS:

```bash
sudo xfs_growfs /data
```

---

# ⚡ EBS Performance Depends On

- Volume type
- IOPS
- Throughput
- EC2 instance type
- Network performance

---

# 💰 EBS Pricing Overview

You are charged for:

- Storage (GB/month)
- Provisioned IOPS (if io1/io2)
- Snapshot storage
- Data transfer (if applicable)

⚠ Stopped EC2 still incurs EBS cost.

---

# 🌍 Real-World Use Cases

- EC2 root volume
- Production database storage
- Application data
- Log storage
- CI/CD artifact storage

---

# 🛡 EBS Best Practices

✔ Use gp3 for most workloads  
✔ Enable encryption  
✔ Take regular snapshots  
✔ Use UUID in fstab  
✔ Monitor with CloudWatch  
✔ Do not open SSH to 0.0.0.0/0  
✔ Use IAM roles instead of access keys  

---

# 🎯 Important Interview Questions

1. What is EBS?
2. Difference between EBS and EFS?
3. Difference between EBS and Instance Store?
4. What is snapshot?
5. Is EBS multi-AZ?
6. What happens when EC2 is terminated?
7. Can we resize EBS without downtime?
8. What is gp3?
9. Why use UUID in fstab?
10. What is encryption in EBS?

---

# 🧠 Quick Summary

- EBS = Persistent block storage
- AZ specific
- Supports snapshots
- Can resize anytime
- Use UUID for permanent mount
- gp3 recommended

---

⭐ If this repository helped you, consider giving it a star!