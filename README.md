# 🚀 ZhIProfile APP: Migrating a Multi-Tier Web Application to AWS Using the Lift-and-Shift Strategy

> **Building a Highly Available, Secure, and Scalable Multi-Tier Web Application on Amazon Web Services (AWS)**

---

# Table of Contents

1. Introduction
2. Project Overview
3. Why Lift and Shift?
4. Business Problem
5. Project Objectives
6. Solution Overview
7. AWS Architecture Overview
8. Technology Stack
9. AWS Services Used
10. High-Level Architecture
11. Request Flow
12. Infrastructure Design Decisions
13. Project Deliverables
14. Skills Demonstrated
15. What's Next

---

# Introduction

Cloud computing has fundamentally changed how organisations build, deploy, and manage applications. Rather than investing heavily in physical infrastructure, businesses can now leverage cloud platforms such as Amazon Web Services (AWS) to build highly available, scalable, and secure applications while paying only for the resources they consume.

One of the fastest ways to adopt cloud computing is through the **Lift-and-Shift (Rehosting)** migration strategy. Instead of redesigning an existing application, organisations migrate it to cloud infrastructure with minimal changes to the application code. This significantly reduces migration time, lowers risk, and enables businesses to begin benefiting from cloud capabilities almost immediately.

This project, **ZhIProfile**, demonstrates a complete Lift-and-Shift migration of a traditional Java-based multi-tier web application from a conventional server environment to AWS. The project showcases how modern AWS services can replace traditional infrastructure components while improving scalability, security, resilience, and operational efficiency.

Rather than focusing only on deploying an application, this project emphasises cloud architecture design, infrastructure planning, security, automation, and operational best practices that reflect real-world production environments.

---

# Project Overview

**Project Name:** ZhIProfile

**Project Type:** AWS Lift-and-Shift Migration

**Cloud Platform:** Amazon Web Services (AWS)

**Architecture:** Multi-Tier Web Application

**Deployment Strategy:** Rehosting (Lift-and-Shift)

**Application Stack:**

* Apache Tomcat
* MySQL Database
* RabbitMQ
* Memcached
* Java
* Maven

**AWS Services**

* Amazon EC2
* Elastic Load Balancer (Application Load Balancer)
* Auto Scaling Group
* Amazon S3
* Amazon EFS
* Amazon Route 53
* Amazon EBS
* AWS Certificate Manager (ACM)
* IAM

---

# What is Lift-and-Shift?

Lift-and-Shift, commonly known as **Rehosting**, is one of the "6 Rs" of cloud migration strategies.

Instead of rebuilding or redesigning an application, Lift-and-Shift simply moves the existing workloads from on-premises infrastructure into the cloud while preserving the application's architecture.

Think of it as relocating a business from one office building to another without changing how the business operates internally.

Instead of this traditional environment:

```
Physical Servers
↓

Nginx Load Balancer
↓

Apache Tomcat

↓

MySQL

↓

Shared File Server
```

We migrate the same architecture into AWS:

```
Application Load Balancer

↓

Amazon EC2

↓

Amazon RDS/EC2 MySQL

↓

Amazon EFS

↓

Amazon S3
```

The application itself remains largely unchanged, but the underlying infrastructure becomes significantly more flexible, resilient, and easier to manage.

---

# Why Choose Lift-and-Shift?

Many organisations choose Lift-and-Shift because it offers several practical advantages:

### Faster Migration

Applications can be moved to the cloud without lengthy redevelopment projects.

### Lower Risk

Since the application code changes very little, there is a reduced risk of introducing new bugs during migration.

### Reduced Capital Expenditure

There is no need to purchase expensive servers, networking hardware, or storage devices. AWS follows a pay-as-you-go pricing model.

### Foundation for Future Modernisation

Once applications are successfully running in the cloud, organisations can gradually adopt cloud-native services such as containers, serverless computing, managed databases, and Infrastructure as Code (IaC).

---

# Business Problem

Imagine a growing company running its business application from an on-premises data centre.

The application currently depends on:

* Physical servers
* Manual deployment
* Local storage
* Static IP addresses
* Limited scalability
* Manual backups
* Traditional load balancing using Nginx

As user traffic increases, several operational challenges begin to emerge:

* Downtime during hardware failures
* Limited storage capacity
* Increasing infrastructure costs
* Manual server provisioning
* Difficulty scaling during peak traffic
* Limited disaster recovery capabilities
* Complex maintenance and patching

These limitations make it difficult for the business to grow efficiently.

The goal of ZhIProfile is to solve these problems by migrating the existing application to AWS without redesigning the application itself.

---

# Project Objectives

The primary objective of ZhIProfile is to modernise existing infrastructure while preserving the current application architecture.

Specific objectives include:

* Host an enterprise web application on AWS.
* Replace physical servers with Amazon EC2 instances.
* Improve availability using Elastic Load Balancing.
* Implement automatic scaling based on traffic demand.
* Store application artifacts securely in Amazon S3.
* Provide shared storage using Amazon EFS.
* Secure communication using HTTPS.
* Manage DNS using Route 53.
* Improve operational security using IAM.
* Provide persistent block storage using Amazon EBS.
* Reduce infrastructure management overhead.
* Prepare the environment for future Infrastructure as Code (Terraform or CloudFormation).

---

# Solution Overview

ZhIProfile adopts a traditional three-tier architecture while replacing on-premises components with AWS-managed services.

The solution consists of three logical layers:

## Presentation Layer

Responsible for receiving requests from users.

Components include:

* Route 53
* Application Load Balancer
* HTTPS (AWS Certificate Manager)

---

## Application Layer

Responsible for processing business logic.

Components include:

* Apache Tomcat
* Auto Scaling Group
* Amazon EC2

---

## Backend Layer

Responsible for data persistence, caching, messaging, and shared storage.

Components include:

* MySQL
* RabbitMQ
* Memcached
* Amazon EFS
* Amazon S3
* Amazon EBS

---

