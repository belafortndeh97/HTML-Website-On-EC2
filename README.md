AWS Web Hosting with EC2 Readme

Project Overview:
This DevOps project utilizes AWS services to host a simple HTML web application on an EC2 instance. The architecture includes a VPC with public and private subnets distributed across two availability zones, ensuring high availability and fault tolerance. The web servers are placed in private subnets, protected by security groups, while resources like NAT Gateway, Bastion Host, and Application Load Balancer reside in public subnets.

AWS Resources Used 

VPC Configuration:
VPC with public and private subnets across two availability zones.
Internet Gateway for communication between instances in the VPC and the internet.

Security Groups:
Configured security groups for firewall rules to control inbound and outbound traffic.

High Availability and Fault Tolerance:
Utilized two availability zones for high availability and fault tolerance.

Public Subnet Resources:
NAT Gateway for instances in private app subnets.
Bastion Host for secure access to instances in private subnets.
Application Load Balancer for distributing web traffic.

Private Subnet Resources:
EC2 instances hosting the website.
Auto Scaling Group for dynamic creation of EC2 instances, ensuring scalability, fault tolerance, and elasticity.

Domain Management:
Used Route 53 to register the domain name and create a record set.

File Storage:
Employed an S3 bucket to store web files, enhancing scalability and flexibility.

Web App Deployment Script:
The provided script automates the deployment of the web application on EC2 instances.


Deployment Script
The deployment script (deploy-web-app.sh) performs the following actions:


bash
Copy code
#!/bin/bash

# Switch to superuser
sudo su

# Update the system
yum update -y

# Install Apache web server
yum install -y httpd

# Navigate to the web server directory
cd /var/www/html

# Download and unzip the web app files from the S3 bucket
wget https://aosnotes-website-project2.s3.us-east-2.amazonaws.com/xmen-main.zip
unzip xmen-main.zip

# Copy the web app files to the web server directory
cp -r xmen-main/* /var/www/html

# Clean up downloaded files
rm -rf xmen-main xmen-main.zip

# Enable and start the Apache web server
systemctl enable httpd
systemctl start httpd


Usage:
Clone this repository to your local machine.
Review and customize the deployment script if necessary.
Execute the script on your EC2 instance to deploy the web application.

bash
Copy code
./deploy-web-app.sh


Additional Notes:
To achieve high availability, scalability, fault tolerance, and elasticity, EC2 instances are launched and managed by an Auto Scaling Group.
Use the provided Route 53 configuration for domain registration and DNS management.
Web files are stored in an S3 bucket, allowing for easy updates and scalability.
Feel free to reach out for any clarifications or improvements to the project. 
Happy coding!
