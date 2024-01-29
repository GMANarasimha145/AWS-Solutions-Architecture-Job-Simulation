
# AWS Solutions Architecture Job Simulation - Partial Implementation

## Overview

This repository showcases a partial implementation of an AWS Solutions Architecture Job Simulation, as outlined in the January 2024 scenario. The architecture encompasses various AWS services, from VPC creation to the deployment of PHP instances, setting up an Application Load Balancer (ALB), configuring Amazon RDS, and integrating PHPMyAdmin.

## Implementation Steps

### 1. VPC and Subnets

- **Create VPC:** Utilize the AWS CLI to create a Virtual Private Cloud, laying the foundation for the entire architecture.
  
- **Creating Subnets:** Establish multiple subnets, including public web, private app, and private DB subnets. Associate these with respective route tables for seamless communication.

### 2. Jump Server and PHP Instances

- **Create Jump Server:** Deploy an Amazon Linux 2 instance configured for secure access. Enable auto-assign IP and set up SSH access.
  
- **Creating PHP Instances:** On the Jump Server, initialize PHP instances using specified Amazon Machine Image (AMI). Execute commands to update, install required software like MariaDB, PHP, and Apache. Customize configurations for optimal performance.

 

### 3. Application Load Balancer (ALB)

- **Create ELB:** Establish an Application Load Balancer to distribute incoming traffic across PHP instances. Ensure high availability and fault tolerance.

- **Create Security Group for ALB:** Configure security groups to regulate incoming and outgoing traffic for the ALB.

### 4. Database Setup with Amazon RDS

- **Create DB Subnet Group for RDS:** Formulate a subnet group specifically for Amazon RDS, considering network isolation.

- **Create Database:** Initialize an RDS database instance with appropriate configurations, ensuring compatibility with the overall architecture.

- **Create a S3 Bucket for Database Backup:** Establish an Amazon S3 bucket dedicated to storing backups for the RDS database.

- **Create Option Group:** Fine-tune the database setup by creating an option group to manage advanced features.

### 5. PHPMyAdmin Integration

- **Access PHPMyAdmin:** Utilize the Jump Server to log into PHP instances and configure PHPMyAdmin for database management.

  

- **ELB DNS URL Configuration:** Resolve issues related to ELB DNS URL by adjusting target group attributes, ensuring smooth integration.

- Commands:
-  ```bash
    sudo yum update -y
    sudo amazon-linux-extras install mariadb10.5
    sudo amazon-linux-extras install php8.2
    sudo yum install -y httpd
    sudo systemctl start httpd
    sudo systemctl enable httpd
    sudo systemctl is-enabled httpd
    sudo chown -R ec2-user:apache /var/www
    sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;
    find /var/www -type f -exec sudo chmod 0664 {} \;
    sudo yum install php-mbstring php-xml -y
    sudo systemctl restart httpd
    sudo systemctl restart php-fpm
    cd /var/www/html
    wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.tar.gz
    mkdir phpMyAdmin && tar -xvzf phpMyAdmin-latest-all-languages.tar.gz -C phpMyAdmin --strip-components 1
    rm phpMyAdmin-latest-all-languages.tar.gz
```