# AWS Architecture Overview
<img width="1237" height="655" alt="Screenshot 2026-07-22 172823" src="https://github.com/user-attachments/assets/5ab41bb7-a867-48ab-9b57-96de0e9579da" />


The migrated infrastructure consists of multiple AWS services working together.

```
                        Users
                           │
                    Internet
                           │
                    GoDaddy DNS
                           │
                      Route 53
                           │
              AWS Certificate Manager
                           │
             Application Load Balancer
                           │
            ┌──────────────┴──────────────┐
            │                             │
      Tomcat EC2                    Tomcat EC2
      (Auto Scaling)                (Auto Scaling)
            │                             │
            └──────────────┬──────────────┘
                           │
                     Amazon EFS
                           │
        ┌──────────────┬──────────────┐
        │              │              │
     MySQL EC2     RabbitMQ EC2   Memcached EC2
                           │
                      Amazon EBS
                           │
                    Amazon S3 Bucket
```

---

# Technology Stack

## Programming Language

* Java

## Build Tool

* Apache Maven

## Web Server

* Apache Tomcat

## Database

* MySQL

## Messaging

* RabbitMQ

## Caching

* Memcached

## Cloud Platform

* Amazon Web Services

## Storage

* Amazon EBS
* Amazon S3
* Amazon EFS

## Networking

* Route 53
* Application Load Balancer

## Security

* IAM
* Security Groups
* AWS Certificate Manager

---

# AWS Services Used

## Amazon EC2

Provides secure virtual servers that host:

* Apache Tomcat
* RabbitMQ
* Memcached
* MySQL

Each service is isolated to improve scalability, maintainability, and fault isolation.

---

## Elastic Load Balancer (Application Load Balancer)

The Application Load Balancer distributes incoming HTTPS requests across healthy Tomcat instances.

Benefits include:

* High availability
* Automatic health checks
* SSL termination
* Intelligent traffic routing

---

## Amazon S3

Stores the application's compiled deployment artifact (WAR file).

Benefits:

* Highly durable
* Secure
* Cost-effective
* Centralised artifact repository

---

## Amazon EFS

Provides a shared file system that can be mounted simultaneously by multiple Tomcat instances.

This is particularly useful when the application scales horizontally.

---

## Amazon EBS

Provides persistent block storage for EC2 instances.

Unlike ephemeral instance storage, EBS volumes retain data even after an instance is stopped.

---

## Route 53

Provides reliable DNS services for internal and public domain resolution.

This allows applications to communicate using meaningful DNS names instead of hard-coded IP addresses.

---

## AWS Certificate Manager (ACM)

Provides free SSL/TLS certificates for securing communication over HTTPS.

Certificates are automatically renewed, reducing operational overhead.

---

## IAM (Identity and Access Management)

IAM ensures secure access to AWS resources by assigning only the permissions required for each user, role, or service.

This project uses IAM roles to securely grant EC2 instances access to Amazon S3 without embedding long-term AWS credentials.

---

# Skills Demonstrated

This project demonstrates practical experience in:

* AWS Cloud Architecture
* Lift-and-Shift Migration Strategy
* Multi-Tier Application Deployment
* Amazon EC2 Administration
* Application Load Balancer Configuration
* Route 53 DNS Management
* SSL/TLS Implementation with ACM
* Shared Storage using Amazon EFS
* Artifact Management with Amazon S3
* Linux Server Administration
* Apache Tomcat Deployment
* MySQL Administration
* RabbitMQ Configuration
* Memcached Configuration
* Auto Scaling
* Infrastructure Planning
* IAM Security Best Practices
* Troubleshooting and Operational Support

---

# What You'll Learn in This Series

In the next section, we move from architecture to implementation.

We'll cover the complete deployment process, including:

* Creating AWS Key Pairs
* Designing Security Groups
* Launching EC2 instances with User Data
* Configuring Route 53 private DNS
* Building the application from source code
* Uploading deployment artifacts to Amazon S3
* Deploying the application on Apache Tomcat
* Configuring HTTPS with AWS Certificate Manager
* Creating an Application Load Balancer
* Mapping a custom GoDaddy domain
* Verifying application health
* Building an Auto Scaling Group for high availability


# End-to-End Deployment and Infrastructure Implementation

In Part 1, we explored the business problem, architecture, AWS services, and overall design of the ZhIProfile project.

In this section, we move from planning into implementation. We'll walk through every stage of deploying the application on AWS, explaining not only **what** was done but also **why** each step is important in a real-world production environment.

---

# Deployment Workflow

The deployment follows a logical sequence that ensures each component is available before the next depends on it.

```
Create Key Pair
        │
        ▼
Create Security Groups
        │
        ▼
Launch EC2 Instances
        │
        ▼
Install Required Software
        │
        ▼
Configure Route 53 Private DNS
        │
        ▼
Build Application from Source Code
        │
        ▼
Upload Artifact to Amazon S3
        │
        ▼
Deploy Artifact to Tomcat
        │
        ▼
Configure HTTPS with ACM
        │
        ▼
Create Application Load Balancer
        │
        ▼
Map GoDaddy Domain
        │
        ▼
Verify Deployment
        │
        ▼
Create Auto Scaling Group
```

---

# Step 1 – Creating the EC2 Key Pair

## Why a Key Pair?

Amazon EC2 instances do not use traditional passwords by default.

Instead, AWS uses **public-key cryptography** to authenticate administrators securely.

When a Key Pair is created:

* AWS stores the public key.
* You download the private key (`.pem` file).
* The private key is used to establish secure SSH connections.

<img width="1547" height="257" alt="image" src="https://github.com/user-attachments/assets/2f6509b1-5caf-4940-a91d-5e2c9b784c6c" />

This approach is significantly more secure than password-based authentication.

### Best Practices

* Store the private key securely.
* Never commit it to GitHub.
* Restrict its permissions.

```bash
chmod 400 zhiprofile-key.pem
```

### Connect to EC2

```bash
ssh -i zhiprofile-key.pem ubuntu@<Public-IP>
```

---

# Step 2 – Creating Security Groups

Security Groups act as **stateful virtual firewalls** for EC2 instances.

