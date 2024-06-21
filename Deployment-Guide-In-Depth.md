# Complete Guide to Deploying a Spring Boot Microservices Project with Oracle DB on AWS

- This guide is the step-wise explanation of deployoning full fledged database connected  Spring Boot application which have multiple microservices , Spring cloud api gateway , Eureka Discovery server and Config server.

## Introduction

This guide provides a step-by-step walkthrough for deploying a full-fledged Spring Boot microservices project connected with Oracle DB on AWS. It covers the setup of AWS resources, deployment of Spring Boot microservices, and configuration of Oracle DB.

## Prerequisites

Before you begin, ensure you have the following:

- An AWS account
- Basic knowledge of AWS services
- Java Development Kit (JDK) installed
- Maven installed
- Initial setup of Oracle Database

## Architecture Overview

1. **AWS Services Used**:
   - Amazon EC2
   - Amazon RDS (Oracle DB)
   - Amazon VPC
   - AWS IAM
   - Amazon S3 (optional for static content)

2. **Spring Boot Microservices**:
   - Multiple microservices each running on separate EC2 instances
   - Configured to connect to a central Oracle DB hosted on Amazon RDS

## Step-by-Step Deployment Guide

### Step 1: Setup AWS Infrastructure

#### 1.1 Create a VPC

1. Go to the VPC Dashboard in AWS Management Console.
2. Create a new VPC with a CIDR block (e.g., 10.0.0.0/16).
3. Create public and private subnets in different Availability Zones.
4. Create and attach an Internet Gateway to the VPC.
5. Create route tables and associate them with the subnets.

#### 1.2 Setup Security Groups

1. Create a security group for the EC2 instances allowing inbound traffic on ports 80 (HTTP), 443 (HTTPS), and custom application ports.
2. Create a security group for the RDS instance allowing inbound traffic on the Oracle DB port (default 1521).

### Step 2: Setup Amazon RDS for Oracle DB

1. Navigate to the RDS Dashboard and create a new database instance.
2. Select Oracle as the engine and configure instance settings (DB instance class, storage, etc.).
3. Set up the master username and password.
4. Configure the security group to allow EC2 instances to connect to the RDS instance.
5. Note the endpoint and port of the RDS instance for later use.

### Step 3: Setup EC2 Instances for Microservices

#### 3.1 Launch EC2 Instances

1. Go to the EC2 Dashboard and launch instances for each microservice.
2. Select an appropriate instance type (e.g., t2.micro for development).
3. Use the security group created earlier for these instances.

#### 3.2 Install Java and Maven

1. SSH into each EC2 instance.
2. Install Java JDK:
   ```bash
   sudo yum update -y
   sudo yum install -y java-1.8.0-openjdk
   ```
3. Install Maven:  
   ```bash
   sudo yum install -y maven
   ```

### Step 4: Deploy Spring Boot Microservices
#### 4.1 Package Microservices  
1. Use Maven to package your Spring Boot applications into executable JAR files:
    ```bash
    mvn clean package
    ```
#### 4.2 Transfer JAR Files to EC2
1. Use SCP or any other method to transfer JAR files to respective EC2 instances:
    ```bash
    scp -i /path/to/your-key.pem your-microservice.jar ec2-user@your-ec2-ip:/home/ec2-user/
    ```

#### 4.3 Run Microservices
1. SSH into each EC2 instance and start the Spring Boot applications:
    ```bash
    java -jar your-microservice.jar
    ```
### Step 5: Setup Spring Cloud Config Server
1. Deploy the Config Server as a Spring Boot application on an EC2 instance.
2. Ensure all microservices point to this Config Server for configuration properties.

### Step 6: Setup Eureka Discovery Server
1. Deploy the Eureka Discovery Server as a Spring Boot application on an EC2 instance.
2. Configure all microservices to register with the Eureka server.

### Step 7: Setup Spring Cloud API Gateway
1. Deploy the API Gateway as a Spring Boot application on an EC2 instance.
2. Configure routing and load balancing through the API Gateway.

### Step 8: Deploy Thymeleaf Frontend
1. Ensure all HTML, CSS, and JS files are in the resources folder of the Controller Service.
2. Start the Controller Service and verify that the frontend is accessible.

### Step 9: Monitoring and Logging
#### 9.1 Setup Amazon CloudWatch
1. Configure CloudWatch to monitor your EC2 instances and RDS instance.
2. Set up alarms for critical metrics like CPU usage, memory usage, and DB connections.

#### 9.2 Centralized Logging
1. Use CloudWatch Logs or other logging solutions to centralize logs from your microservices.

### Step 10: Implement CI/CD Pipeline (Optional)
#### 10.1 Setup a CI/CD Tool
1. Use a CI/CD tool like Jenkins, GitHub Actions, or AWS CodePipeline.
2. Configure the CI/CD pipeline to automate the build, test, and deployment processes.

### Step 11: Configure Security and Networking (Optional)
#### 11.1 Enable HTTPS
1. Obtain an SSL certificate and configure your API Gateway and EC2 instances to use HTTPS.

#### 11.2 Use IAM Roles
1. Assign IAM roles to your EC2 instances to securely access other AWS services.


## Conclusion
This detailed guide covers all the steps needed to deploy your Spring Boot microservices project on AWS, including setting up the infrastructure, deploying the services, and configuring monitoring and logging. For more advanced setups, consider implementing a CI/CD pipeline and enhancing security measures.

## Additional Resources
- [AWS Documentation](https://docs.aws.amazon.com/)
- [Spring Boot Documentation](https://spring.io/projects/spring-boot)
- [Oracle Database Documentation](https://docs.oracle.com/en/database/)
- [AWS RDS for Oracle](https://aws.amazon.com/rds/oracle/)
- [AWS EC2](https://aws.amazon.com/ec2/)

----
This guide provides a comprehensive walkthrough of deploying your Spring Boot microservices project on AWS. Follow each step carefully to ensure a successful deployment.
