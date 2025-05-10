📘 Scenario-Based Interview Questions on EC2, IAM, and VPC
This document contains a collection of practical, scenario-based interview questions and answers focused on AWS services such as EC2, IAM, and VPC. Useful for job interviews, revision, and hands-on AWS learning.

📌 Table of Contents
1. VPC Architecture for a 2-Tier Application

2. Restricting Outbound Internet Access

3. Internet Access for Private Subnet Instances

4. EC2 Private Communication

5. Implementing Network Access Control

6. Isolated Environment for Sensitive Workloads

7. Secure Access to AWS Services from VPC

8. NACLs vs Security Groups

9. IAM Users, Groups, Roles, and Policies

10. Bastion Host Setup

1. VPC Architecture for a 2-Tier Application
Q: How would you design a VPC architecture for a 2-tier application that is highly available and scalable?

A:

Create a VPC with public and private subnets.

Place load balancers in the public subnet.

Deploy application servers in private subnets.

Distribute subnets across multiple Availability Zones.

Use Auto Scaling groups for the application servers for scalability.

2. Restricting Outbound Internet Access
Q: How can you restrict outbound internet access for one subnet but allow it for another?

A:

Modify the route table for the restricted subnet: remove the route to the internet gateway (0.0.0.0/0).

Retain the internet gateway route for the subnet that requires outbound internet access.

3. Internet Access for Private Subnet Instances
Q: How can instances in a private subnet access the internet for software updates?

A:

Use a NAT Gateway or NAT instance in a public subnet.

Update the private subnet's route table to direct internet-bound traffic to the NAT resource.

4. EC2 Private Communication
Q: How can EC2 instances communicate privately?

A:

Launch instances in the same VPC (same or peered subnets).

Ensure security group rules allow inbound/outbound private IP traffic between the instances.

5. Implementing Network Access Control
Q: How would you implement strict access control at the subnet level?

A:

Use Network ACLs (NACLs) for stateless control at the subnet level.

Configure specific inbound and outbound rules based on IPs, ports, and protocols.

6. Isolated Environment for Sensitive Workloads
Q: How do you create an isolated subnet for sensitive workloads?

A:

Create a subnet without an internet gateway.

Place sensitive instances in this isolated subnet.

Optionally, route outbound traffic through a NAT Gateway in another subnet for controlled updates.

7. Secure Access to AWS Services from VPC
Q: How to allow VPC instances secure access to services like S3?

A:

Use VPC Endpoints (interface or gateway type depending on the service).

Allows private communication with AWS services, bypassing the internet.

8. NACLs vs Security Groups
Q: What is the difference between NACL and Security Groups? Use a scenario.

A:

NACLs: Stateless, work at the subnet level. Example: block all traffic from a specific IP range.

Security Groups: Stateful, work at the instance level. Example: only allow HTTP traffic to a web server.

Use both for layered security (defense-in-depth).

9. IAM Users, Groups, Roles, and Policies
Q: What’s the difference between IAM users, groups, roles, and policies?

A:

User: Individual identity with credentials.

Group: Collection of users managed together.

Role: Temporary access assumed by users/services.

Policy: JSON document that defines permissions.

10. Bastion Host Setup
Q: How do you access private subnet instances securely?

A:

Launch a bastion host in a public subnet with a public IP.

Allow SSH (Linux) or RDP (Windows) to the bastion host from trusted IPs.

Configure private instance security groups to allow traffic from the bastion host's security group.

SSH or RDP into private instances via the bastion.