Instead of exposing every server to the internet, each server only allows the traffic required for its role.

This is an important security principle known as **Least Privilege**.

---

## Tomcat Security Group

| Port | Protocol | Purpose                 |
| ---- | -------- | ----------------------- |
| 22   | SSH      | Administration          |
| 8080 | TCP      | Tomcat                  |
| 80   | HTTP     | Testing                 |
| 443  | HTTPS    | Secure traffic from ALB |

---

## MySQL Security Group

Rather than allowing the whole internet to connect,

only Tomcat is allowed.

| Port | Purpose        |
| ---- | -------------- |
| 3306 | MySQL Database |

Source: 

```
Tomcat Security Group
```

---

## RabbitMQ Security Group

| Port  | Purpose                     |
| ----- | --------------------------- |
| 5672  | RabbitMQ Messaging          |
| 15672 | RabbitMQ Management Console |


---

## Memcached Security Group

| Port  | Purpose           |
| ----- | ----------------- |
| 11211 | Application Cache |

---

## Application Load Balancer

Public-facing ports:

| Port | Purpose           |
| ---- | ----------------- |
| 80   | Redirect to HTTPS |
| 443  | Secure Website    |

<img width="1364" height="424" alt="image" src="https://github.com/user-attachments/assets/68139ebc-c888-4aa1-a4b5-4d8a5db54ebe" />

<img width="1373" height="558" alt="image" src="https://github.com/user-attachments/assets/52326b24-16d7-45f7-9bb4-bba94c70e3b2" />

<img width="1409" height="423" alt="image" src="https://github.com/user-attachments/assets/4cb25d3e-1115-4cd0-bd44-74850deb7407" />

<img width="1391" height="495" alt="image" src="https://github.com/user-attachments/assets/b8e063c7-1da1-43b0-bdc6-8b35dc1015e5" />

---

# Why Separate Security Groups?

Many beginners place every server inside one Security Group.

This is not recommended.

Separating Security Groups provides:

* Better security
* Easier troubleshooting
* Reduced attack surface
* Improved compliance

---

# Step 3 – Launching EC2 Instances

ZhIProfile uses separate EC2 instances for each major component.

| Server    | Purpose            |
| --------- | ------------------ |
| Tomcat    | Application Server |
| MySQL     | Database           |
| RabbitMQ  | Messaging          |
| Memcached | Caching            |

Each server can be independently maintained and scaled.

<img width="1715" height="213" alt="image" src="https://github.com/user-attachments/assets/1c5bd245-5be2-4bba-a790-f507166b1645" />
<img width="1472" height="631" alt="Screenshot 2026-07-22 192252" src="https://github.com/user-attachments/assets/3bf39a6e-66fe-46ee-a380-3c0ba9644f76" />
<img width="924" height="366" alt="Screenshot 2026-07-22 192231" src="https://github.com/user-attachments/assets/a18937e9-4f4c-4143-811d-501f162c9063" />

---

# Why Separate Servers?

Imagine the database crashes.

If every service runs on one server:

Everything goes offline.

With separate servers:

* Database can be restored independently.
* RabbitMQ continues running.
* Cache remains available.
* Application servers remain operational.

This design follows modern production practices.

---

# Step 4 – Automating Server Configuration with User Data

AWS User Data allows servers to configure themselves automatically during boot.

Instead of manually installing software every time:

```
Launch Instance

↓

Install Java

↓

Install Tomcat

↓

Install Dependencies

↓

Ready
```

This reduces deployment time and ensures consistency.

Example tasks performed by User Data:

* Update packages
* Install Java
* Configure hostname
* Install monitoring tools
* Install AWS CLI
* Mount EFS
* Configure startup services

Automation reduces human error and is the first step toward Infrastructure as Code (IaC).
<img width="1066" height="831" alt="image" src="https://github.com/user-attachments/assets/b5a583c2-b368-4dd1-975d-662f0e96e64e" />
---

# Step 5 – Configuring Route 53 Private DNS

Applications should never rely on hard-coded IP addresses.

Suppose your database IP changes.

Without DNS:

Every configuration file must be updated.

Instead, Route 53 provides friendly names.

Example:

```
db.zhiprofile.internal

rabbit.zhiprofile.internal

cache.zhiprofile.internal
```
<img width="1359" height="551" alt="image" src="https://github.com/user-attachments/assets/7b86a55c-3a3a-4552-83ca-f9f100183ced" />

The application communicates using DNS instead of IP addresses.

Benefits include:

* Easier maintenance
* Greater flexibility
* Simplified disaster recovery
* Better scalability
<img width="1913" height="837" alt="Screenshot 2026-07-23 165334" src="https://github.com/user-attachments/assets/b38cac17-760f-4b56-a963-1e5ef0821876" />
<img width="1839" height="837" alt="Screenshot 2026-07-23 165843" src="https://github.com/user-attachments/assets/10fcfb40-fce6-482a-afbe-8b6ecec35545" />
<img width="1629" height="758" alt="Screenshot 2026-07-23 170046" src="https://github.com/user-attachments/assets/597b0625-dee9-48d0-8983-7d70711a7396" />
<img width="1800" height="725" alt="Screenshot 2026-07-23 170136" src="https://github.com/user-attachments/assets/7f89607e-fd24-4ca6-a84e-e6e5123f2d75" />
<img width="1034" height="654" alt="Screenshot 2026-07-23 170648" src="https://github.com/user-attachments/assets/915ba0b9-4238-4d33-b7d5-c794ad0c1231" />

---

# Step 6 – Preparing the Application Source Code

The application source code is stored in GitHub.

Clone the repository:

```bash
git clone https://github.com/<repository>.git
```

Enter the project:

```bash
cd zhiprofile
```
<img width="846" height="571" alt="Screenshot 2026-07-23 181633" src="https://github.com/user-attachments/assets/a78cf5ef-72af-4e96-a38c-dd170bf1db5b" />
<img width="846" height="571" alt="Screenshot 2026-07-23 181712" src="https://github.com/user-attachments/assets/f154b0c8-0c63-4841-b7c9-6ccef9c20f13" />

