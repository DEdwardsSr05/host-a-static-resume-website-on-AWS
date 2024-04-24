![ALT text](/Mole-task-1.drawio.png)

# Hosting a Static Website on AWS

This project demonstrates the deployment of a static HTML web application on AWS, leveraging various AWS services to ensure reliability, scalability, and security.

## Architecture Overview

The project utilizes the following AWS resources:

1. **Virtual Private Cloud (VPC)**: A VPC is created with both public and private subnets across two different availability zones, providing a secure and isolated network environment.
2. **Internet Gateway**: An Internet Gateway is configured to facilitate connectivity between the VPC instances and the wider internet.
3. **Security Groups**: Security Groups are used as a network firewall mechanism, controlling inbound and outbound traffic to the resources within the VPC.
4. **Availability Zones**: The solution is designed to span two Availability Zones, enhancing system reliability and fault tolerance.
5. **Public Subnets**: Public subnets are used for infrastructure components, such as the NAT Gateway and Application Load Balancer, allowing internet-facing access.
6. **EC2 Instance Connect Endpoint**: The EC2 Instance Connect Endpoint is utilized to enable secure connections to assets within both public and private subnets.
7. **Private Subnets**: The web servers (EC2 instances) are positioned within private subnets, enhancing the overall security of the application.
8. **NAT Gateway**: The NAT Gateway enables instances in the private Application and Data subnets to access the internet while keeping them isolated from public access.
9. **EC2 Instances**: The website is hosted on EC2 Instances, which are automatically managed by an Auto Scaling Group.
10. **Application Load Balancer**: An Application Load Balancer is used to evenly distribute web traffic to the Auto Scaling Group of EC2 instances across multiple Availability Zones.
11. **Auto Scaling Group**: The Auto Scaling Group automatically manages the EC2 instances, ensuring website availability, scalability, fault tolerance, and elasticity.
12. **GitHub**: The web files are stored on GitHub for version control and collaboration.
13. **AWS Certificate Manager**: The application communications are secured using a certificate from AWS Certificate Manager.
14. **AWS Simple Notification Service (SNS)**: SNS is configured to alert about activities within the Auto Scaling Group.
15. **AWS Route 53**: The domain name is registered, and the DNS record is set up using AWS Route 53.

## Deployment Steps

1. Configure the VPC with public and private subnets across two Availability Zones.
2. Create the Internet Gateway and establish the necessary routing tables.
3. Define the Security Groups to control inbound and outbound traffic.
4. Provision the NAT Gateway and the Application Load Balancer in the public subnets.
5. Set up the EC2 Instance Connect Endpoint to enable secure connections.
6. Deploy the web servers (EC2 instances) in the private subnets.
7. Create the Auto Scaling Group and configure the Application Load Balancer to distribute traffic.
8. Store the web files on GitHub for version control and collaboration.
9. Obtain and configure the SSL/TLS certificate using AWS Certificate Manager.
10. Set up the SNS topic to receive notifications about the Auto Scaling Group activities.
11. Register the domain name and configure the DNS record using AWS Route 53.

## Scripts

The following scripts are provided to automate the deployment process:

#!/bin/bash

# Switch to the root user to gain full administrative privileges
sudo su

# Update all installed packages to their latest versions
yum update -y

# Install Apache HTTP Server
yum install httpd -y

# Change the current working directory to the Apache web root
cd /var/www/html

# Install Git
yum install git -y

# Clone the project GitHub repository to the current directory
git clone https://github.com/DEdwardsSr05/host-a-static-resume-website-on-AWS.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-resume-website-on-AWS/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-resume-website-on-AWS

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd 

# Start the Apache HTTP Server to serve web content
systemctl start httpd


The script will perform the necessary steps to set up the web server and deploy the static website.

## Conclusion

This project demonstrates the deployment of a static HTML web application on AWS, leveraging various services to ensure reliability, scalability, and security. The provided scripts streamline the deployment process, making it easier to set up and maintain the web application on AWS.
