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


## 🧠 Terraform Interview Concepts

- What is Terraform state?
- Difference between plan and apply
- What is a provider?
- What are modules?
- Local vs Remote state

---

🎯 You now have a complete beginner-to-intermediate Terraform guide.