---

# Installing Java

Verify Java:

```bash
java -version
```

---

# Installing Maven

Verify Maven:

```bash
mvn -version
```
<img width="965" height="174" alt="Screenshot 2026-07-23 183203" src="https://github.com/user-attachments/assets/fef91a6c-e134-4e31-bb3c-74bb53af2dab" />

Maven manages:

* Dependencies
* Compilation
* Testing
* Packaging

---

# Step 7 – Building the Application

Compile the project:

```bash
mvn clean install
```

This command performs several tasks:

### Clean

Deletes previous build files.

### Compile

Compiles Java source code.

### Test

Executes automated unit tests.

### Package

Creates a deployable WAR file.

Output:

```
target/ROOT.war
```

This WAR file is the deployable application artifact.

---

# Why Build Locally First?

Building before deployment allows developers to identify:

* Compilation errors
* Missing dependencies
* Failed tests
* Configuration issues

before reaching production.

---

# Step 8 – Creating the Amazon S3 Bucket

Instead of copying application files directly between servers,

ZhIProfile uses Amazon S3 as a central artifact repository.

Example bucket:

```
zhiprofile-artifacts
```
<img width="1614" height="843" alt="Screenshot 2026-07-23 171241" src="https://github.com/user-attachments/assets/73258bbf-b5ec-41cc-aa63-84c109168389" />
<img width="1765" height="537" alt="Screenshot 2026-07-23 171459" src="https://github.com/user-attachments/assets/6675b412-6af8-41f2-ae00-544c6fb3367f" />
<img width="1583" height="666" alt="Screenshot 2026-07-23 171626" src="https://github.com/user-attachments/assets/5af7a764-7b00-45cf-949b-0bd4288051f7" />

Benefits:

* Centralised storage
* High durability
* Easy version management
* Integration with CI/CD pipelines

---

# Uploading the WAR File

Using AWS CLI:

```bash
aws s3 cp target/ROOT.war s3://zhiprofile-artifacts/
```

Once uploaded,

every Tomcat server can retrieve the same application version.

---

# Why Use S3 Instead of SCP?

Many traditional environments use:

```
scp ROOT.war server:/var/lib/tomcat/
```

This becomes difficult when managing multiple servers.

Amazon S3 offers:

* One upload
* Many downloads
* Better scalability
* Version history
* Lifecycle management

---

# Step 9 – Deploying the Artifact to Tomcat

On the Tomcat EC2 instance:

Download the application:

```bash
aws s3 cp s3://zhiprofile-artifacts/ROOT.war .
```

Copy the WAR file:

```bash
sudo cp ROOT.war /var/lib/tomcat10/webapps/
```

Restart Tomcat:

```bash
sudo systemctl restart tomcat10
```

Tomcat automatically extracts:

```
ROOT.war

↓

ROOT/

↓

Application Starts
```

---

# Verifying Deployment

Check Tomcat:

```bash
sudo systemctl status tomcat10
```

Verify:

```
http://Server-IP:8080
```

If successful,

the ZhIProfile application homepage loads successfully.

<img width="1907" height="963" alt="Screenshot 2026-07-24 175253" src="https://github.com/user-attachments/assets/b9481a6d-c86d-4417-8ea6-0e9385388c77" />

---

# Common Deployment Issues

During deployment, several issues may arise.

## 404 Not Found

Possible causes:

* Wrong context path
* WAR file not extracted
* Application deployment failure

---

## Port Already in Use

Check:

```bash
sudo ss -tulpn
```

---

## Java Version Mismatch

Verify:

```bash
java -version
```

---

## Permission Errors

Verify ownership:

```bash
sudo chown -R tomcat:tomcat /var/lib/tomcat10/webapps/
```

---

## S3 Access Denied

Common causes:

* Missing IAM Role
* Incorrect Bucket Policy
* Missing S3 permissions

Instead of storing AWS Access Keys on the server, ZhIProfile uses an IAM Role attached to the EC2 instance to grant secure, temporary access to the S3 bucket.
<img width="1729" height="321" alt="Screenshot 2026-07-23 172425" src="https://github.com/user-attachments/assets/c78704d3-3704-4a6a-a8a3-110305520fd4" />
<img width="1780" height="883" alt="Screenshot 2026-07-23 172140" src="https://github.com/user-attachments/assets/de4fa8c5-fa87-46a4-b070-1941e1800bbe" />

---

# Why This Deployment Approach Matters

At first glance, uploading a WAR file to Amazon S3 and then downloading it to Tomcat may seem like an extra step compared to copying it directly to a server.

In reality, this design mirrors how many production environments operate. By storing build artifacts in a central location, every application server retrieves the exact same version, reducing inconsistencies and making rollbacks easier. It also lays the foundation for integrating CI/CD pipelines in the future, where each successful build can automatically publish a new version to S3 and trigger deployments across multiple application servers.

At this stage, the application is successfully running on an EC2-hosted Tomcat server. In the next phase, we'll make the environment production-ready by introducing HTTPS with AWS Certificate Manager, replacing Nginx with an Application Load Balancer, integrating a custom domain through GoDaddy and Route 53, and implementing Auto Scaling to achieve high availability and resilience.


# Production Deployment, High Availability, Security, and Scalability

We have successfully migrated the application to AWS, deployed the application artifact to Apache Tomcat, and verified that the application was accessible using the EC2 public IP address.

While the application is now functional, it is **not yet production-ready**.

<img width="1911" height="983" alt="Screenshot 2026-07-24 190648" src="https://github.com/user-attachments/assets/8e9429c8-a276-466a-9862-42dfebddcc48" />
<img width="960" height="314" alt="Screenshot 2026-07-24 190706" src="https://github.com/user-attachments/assets/b53a6fb9-22ea-4274-a63d-144957e2d333" />
<img width="1913" height="990" alt="Screenshot 2026-07-24 190728" src="https://github.com/user-attachments/assets/9ba144a9-fee3-4cc6-854e-7496082250b4" />
<img width="1902" height="986" alt="Screenshot 2026-07-24 190828" src="https://github.com/user-attachments/assets/b1f89ee0-6030-4d56-a128-a4555e765476" />


