# AWS Elastic Load Balancing (ELB) – Complete Beginner Guide

This **README.md** explains **AWS Elastic Load Balancing (ELB)** in a **simple, step-by-step way** so that even a beginner can understand it easily.

---

## What is Elastic Load Balancing?

**Elastic Load Balancing (ELB)** automatically distributes incoming traffic across multiple targets such as:

- EC2 instances  
- Containers  
- IP addresses  

👉 Think of a Load Balancer like a **traffic manager** that sends users to different servers so no single server becomes overloaded.

Without a Load Balancer:

- One server handles all traffic  
- If it crashes → Application goes down  

With a Load Balancer:

- Traffic is distributed  
- High availability is maintained  
- Application becomes fault tolerant  

---

## Why Do We Need Load Balancer?

Load Balancer is used to:

- Improve application availability  
- Distribute traffic evenly  
- Handle high traffic automatically  
- Remove unhealthy servers automatically  
- Improve scalability  

> **If one server fails, traffic is automatically redirected to healthy servers**

---

## Types of AWS Load Balancers

### 1. Application Load Balancer (ALB)

- Works at Layer 7 (HTTP/HTTPS)
- Supports path-based routing (`/api`, `/login`)
- Best for web applications
- Supports SSL termination

---

### 2. Network Load Balancer (NLB)

- Works at Layer 4 (TCP/UDP)
- Ultra-high performance
- Low latency
- Supports static IP

---

### 3. Gateway Load Balancer (GWLB)

- Used for security appliances
- Firewall and traffic inspection
- Works with third-party security tools

---

## Key Components of Load Balancer

- **Listener** – Checks incoming requests (HTTP/HTTPS)
- **Target Group** – Contains EC2 instances
- **Health Check** – Monitors server health
- **Availability Zones** – Provides high availability

---

## Load Balancer Architecture

Example flow:

User → Load Balancer → Target Group → EC2 Instances  

Load Balancer distributes traffic across multiple Availability Zones for reliability.

---

## Step-by-Step: Create Application Load Balancer

### Step 1: Launch EC2 Instances

- Launch **2 EC2 instances**
- Place them in **different Availability Zones**
- Allow **HTTP (port 80)** in Security Group
- Install web server (Apache / Nginx)

Example (Ubuntu):

```bash
sudo apt update
sudo apt install apache2 -y
```

---

### Step 2: Create Target Group

1. Go to **EC2 → Target Groups**
2. Click **Create Target Group**
3. Select:
   - Target type: Instances
   - Protocol: HTTP
   - Port: 80
4. Register both EC2 instances
5. Click **Create**

---

### Step 3: Create Load Balancer

1. Go to **EC2 → Load Balancers**
2. Click **Create Load Balancer**
3. Select **Application Load Balancer**

Configure:

- Scheme: Internet-facing
- IP type: IPv4
- Listener: HTTP (80)
- Select at least 2 AZs

---

### Step 4: Configure Security Group

Inbound rule:

- HTTP (80) → 0.0.0.0/0  

Outbound rule:

- Allow all traffic

---

### Step 5: Attach Target Group

- Select the created Target Group
- Click **Create Load Balancer**
- Wait until status becomes **Active**

---

## Step 6: Test Load Balancer

1. Copy the DNS name of Load Balancer
2. Paste into browser:

```
http://your-load-balancer-dns
```

Refresh multiple times.

You should see different servers responding.

---

## Health Checks

Load Balancer automatically:

- Checks if instance is responding
- Removes unhealthy instances
- Routes traffic only to healthy instances

---

## Load Balancer vs Single EC2

| Feature | Load Balancer | Single EC2 |
|----------|---------------|------------|
| High Availability | Yes | No |
| Fault Tolerance | Yes | No |
| Auto Scaling Support | Yes | Limited |
| Traffic Distribution | Yes | No |

---

## Pricing (Simple)

You pay for:

- Running hours  
- Data processed  
- Number of requests  

---

## Real-World Use Cases

- Hosting web applications  
- Production environments  
- Microservices architecture  
- High-traffic applications  

---

## Best Practices

- Use at least 2 Availability Zones  
- Enable HTTPS using ACM  
- Use health checks properly  
- Integrate with Auto Scaling  
- Monitor using CloudWatch  

---

🎉 **You now understand AWS Load Balancer clearly and practically!**