# Building-a-3-Tier-VPC-Infrastructure-with-a-Public-and-Private-Subnet

# AWS Virtual Private Cloud (VPC) Setup

## Introduction
In today’s cloud-driven landscape, businesses demand highly secure, reliable, and scalable network environments to host their applications and manage sensitive data. This project focuses on leveraging Amazon Web Services (AWS) to design and implement a Virtual Private Cloud (VPC), providing an isolated and customizable network environment tailored to modern business needs.
The AWS VPC is a foundational service that allows organizations to deploy resources such as servers, databases, and applications in a secure, private network. By carefully designing and configuring the VPC, this project demonstrates how enterprises can achieve optimal performance, enhanced security, and seamless integration with on-premises systems and other cloud resources.

---

## Objectives

- Establish a secure and scalable networking environment.
- Enable internet connectivity for public resources.
- Segregate network traffic for enhanced security.
- Optimize resource configuration for accessibility and functionality.

---

## Project Steps

### Step 1: Create a VPC

A Virtual Private Cloud (VPC) is a secure, isolated section of a public cloud where users can deploy resources with complete control over networking.

#### Key Points:
- **Region:** us-east-1
- **CIDR Block:** 10.0.0.0/16 (accommodates IP addresses from 10.0.0.0 to 10.0.255.255)
- **Availability Zones:** us-east-1a and us-east-1b for high availability

#### Instructions:
1. Search for **VPC** in the AWS Management Console.
2. Click **Create VPC**.
3. Fill in the VPC creation form using the specified CIDR block.
4. Click **Create VPC**.

---

### Step 2: Enable DNS Host Name

Enabling DNS hostnames simplifies resource communication by providing user-friendly names for public and internal resources.

#### Instructions:
1. On the VPC dashboard, select the created VPC.
2. Click **Actions** > **Edit VPC settings**.
3. Check **Enable DNS hostnames**.
4. Save changes.

---

### Step 3: Create an Internet Gateway

An Internet Gateway connects the private network to the internet, enabling online access for resources.

#### Instructions:
1. Navigate to **Internet Gateway** in the AWS Console.
2. Click **Create Internet Gateway**.
3. Name the gateway and click **Create**.
4. Attach the gateway to the VPC:
   - Select the Internet Gateway.
   - Click **Actions** > **Attach to VPC**.
   - Choose the created VPC and attach it.

---

### Step 4: Create Public Subnets

Public subnets allow resources to connect to the internet through the Internet Gateway.

#### Configuration:
- **Public Subnet AZ 1:**
  - Name: Public_Subnet_AZ_1
  - Availability Zone: us-east-1a
  - CIDR Block: 10.0.0.0/24
- **Public Subnet AZ 2:**
  - Name: Public_Subnet_AZ_2
  - Availability Zone: us-east-1b
  - CIDR Block: 10.0.1.0/24

#### Instructions:
1. Go to **Subnets** > **Create Subnet**.
2. Select the VPC and specify the subnet details.
3. Enable **Auto-assign public IPv4 address** for each public subnet.

---

### Step 5: Create Route Tables

Route tables define how traffic flows between resources in the VPC and external networks.

#### Instructions:
1. Navigate to **Route Tables** > **Create Route Table**.
2. Name the route table and associate it with the VPC.
3. Add a route for internet traffic:
   - Destination: 0.0.0.0/0
   - Target: Internet Gateway
4. Associate the route table with the public subnets.

---

### Step 6: Create Private Subnets

Private subnets are isolated from the internet, ensuring secure communication for internal resources like databases.

#### Configuration:
- **Private Subnet AZ 1 (Webserver):**
  - Name: Webserver_Subnet_AZ_1
  - Availability Zone: us-east-1a
  - CIDR Block: 10.0.2.0/24
- **Private Subnet AZ 1 (Database):**
  - Name: Database_Subnet_AZ_1
  - Availability Zone: us-east-1a
  - CIDR Block: 10.0.4.0/24
- **Private Subnet AZ 2 (Webserver):**
  - Name: Webserver_Subnet_AZ_2
  - Availability Zone: us-east-1b
  - CIDR Block: 10.0.3.0/24
- **Private Subnet AZ 2 (Database):**
  - Name: Database_Subnet_AZ_2
  - Availability Zone: us-east-1b
  - CIDR Block: 10.0.5.0/24

#### Instructions:
1. Create each subnet under **Subnets** > **Create Subnet**.
2. Specify the VPC, availability zone, and CIDR block.
3. Associate subnets with the appropriate route table.

---

## Conclusion
The outlined steps provide a structured approach to setting up a secure and functional networking environment in AWS. By creating a Virtual Private Cloud (VPC), enabling DNS hostnames, and configuring public and private subnets, this project ensures both accessibility for public-facing resources and isolation for critical backend components. The integration of an Internet Gateway, route tables, and automated IP assignment enhances connectivity and resource management.
This setup establishes a robust foundation for hosting scalable and secure applications, meeting both operational and security requirements.