A production environment must provide:

* Secure communication (HTTPS)
* High availability
* Automatic scaling
* Fault tolerance
* Centralised traffic management
* Shared application storage
* Monitoring
* Disaster recovery

In this section, we'll transform the application into a production-grade deployment using AWS-managed services.

---

# Why Production Deployment Matters

Imagine your application is running on a single EC2 instance.

Everything works perfectly.

Then one day:

* The EC2 instance crashes.
* AWS schedules maintenance.
* CPU utilisation reaches 100%.
* Thousands of users attempt to access the application simultaneously.

If only one application server exists, your website becomes unavailable.

Modern cloud architecture avoids this single point of failure by distributing workloads across multiple servers.

This is where Elastic Load Balancing and Auto Scaling become essential.

---

# Step 10 – Creating an SSL Certificate with AWS Certificate Manager (ACM)

## Why HTTPS?

Without HTTPS:

```text
Browser
      ↓
Username
Password
Credit Card
      ↓
Internet
```

Information is transmitted in plain text and can potentially be intercepted.

With HTTPS:

```text
Browser
      ↓
Encrypted Data
      ↓
Application Load Balancer
```

All communication between users and your application is encrypted using SSL/TLS.

---

## AWS Certificate Manager
<img width="1664" height="155" alt="Screenshot 2026-07-25 181214" src="https://github.com/user-attachments/assets/8e70c6f3-13eb-4dda-912c-4437584df64d" />

AWS Certificate Manager (ACM) provides free SSL/TLS certificates.

Advantages include:

* Automatic renewal
* Seamless integration with AWS services
* Improved browser trust
* Enhanced security
* Better search engine rankings

Unlike traditional servers where SSL certificates must be manually renewed every year, ACM automates this process, reducing operational effort and the risk of expired certificates.

---

## Certificate Validation

To issue a certificate, ACM verifies ownership of your domain.

This can be done through:

* DNS validation (recommended)
* Email validation

For ZhIProfile, DNS validation is used because it is fully automated and allows ACM to renew the certificate without further intervention.
<img width="1881" height="853" alt="Screenshot 2026-07-25 181225" src="https://github.com/user-attachments/assets/890f6733-75d9-4ced-b78f-b99c0c0f43ab" />

---

# Step 11 – Creating the Application Load Balancer (ALB)

Traditionally, many organisations use Nginx as a reverse proxy and load balancer.

In AWS, this role is handled by the **Application Load Balancer (ALB)**.

Instead of directing users to a single EC2 instance:

```text
Internet

↓

Tomcat Server
```

Traffic now follows:

```text
Internet

↓

Application Load Balancer

↓

Tomcat 1

Tomcat 2

Tomcat 3
```

The ALB intelligently distributes requests across healthy application servers.
<img width="1373" height="700" alt="image" src="https://github.com/user-attachments/assets/794e4ef5-9e2c-4ac7-af6e-3f000c277042" />

---

## Benefits of the Application Load Balancer

### High Availability

If one application server fails, traffic is automatically routed to healthy servers.

---

### SSL Termination

Rather than installing SSL certificates on every Tomcat server, HTTPS is terminated at the ALB.

Benefits include:

* Easier certificate management
* Reduced server configuration
* Improved security

---

### Health Checks

The ALB continuously checks the health of every application server.

If a server becomes unhealthy:

```text
Tomcat 1

❌ Unhealthy

↓

Automatically removed
```

Users never notice the failure because requests continue to healthy instances.

---

### Intelligent Routing

Traffic is distributed evenly across all available servers, preventing any single instance from becoming overloaded.

---

# Step 12 – Creating a Target Group

A Target Group defines which servers receive traffic from the Application Load Balancer.
<img width="1364" height="653" alt="image" src="https://github.com/user-attachments/assets/1778c121-94e8-4f2b-be35-cba5dca7d651" />


For ZhIProfile:

```text
Application Load Balancer

↓

Target Group

↓

Tomcat Instance 1

Tomcat Instance 2
```

Every EC2 instance registered with the Target Group automatically begins receiving requests once it passes the health check.

---

# Health Check Configuration

Health checks determine whether an application instance is healthy enough to receive traffic.

Typical settings include:

Health Check Protocol:

```text
HTTP
```

Health Check Port:

```text
8080
```

Health Check Path:

```text
/
```

Healthy Threshold:

```text
5
```

Unhealthy Threshold:

```text
2
```

Timeout:

```text
5 seconds
```

Interval:

```text
30 seconds
```

If the application repeatedly fails these checks, the ALB stops forwarding traffic to that instance until it recovers.
<img width="1320" height="216" alt="image" src="https://github.com/user-attachments/assets/1d37e8c7-eec5-4c46-a453-9759cee8b8ad" />

---

# Step 13 – Configuring HTTPS Listeners

The Application Load Balancer uses listeners to determine how incoming traffic is handled.
<img width="1679" height="279" alt="image" src="https://github.com/user-attachments/assets/945ba27c-4b71-4f17-9aef-90e22738ad36" />

For ZhIProfile:

HTTP Listener:

```text
Port 80
```

Automatically redirects to:

```text
HTTPS Port 443
```

HTTPS Listener:

```text
443

↓

Application Load Balancer

↓

Target Group

↓

Tomcat Servers
```

This ensures every visitor uses an encrypted connection.

---

# Step 14 – Connecting GoDaddy Domain to AWS

The application currently runs behind an AWS-generated DNS name.

Example:

```text
zhiprofile-alb-123456.eu-west-1.elb.amazonaws.com
```

While functional, this is not user-friendly.

Instead, users should access:

```text
https://www.zhibrad.xyz
```

---

## Updating GoDaddy DNS

Inside GoDaddy:

Create a CNAME record.
<img width="1802" height="567" alt="Screenshot 2026-07-25 181728" src="https://github.com/user-attachments/assets/238f88bb-67a8-4d9b-b08c-f3b0e7fab63a" />

