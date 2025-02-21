# Amazon Virtual Private Cloud

## Objective

The goal of this project was to create an Amazon Virtual Private Cloud (VPC) to host an application with a web server and a MySQL database using Amazon RDS. The project involved setting up a secure cloud networking environment, configuring subnets, security groups, and routing policies to ensure controlled access and efficient communication between resources.


### Skills Learned

- Cloud networking fundamentals: VPC, subnets, internet gateways, and routing tables.
- Security best practices: Security groups, firewall rules, and least privilege access.
- Database management: Setting up Amazon RDS and connecting it to an application.
- AWS EC2 and RDS configuration: Deploying and managing cloud instances.

### Tools Used

- AWS Management Console for creating and configuring resources.
- Amazon EC2 for hosting the web server.
- Amazon RDS for managing the MySQL database.
- Security Groups & IAM Policies for access control.


## Project Outcome 
- Successfully created a secure AWS VPC with public and private subnets.
- Deployed and configured a web server connected to Amazon RDS.
- Ensured controlled access between subnets using security groups.
- Gained hands-on experience in AWS cloud networking and security.

## Steps
### Creating the VPC
Created a VPC named MyVPC with the following configurations:

IPv4 CIDR Block: 10.0.0.0/16

### Setting Up Public and Private Subnets 
Created two public subnets (10.0.1.0/24 and 10.0.2.0/24).

Created two private subnets (10.0.3.0/24 and 10.0.4.0/24).

Enabled auto-assign public IPv4 addresses for public subnets.

### Configuring the Internet Gateway 
Created and attached an Internet Gateway (IGW) to MyVPC.

Verified successful attachment of the IGW to allow internet traffic.

![Screenshot 2025-02-20 163932](https://github.com/user-attachments/assets/5cdaa64c-6b5c-468b-b6a3-b1b7336c96a1)
*Internet Gateway Associated with the VPC*

### Creating Route Tables and Routing Rules 
Created a Route Table for public subnets.

Added a default route to 0.0.0.0/0, pointing to the Internet Gateway.

Associated the public subnets with the route table.

### Configuring Security Groups 
Web Server Security Group: Allowed HTTP (port 80) access from the internet.

Database Security Group: Allowed MySQL (port 3306) access only from the web server.

### Deploying a Web Server (EC2 Instance)
Launched an Amazon Linux EC2 instance with:

t2.micro instance type

Amazon Linux 2 AMI

Web Server Security Group attached.

Configured User Data to install and start the web server automatically:

![Screenshot 2025-02-20 164917](https://github.com/user-attachments/assets/349a26cd-2375-4ad8-908e-2fa507012182)
*Commands Used to Configure User Data*

![Screenshot 2025-02-20 165126](https://github.com/user-attachments/assets/70609021-9923-41c0-a19e-23da36d39815)
*EC2 Instance with Public IPv4*

### Creating Private Subnets for MySQL Server
Created two private subnets for the RDS instance in different Availability Zones.

### Creating Security Group for the Database Server
Configured a Security Group allowing only MySQL traffic from the Web Server Security Group.

### Creating a Database Subnet Group
Created a DB Subnet Group with the private subnets to host the RDS instance.

### Deploying Amazon RDS (MySQL Database) in a Private Subnet 
Created an Amazon RDS instance with:
Creation method: Standard create

Engine type: Aurora (MySQL compatible)

Template: Dev/Test

Instance class: db.t3.small

Subnet group: Select the created DB subnet group

VPC Security Group: Attach the Database Security Group

Set Initial database name to myDB

Disable Auto Minor Version Upgrade

Copied the Database Endpoint from the Connectivity & Security section

![Screenshot 2025-02-20 170744](https://github.com/user-attachments/assets/d92b9d60-81c5-4ac2-8bd5-b7600b2f7bff)
*Amazon RDS Database*

### Connecting the Address Book Application to RDS
Accessed the web server using its public IP address.

Configured the application database settings:

Endpoint: Copied the RDS endpoint from the Connectivity & Security section

Database Name: myDB

Verified that the applicatoon successfully connected to the database

![Screenshot 2025-02-20 170744](https://github.com/user-attachments/assets/69bf9f47-97c5-4f3a-b7ae-ed37031e9631)
*Address Book Application Successfully Connected to the Database*

## Future Improvements 
- Implement a NAT Gateway for secure outbound traffic from private subnets.
- Use AWS IAM Roles to improve security and manage access.
- Automate VPC deployment using AWS CloudFormation.
- Expand to multi-region deployments for higher availability.







