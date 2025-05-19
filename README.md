## AWS Cloud Infrastruture deployment architecture

![Screenshot 2025-05-19 092819](https://github.com/user-attachments/assets/9b269b1c-4d95-4818-a706-935173b78929)

This is an AWS cloud infrastructure deployment architecture diagram, illustrating the flow of CI/CD using GitHub Actions with services like Amazon ECS, ECR, S3, and VPC networking components in a multi-AZ (Availability Zone) setup. Here's a breakdown of what's happening:

---

### **1. CI/CD Pipeline (Left side)**

- **Push Code to GitHub:** The process starts when a developer pushes code to GitHub.
- **GitHub Actions Workflow:**
    - **Step 1:** Check user permissions.
    - **Step 2:** Build Docker images and push them to **Amazon ECR (Elastic Container Registry)**.
    - **Step 3:** Upload configuration and runtime files to **Amazon S3**.
    - **Step 4:** Deploy the container with:
        - Subnet info
        - Environment variables
        - S3 bucket URLs

---

### **2. AWS Infrastructure (Middle section)**

- **VPC** in **Mumbai Region** (`10.10.0.0/16`):
    - Contains **2 Public Subnets** in **2 Availability Zones (AZ-1 & AZ-2)**.
    - Each subnet (`10.10.2.0/24` and `10.10.3.0/24`) contains:
        - Security Groups (inbound/outbound rules)
        - ECS tasks/services likely to be deployed here.
- **Elastic Load Balancer (ELB):**
    - Distributes traffic across multiple availability zones.
    - Entry point for external users (e.g., via `myservice-elb...elb.amazonaws.com`).
- **Internet Gateway (igw):**
    - Routes public traffic into the VPC.
- **Route Tables (RT):**
    - Manage traffic:
        - **Green (Public):** Route to Internet Gateway.
        - **Blue (Private):** Route through NAT Gateway for outbound internet.

---

### **3. Routing Tables (Right section)**

- Define **destination and targets**:
    - **Public Route Table**: Routes 0.0.0.0/0 to **igw** for internet access.
    - **Private Route Table**: Routes 0.0.0.0/0 to **NAT Gateway** for secure outbound access.
    - Local traffic (`10.10.0.0/16`) stays inside the VPC.

---

### **4. Notes on Security and Routing**

- EC2 instances in private subnets don’t need public IPs.
- Security Groups control access (firewalls).
- No special routing needed for ELB to communicate across subnets.
