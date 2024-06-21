# Complete Guide to Deploying a Spring Boot Microservices Project with Oracle DB on AWS

## Introduction

This guide provides a step-by-step walkthrough for deploying a full-fledged Spring Boot microservices project connected with Oracle DB on AWS. It covers the setup of AWS resources, deployment of Spring Boot microservices, and configuration of Oracle DB.

## Prerequisites

Before you begin, ensure you have the following:

- An AWS account
- Basic knowledge of AWS services
- Java Development Kit (JDK) installed
- Maven or Gradle installed
- Oracle Database setup locally for initial development

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

### Step 1: Setup VPC

1. **Create a VPC**:
   - Go to the VPC Dashboard in AWS Management Console.
   - Create a new VPC with appropriate CIDR block (e.g., 10.0.0.0/16).

2. **Create Subnets**:
   - Create public and private subnets in different Availability Zones.

3. **Internet Gateway**:
   - Create and attach an Internet Gateway to the VPC.

4. **Route Tables**:
   - Create route tables and associate them with the subnets.
   - For public subnets, add a route to the Internet Gateway.

### Step 2: Setup Amazon RDS (Oracle DB)

1. **Create an RDS Instance**:
   - Navigate to the RDS Dashboard and create a new database instance.
   - Select Oracle as the engine and configure instance settings (DB instance class, storage, etc.).
   - Set up the master username and password.

2. **Configure Security Groups**:
   - Create a security group allowing inbound traffic on the Oracle DB port (default 1521).
   - Ensure the VPC and subnets are correctly configured for RDS.

3. **Database Configuration**:
   - After the DB instance is available, note the endpoint and port.
   - Use Oracle SQL Developer or any other SQL client to connect and create necessary schemas and tables.

### Step 3: Setup EC2 Instances for Spring Boot Microservices

1. **Launch EC2 Instances**:
   - Navigate to the EC2 Dashboard and launch instances for each microservice.
   - Select an appropriate instance type (e.g., t2.micro for development).

2. **Security Groups**:
   - Create security groups allowing inbound traffic for HTTP (port 80) and custom application ports.
   - Ensure EC2 instances can connect to the Oracle RDS instance.

3. **Configure Instances**:
   - SSH into each instance and install Java JDK and Maven/Gradle.
   - Configure instances for running Spring Boot applications.

### Step 4: Deploy Spring Boot Microservices

1. **Package Microservices**:
   - Use Maven/Gradle to package your Spring Boot applications into executable JAR files.
   - `mvn clean package` or `./gradlew build`.

2. **Transfer JAR Files to EC2**:
   - Use SCP or any other method to transfer JAR files to respective EC2 instances.

3. **Run Microservices**:
   - SSH into each EC2 instance and start the Spring Boot applications.
   - `java -jar your-microservice.jar`.

4. **Configuration**:
   - Ensure each microservice is configured to connect to the Oracle DB.
   - Use environment variables or AWS Secrets Manager to manage DB credentials securely.

### Step 5: Setup Load Balancing and Auto Scaling (Optional)

1. **Elastic Load Balancing (ELB)**:
   - Create an ELB and register your EC2 instances.
   - Configure health checks and listener settings.

2. **Auto Scaling**:
   - Set up Auto Scaling groups to manage the number of EC2 instances based on load.
   - Configure scaling policies to maintain application availability.

### Step 6: Monitoring and Logging

1. **Amazon CloudWatch**:
   - Set up CloudWatch to monitor your EC2 instances and RDS instance.
   - Configure alarms for critical metrics (CPU usage, memory usage, DB connections).

2. **Centralized Logging**:
   - Use CloudWatch Logs or other logging solutions (e.g., ELK stack) to centralize logs from your microservices.

## Conclusion

Deploying a full-fledged Spring Boot microservices project with Oracle DB on AWS involves setting up various AWS resources and configuring your application to leverage these services. By following this guide, you can ensure a scalable, reliable, and secure deployment of your Spring Boot applications in the cloud.

## Additional Resources

- [AWS Documentation](https://docs.aws.amazon.com/)
- [Spring Boot Documentation](https://spring.io/projects/spring-boot)
- [Oracle Database Documentation](https://docs.oracle.com/en/database/)
- [AWS RDS for Oracle](https://aws.amazon.com/rds/oracle/)
- [AWS EC2](https://aws.amazon.com/ec2/)

---

This guide provides a comprehensive overview of deploying Spring Boot microservices with Oracle DB on AWS, from setting up AWS resources to configuring and running your applications.