Example:

```text
Host

www
```

Points to:

```text
Application Load Balancer DNS
```

Now visitors can access the application using a memorable domain name instead of an AWS endpoint.

---

# Step 15 – Verifying the Entire Application

Once the domain is configured, several validation tests should be performed.

## Application Test

Verify:

* Homepage loads successfully.
* Login page is accessible.
* User authentication works.
* Navigation is functional.

---

## HTTPS Verification

Ensure:

```text
https://www.zhiprofile.xyz
```

The browser should display the padlock icon, confirming that the SSL certificate is valid.

---

## Database Connectivity

Confirm that the application can:

* Read data
* Write data
* Update records
* Delete records

---

## RabbitMQ Verification

Ensure background messaging services operate correctly.

Examples include:

* Notification queues
* Asynchronous processing
* Event-driven communication

---

## Memcached Verification

Repeated requests should be served faster due to cached data.

Benefits include:

* Reduced database load
* Faster response times
* Improved user experience

---

# Step 16 – Amazon EFS Shared Storage

As additional Tomcat instances are introduced, each server needs access to the same shared files.

Without shared storage:
<img width="1375" height="771" alt="image" src="https://github.com/user-attachments/assets/79059efb-ef8f-4009-8687-33f08dccb3f6" />
<img width="1634" height="833" alt="image" src="https://github.com/user-attachments/assets/186a00d7-ff17-464e-89e7-fb183b8ba585" />

```text
Tomcat 1

Image Uploaded

↓

Tomcat 2

Image Missing
```

Each server has its own local storage, leading to inconsistent user experiences.

Amazon Elastic File System (EFS) solves this by providing a shared file system accessible by all application servers.

```text
Tomcat 1

↓

Amazon EFS

↑

Tomcat 2
```

Now every server reads and writes to the same storage location.

---

## Benefits of Amazon EFS

* Shared storage
* High availability
* Automatic scaling
* No manual storage management
* Multi-instance support

---

# Step 17 – Building the Auto Scaling Group

One of the greatest benefits of cloud computing is elasticity.

Traditional infrastructure often requires purchasing servers months before they're needed.

AWS allows infrastructure to scale automatically based on demand.
<img width="1387" height="789" alt="image" src="https://github.com/user-attachments/assets/b9630b1a-a4a1-45d7-8680-21bf58cc9637" />
<img width="1413" height="591" alt="image" src="https://github.com/user-attachments/assets/59b9d589-931c-400b-b7d4-4a78c3ec7491" />

---

## Auto Scaling Workflow

```text
Traffic Increases

↓

CloudWatch Alarm

↓

Launch New EC2 Instance

↓

Register with Target Group

↓

Receive Traffic
```

When demand decreases:

```text
Traffic Drops

↓

Terminate Extra Instance

↓

Reduce Costs
```

---

## Launch Template

Instead of manually creating every new server, AWS uses a Launch Template containing:

* Amazon Machine Image (AMI)
* Instance Type
* Security Group
* IAM Role
* User Data
* Key Pair

Every new server launched by Auto Scaling is identical to the original deployment.
<img width="1723" height="484" alt="image" src="https://github.com/user-attachments/assets/f0841edb-9541-4209-93a1-16bfa076d2ae" />

---

## Scaling Policies

Example:

Minimum:

```text
1 Instances
```

Desired:

```text
1 Instances
```

Maximum:

```text
4 Instances
```

Scaling Trigger:

```text
CPU > 60%
```

When CPU utilisation exceeds 60%, additional Tomcat servers are automatically launched.
<img width="1442" height="570" alt="image" src="https://github.com/user-attachments/assets/aed117b7-92da-440f-92c0-a5907ce1160c" />

---

# Monitoring with Amazon CloudWatch

Production systems require continuous monitoring.

Amazon CloudWatch collects metrics from every AWS service.

Examples include:

* CPU utilisation
* Network traffic
* Disk activity
* Status checks
* Application logs

CloudWatch Alarms can trigger actions such as:

* Sending email notifications
* Launching additional EC2 instances
* Restarting failed services
* Executing automated recovery procedures

Monitoring helps administrators detect issues before they affect end users.
<img width="1711" height="203" alt="image" src="https://github.com/user-attachments/assets/ac230abb-71b9-40df-a3ab-437da892b792" />

---

# High Availability Strategy

ZhIProfile is designed to eliminate single points of failure.

The production architecture uses:

* Multiple Availability Zones
* Application Load Balancer
* Auto Scaling Group
* Amazon EFS
* Amazon S3
* Amazon EBS Snapshots
* Route 53
* AWS Certificate Manager

Together, these services ensure that the application remains available even if individual servers fail.

---

# End-to-End Request Flow

The following illustrates how a user's request travels through the system:

```text
User
  │
  ▼
GoDaddy DNS
  │
  ▼
Amazon Route 53
  │
  ▼
Application Load Balancer
  │
  ▼
Target Group
  │
  ├───────────────┐
  ▼               ▼
Tomcat EC2    Tomcat EC2
  │               │
  └───────┬───────┘
          ▼
       Amazon EFS
          │
          ▼
 MySQL • RabbitMQ • Memcached
          │
          ▼
       Amazon EBS
```

This layered design ensures secure, scalable, and fault-tolerant communication across every component.

---

# Production Best Practices Implemented

Throughout the ZhIProfile deployment, several AWS best practices were followed:

* IAM roles instead of hard-coded credentials
* Principle of least privilege for security
* HTTPS enforced using AWS Certificate Manager
* Elastic Load Balancer for traffic distribution
* Health checks for automatic failover
* Auto Scaling for elasticity
* Shared storage using Amazon EFS
* Centralised artifact storage in Amazon S3
* Persistent storage using Amazon EBS
* CloudWatch monitoring and alarms
* Separation of application, database, cache, and messaging services into dedicated EC2 instances

These practices improve reliability, security, and maintainability while aligning the environment with production standards.

---

# Conclusion

