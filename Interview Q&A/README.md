# Scenario Based Interview Questions on EC2, IAM and VPC

### Q: You have been assigned to design a VPC architecture for a 2-tier application. The application needs to be highly available and scalable. How would you design the VPC architecture?

**A:**  
I would create 2 subnets: public and private. The public subnet would contain the load balancers and be accessible from the internet. The private subnet would host the application servers.  
I would distribute the subnets across multiple Availability Zones for high availability. Additionally, I would configure auto scaling groups for the application servers.

---

### Q: Your organization has a VPC with multiple subnets. You want to restrict outbound internet access for resources in one subnet, but allow outbound internet access for resources in another subnet. How would you achieve this?

**A:**  
Modify the route table associated with the restricted subnet by removing the default route (0.0.0.0/0) pointing to the internet gateway.  
For the other subnet, retain the route to the internet gateway.

---

### Q: You have a VPC with a public subnet and a private subnet. Instances in the private subnet need to access the internet for software updates. How would you allow internet access for instances in the private subnet?

**A:**  
Use a NAT Gateway or NAT instance in the public subnet.  
Update the private subnet’s route table to direct internet-bound traffic to the NAT Gateway/instance.

---

### Q: You have launched EC2 instances in your VPC, and you want them to communicate with each other using private IP addresses. What steps would you take to enable this communication?

**A:**  
Ensure the instances are in the same VPC.  
Place them in the same subnet or ensure peering between subnets.  
Check security group rules to allow communication via required ports/protocols.

---

### Q: You want to implement strict network access control for your VPC resources. How would you achieve this?

**A:**  
Use Network Access Control Lists (NACLs) at the subnet level to define inbound/outbound rules.  
Configure source/destination IPs, ports, and protocols to enforce access control.

---

### Q: Your organization requires an isolated environment within the VPC for running sensitive workloads. How would you set up this isolated environment?

**A:**  
Create a subnet with no route to an internet gateway—this is an isolated subnet.  
Place sensitive workloads there.  
If outbound access is needed, use a NAT Gateway/instance via another subnet.

---

### Q: Your application needs to access AWS services, such as S3 securely within your VPC. How would you achieve this?

**A:**  
Use VPC Endpoints (interface or gateway) for services like S3 or DynamoDB.  
This enables private, secure access without routing through the internet.

---

### Q: What is the difference between NACL and Security Groups? Explain with a use case.

**A:**  
- NACLs: Stateless, operate at the subnet level, good for broader rules.  
- Security Groups: Stateful, operate at instance level, good for detailed controls.  
Use both together to implement layered security—NACLs for subnet-wide restrictions, security groups for instance-specific rules.

---

### Q: What is the difference between IAM Users, Groups, Roles, and Policies?

**A:**  
- **IAM User**: Represents a person or app with credentials.  
- **IAM Group**: Collection of IAM Users. Permissions are attached to groups.  
- **IAM Role**: Used to delegate access, assumed temporarily by users/services.  
- **IAM Policy**: JSON document that defines permissions. Attached to Users, Groups, or Roles.

---

### Q: You have a private subnet in your VPC that contains instances with no direct internet access. However, you need to securely access these instances for administrative purposes. How would you set up a bastion host?

**A:**  
- Launch a bastion host EC2 instance in a public subnet with a public IP.  
- Allow inbound SSH/RDP only from trusted IPs.  
- Allow inbound traffic from the bastion host security group to private instances.  
- Connect to the bastion, then use it to SSH/RDP into private instances.
