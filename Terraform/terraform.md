# 🌍 Terraform Complete Guide (Beginner to Intermediate)

Terraform is an **Infrastructure as Code (IaC)** tool that allows you to **define, create, update, and manage infrastructure using code** instead of manual steps.

---

## 🚀 Why Terraform?

- Automates infrastructure provisioning
- Works with multiple cloud providers
- Infrastructure is version-controlled
- Repeatable, reliable, and scalable
- Reduces human errors

---

## 🧠 What is Infrastructure as Code (IaC)?

Infrastructure as Code (IaC) means managing infrastructure using **code files**.

Instead of manually creating servers, networks, or databases, you define them in files and Terraform creates them automatically.

---

## 🏗️ Terraform Architecture

- **Terraform CLI** – Command-line tool
- **Providers** – Connect Terraform to cloud platforms
- **Resources** – Infrastructure components
- **State File** – Tracks current infrastructure

---

## 📦 Terraform Basic Syntax (HCL)

Terraform uses **HCL (HashiCorp Configuration Language)**.

### Basic Structure

```hcl
block_type "label1" "label2" {
  key = "value"
}
```

### Example

```hcl
resource "aws_instance" "web" {
  instance_type = "t2.micro"
}
```

---

## 🔌 Provider Block (Very Important)

A provider tells Terraform which cloud platform to use.

### Syntax

```hcl
provider "aws" {
  region = "ap-south-1"
}
```

### Explanation

- `provider "aws"` → Use AWS
- `region` → Where resources will be created

### Common Providers

- AWS
- Azure
- Google Cloud (GCP)
- Kubernetes
- Docker

---

## 🧱 Resource Block

A resource defines what infrastructure to create.

### Syntax

```hcl
resource "provider_resource" "resource_name" {
  argument = value
}
```

### Example – EC2 Instance

```hcl
resource "aws_instance" "web" {
  ami           = "ami-0abcdef"
  instance_type = "t2.micro"
}
```

### Explanation

- `aws_instance` → Resource type
- `web` → Logical name
- `ami` → OS image
- `instance_type` → Server size

---

## 🔑 Variables

Variables make code reusable and flexible.

### Define Variable

```hcl
variable "instance_type" {
  default = "t2.micro"
}
```

### Use Variable

```hcl
instance_type = var.instance_type
```

---

## 📤 Output Values

Outputs display important values after infrastructure is created.

### Example

```hcl
output "public_ip" {
  value = aws_instance.web.public_ip
}
```

---

## 📂 Terraform State

Terraform stores infrastructure details in:

```
terraform.tfstate
```

### Purpose

- Tracks created resources
- Helps Terraform detect changes

⚠️ Never edit state file manually.

---

## 🌐 Remote State (Best Practice)

Remote state is used for:

- Team collaboration
- Backup
- State locking

### Example – S3 Backend

```hcl
terraform {
  backend "s3" {
    bucket = "terraform-state-bucket"
    key    = "dev/terraform.tfstate"
    region = "ap-south-1"
  }
}
```

---

## 🧩 Modules

Modules are reusable Terraform configurations.

### Example

```hcl
module "vpc" {
  source = "./vpc"
}
```

### Benefits

- Clean code
- Reusability
- Standardization

---

# 🖥 Install Terraform on Ubuntu (AWS EC2)

This guide explains how to install Terraform on Ubuntu 20.04 / 22.04.

---

## Prerequisites

- Ubuntu EC2 instance
- SSH access
- Internet access

---

## Step 1: Launch EC2 Instance

- Choose Ubuntu AMI
- Attach IAM role (AdministratorAccess)
- Allow SSH (Port 22)

---

## Step 2: SSH into Instance

```bash
ssh ubuntu@<EC2_PUBLIC_IP>
```

---

## Step 3: Update System

```bash
sudo apt update && sudo apt upgrade -y
```

---

## Step 4: Install Terraform

```bash
wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update && sudo apt install terraform -y
```

---

## Step 5: Verify Installation

```bash
terraform version
```

---

# 🔄 Terraform Workflow

```bash
terraform init     # Initialize project
terraform plan     # Preview changes
terraform apply    # Create/update infrastructure
terraform destroy  # Delete infrastructure
```

---

## 🧪 Important Terraform Commands

```bash
terraform fmt
terraform validate
terraform show
terraform output
terraform state list
```

---

## 📁 Recommended Project Structure

```
terraform-project/
│── provider.tf
│── main.tf
│── variables.tf
│── outputs.tf
│── terraform.tfvars
```

---

## 🔐 Security Best Practices

- Never hardcode secrets
- Use IAM roles
- Store state remotely
- Add `terraform.tfstate` to `.gitignore`