By the end of this phase, ZhIProfile has evolved from a single-server deployment into a resilient, production-ready cloud application. Traffic is securely encrypted with HTTPS, distributed through an Application Load Balancer, and automatically scaled based on demand. Shared storage ensures consistency across application servers, while CloudWatch provides visibility into the health and performance of the infrastructure.

In **Part 4**, we'll focus on operational excellence by exploring security hardening, disaster recovery, cost optimisation, troubleshooting techniques, lessons learned, recruiter highlights, portfolio value, future enhancements, and key interview talking points that demonstrate the real-world impact of this project.


By the end of this project, you'll understand not only **how** to deploy a multi-tier application on AWS, but also **why** each architectural decision was made and how those decisions contribute to a secure, scalable, and production-ready cloud environment.


# Operational Excellence, Security, Cost Optimisation, Lessons Learned, and Portfolio Showcase

With the application successfully deployed on AWS using a Lift-and-Shift strategy, the next step is ensuring the environment is secure, resilient, cost-efficient, and maintainable. In a production environment, successful deployment is only the beginning. Continuous improvement, monitoring, automation, and operational excellence determine whether an application can reliably support business growth.

This final part highlights the operational practices adopted in the ZhIProfile project and demonstrates the engineering mindset behind the deployment.

---

# Security First: Protecting the Cloud Environment

Security is one of the most important pillars of the AWS Well-Architected Framework. Every design decision in ZhIProfile considered the principle of minimising risk while maintaining usability.

## Identity and Access Management (IAM)

Rather than using a single administrator account for every task, IAM was used to create dedicated users, groups, roles, and policies.

Key implementations included:

* IAM Roles attached to EC2 instances for secure access to Amazon S3.
* Least privilege permissions for users and services.
* Separation of administrative and application permissions.
* Elimination of hard-coded AWS Access Keys from application servers.

This approach improves security and simplifies credential management.

---

## Network Security

Each application component was protected using dedicated Security Groups.

Communication was restricted as follows:

| Component                 | Accessible From            |
| ------------------------- | -------------------------- |
| Application Load Balancer | Internet (Ports 80 & 443)  |
| Tomcat EC2                | ALB and SSH administrators |
| MySQL EC2                 | Tomcat Security Group only |
| RabbitMQ EC2              | Application servers only   |
| Memcached EC2             | Application servers only   |

By preventing unnecessary public access, the attack surface was significantly reduced.

---

## Secure Communication with HTTPS

All external traffic is encrypted using SSL/TLS certificates issued by AWS Certificate Manager (ACM).

Benefits include:

* Protection against man-in-the-middle attacks.
* Encrypted user credentials and sensitive information.
* Improved browser trust.
* Better search engine optimisation (SEO), as HTTPS is a ranking signal.

---

# Monitoring and Observability

Deploying an application without monitoring is like driving a car without a dashboard.

Amazon CloudWatch provides visibility into infrastructure health and application performance.

The following metrics were monitored:

* CPU utilisation
* Memory usage (via CloudWatch Agent)
* Network traffic
* Disk utilisation
* Application status
* EC2 health checks
* Load Balancer request count
* HTTP response codes

CloudWatch Alarms can notify administrators when thresholds are exceeded, enabling faster incident response.

---

# Logging Strategy

In production, logs are invaluable for troubleshooting.

ZhIProfile centralises operational logs, including:

* Apache Tomcat logs
* Application logs
* System logs
* CloudWatch Logs (where configured)

A structured logging approach makes it easier to investigate issues, identify performance bottlenecks, and audit system activity.

---

# Backup and Disaster Recovery

Cloud infrastructure should always assume that failures can occur.

ZhIProfile incorporates multiple recovery mechanisms.

## Amazon EBS Snapshots

Persistent volumes attached to EC2 instances are backed up using EBS snapshots.

Benefits include:

* Point-in-time recovery.
* Fast restoration.
* Long-term backup retention.

---

## Amazon S3

Application artifacts are stored in Amazon S3, which offers eleven nines (99.999999999%) of durability.

This ensures deployment packages remain available even if individual servers fail.

---

## Amazon EFS

Shared application data is stored on Amazon EFS.

Because EFS is a managed, regional service, data remains accessible across multiple Availability Zones.

---

## Auto Scaling Recovery

If an application server becomes unhealthy:

1. The Application Load Balancer marks it as unhealthy.
2. Traffic is no longer routed to the failed instance.
3. The Auto Scaling Group terminates the unhealthy server.
4. A replacement EC2 instance is launched automatically.
5. The new instance joins the Target Group after passing health checks.

This automated recovery process minimises downtime and improves service availability.

---

# Cost Optimisation

One of the primary motivations for migrating to AWS is reducing infrastructure costs while maintaining performance.

## Pay-As-You-Go

Unlike traditional data centres that require large capital investments, AWS charges only for the resources consumed.

Benefits include:

* No upfront hardware purchases.
* Flexible scaling.
* Better budgeting.
* Reduced idle infrastructure.

---

## Auto Scaling

Instead of permanently running multiple application servers, Auto Scaling launches additional instances only when demand increases.

Benefits include:

* Reduced compute costs during low traffic.
* Improved user experience during peak traffic.
* Efficient resource utilisation.

---

## Amazon S3 Storage Classes

As the project evolves, older deployment artifacts can be transitioned to lower-cost storage classes using S3 Lifecycle Policies.

Examples include:

* S3 Standard
* S3 Standard-Infrequent Access
* S3 Glacier Instant Retrieval
* S3 Glacier Flexible Retrieval

---

## Right-Sizing EC2 Instances

Selecting the appropriate EC2 instance type prevents over-provisioning.

Performance should be monitored regularly, and instance sizes adjusted based on actual utilisation.

---

# Challenges Encountered

Real-world projects rarely proceed without obstacles. During the ZhIProfile deployment, several challenges were encountered and resolved.

### Apache Tomcat 404 Errors

**Cause:** The application archive (WAR file) was not deployed correctly, or the context path was incorrect.

**Resolution:** Verified the deployment directory, checked Tomcat logs, and confirmed successful extraction of the WAR file.

