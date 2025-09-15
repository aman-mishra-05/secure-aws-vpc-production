# Secure AWS VPC Production Deployment

*Description:*  
Production-ready AWS VPC deployment with multi-AZ, Application Load Balancer (ALB), Auto Scaling Group (ASG), private/public subnets, NAT gateways, and Bastion host.

---

## 📌 Project Overview

This project demonstrates a *secure, highly available AWS VPC* for production servers.  
All resources were deployed manually using the *AWS Console*.

- Servers run in *private subnets* and receive traffic via ALB  
- NAT Gateways allow private servers to access the internet  
- Bastion Host enables secure SSH access to private servers  
- Auto Scaling ensures dynamic scaling across 2 Availability Zones  

---

## 🛠 AWS Services Used

- *VPC & Subnets* (public + private)  
- *Internet Gateway & NAT Gateway*  
- *EC2 Instances* (application servers + Bastion host)  
- *Auto Scaling Group (ASG)*  
- *Application Load Balancer (ALB)*  
- *Target Groups*  
- *Security Groups*  
- *IAM Roles*  

---

## 📊 Architecture Diagram

![Architecture Diagram](architecture-diagram.png)

*Key points:*  
- Multi-AZ deployment for high availability  
- ALB distributes traffic across private EC2 instances  
- NAT gateways in both AZs for redundancy  
- Bastion host in public subnet for secure access  

---

## 🚀 Deployment Steps (Manual via AWS Console)

### 1. Create VPC & Subnets
- Create a VPC (CIDR: 10.0.0.0/16)  
- Create 2 *public subnets* and 2 *private subnets* across 2 AZs  

### 2. Configure Internet & NAT Gateways
- Attach *Internet Gateway* to VPC  
- Create *NAT Gateways* in both public subnets for private subnet internet access  

### 3. Set Up Security Groups
- *ALB SG:* HTTP (80) open to 0.0.0.0/0  
- *App SG:* Only allow traffic from ALB SG  
- *Bastion SG:* SSH from your IP only  

### 4. Deploy Bastion Host
- Launch EC2 instance in *public subnet*  
- Connect via SSH to manage private servers  

### 5. Launch Application Servers
- EC2 instances in *private subnets*  
- Install Docker / your app  
- Add /health endpoint for ALB health check  

### 6. Set Up ALB & Target Groups
- Create *Application Load Balancer* in public subnets  
- Create *Target Group* and register private EC2 instances  
- Configure ALB listener → forward to Target Group  

### 7. Configure Auto Scaling Group
- Create *ASG* for private EC2 instances  
- Attach to Target Group → set min/max/desired instance count  

### 8. Test Application
- Open *ALB DNS name* in browser → app should load  

### 9. Cleanup
- Terminate resources to avoid AWS charges  

---

## 🔮 Future Enhancements
- Add HTTPS via AWS Certificate Manager (ACM)  
- Replace EC2 + Docker with ECS/EKS  
- Add CloudWatch monitoring & alarms  
- Use SSM Session Manager instead of Bastion Host