---
## 🧠 Kubernetes Controller Comparisons (From Notes)


# 1️⃣ ReplicaSet vs StatefulSet

| ReplicaSet | StatefulSet |
|------------|-------------|
| It maintains a specified number of identical pods running at all times. | It manages stateful pods that require unique identity & persistent storage. |
| Mainly used for stateless applications. | Used for stateful applications. |
| Pod names are randomly generated. | Pods have fixed and ordered names. |
| Pods are created and deleted in any order. | Pods are created sequentially and deleted in reverse order. |
| If a pod fails, a new pod is created with a different identity. | If a pod fails, it is created with the same identity & storage. |
| Commonly created automatically by Deployment. | Created directly using StatefulSet YAML manifest. |
| Example use case: Web applications. | Example use case: MongoDB, MySQL. |

---

# 2️⃣ ReplicationController vs ReplicaSet

| ReplicationController | ReplicaSet |
|------------------------|------------|
| ReplicationController is the older K8s controller used to maintain a specified number of pod replicas. | ReplicaSet is newer & improved version used to maintain a specified number of pod replicas. |
| Supports only equality-based selector. | Supports set-based selector along with equality-based selector. |
| ReplicationController is deprecated in modern Kubernetes usage. | ReplicaSet is actively used & recommended. |
| Usually created using a YAML file manually. | Often created automatically by a Deployment. |
| Limited features compared to ReplicaSet. | ReplicaSet is the improved replacement for ReplicationController. |

---

# 3️⃣ ReplicaSet vs Deployment

| ReplicaSet | Deployment |
|------------|------------|
| ReplicaSet ensures that a fixed number of pods are always running. | Deployment manages lifecycle & updates of an application. |
| ReplicaSet directly manages & creates pods. | Deployment manages ReplicaSet which then manages pods. |
| It does not support rolling updates and rollback. | It supports rolling updates & rollback to previous versions. |
| Mainly used to maintain pod replicas. | Used for deploying, updating & scaling applications. |
| ReplicaSet is not usually used directly. | Deployment is used to deploy applications. |

---

# 4️⃣ DaemonSet vs StatefulSet

| DaemonSet | StatefulSet |
|------------|-------------|
| DaemonSet runs one pod on every node in the cluster. | StatefulSet runs pods with unique identity & stable storage. |
| Pods are identical on all nodes. | Each pod is unique. |
| Pod scheduling depends on number of nodes. | Pod scheduling depends on replica count. |
| Names of the pods are not fixed. | Names of the pods are fixed & ordered. |
| Pods are created at once. | Pods are created in order. |
| Mostly used for logging, monitoring, networking agents. | Mostly used in databases like MongoDB, MySQL. |

---

# 5️⃣ ReplicationController vs Deployment

| ReplicationController | Deployment |
|------------------------|------------|
| It ensures a specified number of pods are running at all times. | Deployment manages application deployment and updates. |
| ReplicationController directly creates & manages pods. | It manages & creates ReplicaSets which then manage pods. |
| Does not support rolling updates & rollbacks. | It supports rolling updates as well as rollback to previous versions. |
| It uses equality-based selectors only. | Uses set-based and equality-based selectors. |
| It is older K8s controller. | It is newer & advanced controller. |

---

# 6️⃣ Docker vs Kubernetes

| Docker | Kubernetes |
|--------|------------|
| Docker is a containerization platform. | Kubernetes is a container orchestration platform. |
| It is used to build, package, and run containers. | It is used to manage, deploy, and scale containers. |
| Works on a single host (by default). | Works on a cluster of multiple nodes. |
| Manages individual containers. | Manages multiple containers across multiple servers. |
| No built-in auto scaling. | Supports auto scaling of pods. |
| No built-in self-healing. | Supports self-healing (restarts failed pods automatically). |
| Simple to set up and use. | More complex setup compared to Docker. |
| Uses Docker Engine to run containers. | Uses container runtime (Docker, containerd, etc.) to run containers. |
| Focus is on container creation. | Focus is on container orchestration. |
| Example: Running a Node.js app in a container. | Example: Managing thousands of containers in production. |

---

## 🔎 Simple Explanation

- **Docker** → Creates and runs containers.
- **Kubernetes** → Manages and controls containers at scale.

---

## 📌 Real World Analogy

- Docker = You pack lunch boxes.
- Kubernetes = You manage delivery of thousands of lunch boxes to different locations.

---

## 🧠 Terraform Interview Concepts

- What is Terraform state?
- Difference between plan and apply
- What is a provider?
- What are modules?
- Local vs Remote state

---

🎯 You now have a complete beginner-to-intermediate Terraform guide.