---

### Amazon S3 Access Denied

**Cause:** The EC2 instance lacked permission to access the S3 bucket.

**Resolution:** Attached an IAM Role with the appropriate `s3:GetObject` permissions instead of embedding AWS credentials.

---

### Route 53 Name Resolution Issues

**Cause:** Incorrect DNS records or propagation delays.

**Resolution:** Verified hosted zone records, ensured correct record types, and allowed time for DNS propagation.

---

### SSL Certificate Validation

**Cause:** DNS validation records were incomplete.

**Resolution:** Added the required validation CNAME records and confirmed ownership before attaching the certificate to the Application Load Balancer.

---

### Security Group Misconfiguration

**Cause:** Required ports were not open between application components.

**Resolution:** Reviewed inbound and outbound rules, limiting access to trusted Security Groups while maintaining application functionality.

---

# Lessons Learned

Every cloud project offers valuable learning opportunities.

Key takeaways from ZhIProfile include:

* Cloud architecture should prioritise resilience over simplicity.
* Infrastructure planning is just as important as application development.
* Automation reduces human error and deployment time.
* Monitoring is essential for maintaining production workloads.
* Security should be incorporated from the start, not added later.
* Designing for failure improves long-term reliability.
* Managed AWS services reduce operational complexity and allow teams to focus on delivering business value.

---

# Business Impact

Migrating ZhIProfile to AWS provides tangible operational benefits.

### Improved Scalability

The application can automatically adjust to varying traffic levels without manual intervention.

---

### Higher Availability

Multiple application servers and automatic failover reduce downtime.

---

### Enhanced Security

IAM, Security Groups, HTTPS, and encrypted communication improve the overall security posture.

---

### Operational Efficiency

Managed AWS services reduce maintenance tasks and simplify infrastructure management.

---

### Future Readiness

The architecture provides a strong foundation for adopting Infrastructure as Code, CI/CD pipelines, containers, and microservices.

---

# Skills Demonstrated

This project demonstrates practical experience across multiple DevOps and cloud engineering domains.

## Cloud Computing

* Amazon Web Services (AWS)
* Multi-tier architecture
* Lift-and-Shift migration
* Cloud infrastructure design

## Compute

* Amazon EC2
* Auto Scaling Groups
* Launch Templates

## Networking

* Application Load Balancer
* Route 53
* Security Groups
* DNS configuration

## Storage

* Amazon S3
* Amazon EBS
* Amazon EFS

## Security

* IAM
* SSL/TLS
* AWS Certificate Manager
* Principle of Least Privilege

## Application Deployment

* Apache Tomcat
* Java
* Maven
* WAR deployment

## Databases and Middleware

* MySQL
* RabbitMQ
* Memcached

## Linux Administration

* Ubuntu Server
* Shell scripting
* Service management
* Package installation
* Log analysis

## DevOps Practices

* Infrastructure planning
* Automation with User Data
* Monitoring and observability
* Troubleshooting
* High availability
* Disaster recovery

---

# Future Improvements

Although ZhIProfile successfully demonstrates a Lift-and-Shift migration, several enhancements could further modernise the environment.

## Infrastructure as Code

Provision infrastructure using:

* Terraform
* AWS CloudFormation

Benefits include repeatability, version control, and reduced manual effort.

---

## Continuous Integration and Continuous Deployment (CI/CD)

Introduce a deployment pipeline using:

* GitHub Actions
* AWS CodePipeline
* Jenkins

Automated builds, testing, and deployments reduce release time and improve consistency.

---

## Containerisation

Package the application using Docker.

Benefits include portability, consistent environments, and simplified deployments.

---

## Container Orchestration

Run containers on:

* Amazon ECS
* Amazon EKS

This improves scalability and operational flexibility.

---

## Database Modernisation

Migrate from a self-managed MySQL EC2 instance to Amazon RDS for automated backups, patching, and high availability.

---

## Secrets Management

Store sensitive values such as database passwords in AWS Secrets Manager or AWS Systems Manager Parameter Store instead of configuration files.

---

# Recruiter Highlights

This project demonstrates the ability to:

* Design and implement a production-ready AWS architecture.
* Deploy and manage Java applications on Apache Tomcat.
* Configure secure networking and HTTPS.
* Build scalable, highly available cloud infrastructure.
* Implement operational best practices.
* Troubleshoot real-world deployment issues.
* Apply DevOps principles to application hosting and lifecycle management.

These are the types of responsibilities commonly associated with Cloud Engineer, DevOps Engineer, Site Reliability Engineer (SRE), and Infrastructure Engineer roles.

---

# Portfolio Summary

**Project:** ZhIProfile – AWS Lift-and-Shift Migration

**Objective:** Migrate a traditional multi-tier Java web application to AWS while preserving application functionality and improving scalability, security, and operational resilience.

**Key Technologies:** Amazon EC2, Application Load Balancer, Auto Scaling, Amazon S3, Amazon EFS, Amazon EBS, Route 53, IAM, AWS Certificate Manager, Apache Tomcat, MySQL, RabbitMQ, Memcached, Java, Maven, Linux.

**Key Outcomes:**

* Successfully migrated a multi-tier application to AWS.
* Implemented secure HTTPS communication.
* Introduced automated scaling and load balancing.
* Improved fault tolerance and high availability.
* Established a foundation for future DevOps automation and cloud-native enhancements.

---

# Final Thoughts

ZhIProfile represents more than a technical migration exercise—it reflects the practical decision-making required to move enterprise workloads into the cloud. By combining AWS compute, networking, storage, security, and monitoring services, the project demonstrates how existing applications can be modernised incrementally without a complete redesign.

More importantly, it highlights the mindset of a cloud engineer: designing systems that are secure, resilient, scalable, and maintainable while aligning technology decisions with business objectives.

Whether you're a recruiter evaluating cloud engineering skills, a hiring manager looking for production experience, or a fellow engineer exploring AWS migration strategies, ZhIProfile showcases an end-to-end implementation grounded in real-world practices and AWS best practices.
