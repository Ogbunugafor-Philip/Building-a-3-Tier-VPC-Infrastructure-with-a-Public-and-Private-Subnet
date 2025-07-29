# Building-a-3-Tier-VPC-Infrastructure-with-a-Public-and-Private-Subnet

![image](https://github.com/user-attachments/assets/4af3f410-a0d5-4cdd-9288-0d3e74ed54f5)



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

Step 1: Create a VPC

Step 2: Enable DNS Host Name

Step 3: Create Internet Gate Way

Step 4: Attach Internet Gateway to VPC

Step 5: Create Public Subnets

Step 6: Enable auto assign Public IPv4 address

Step 7: Create Route Tables

Step 8: Edit Association to allow Public Subnet access to the Internet

Step 9: Create the Private Subnets (Webserver and Database server)


## Project Implementation

### Step 1: Create a VPC

A Virtual Private Cloud (VPC) is a secure, isolated section of a public cloud where users can deploy resources with complete control over networking.

#### Key Points:
- **Region:** us-east-1
- **CIDR Block:** 10.0.0.0/16 (accommodates IP addresses from 10.0.0.0 to 10.0.255.255)
- **Availability Zones:** us-east-1a and us-east-1b for high availability

#### Instructions:
1. Search for **VPC** in the AWS Management Console.
   ![image](https://github.com/user-attachments/assets/91e25df2-970f-4061-8030-759d822a7856)

2. Click **Create VPC**.
3. Fill in the VPC creation form using the specified CIDR block.
   ![image](https://github.com/user-attachments/assets/7af67eed-212d-41ce-82fa-c2def0d9371e)

4. Click **Create VPC**.

---

### Step 2: Enable DNS Host Name

There are two major reasons why we enable DNS Host Name.
Public DNS Names for EC2 Instances: When you turn on DNS hostnames in your VPC, any instance with a public IP gets a friendly name (like ec2-1-2-3-4.compute.amazonaws.com) instead of just an IP address (like 1.2.3.4).
This makes life easier because:
   - You can use the name instead of the IP to connect to your server (like when you use SSH).
   - If you’re hosting a website or app on the server, people can use this name to access it instead of remembering some random numbers.
Internal DNS Names for Private Resources: For servers inside your VPC (without public IPs), they also get friendly names to talk to each other within the network.
This is super handy because:
   - Servers can communicate using these names instead of keeping track of ever-changing IPs.
   - Imagine you have a database and a web server—they can easily find and talk to each other using these names, like calling each other by a nickname instead of a phone number.


#### Instructions:
1. On the VPC dashboard, select the created VPC.
2. Click **Actions** > **Edit VPC settings**.
   ![image](https://github.com/user-attachments/assets/ff2b9467-b3f5-41f8-ba15-cbdf1323c1a1)

3. Check **Enable DNS hostnames**.
   ![image](https://github.com/user-attachments/assets/9ab00c00-f691-4bff-b199-3bea492018df)

4. Save changes.

---

### Step 3: Create an Internet Gateway

An Internet Gateway connects the private network to the internet, enabling online access for resources.

#### Instructions:
1. Navigate to **Internet Gateway** in the AWS Console.
   ![image](https://github.com/user-attachments/assets/13caff90-ee26-4535-b531-5b3fbe26e480)

2. Click **Create Internet Gateway**.
   ![image](https://github.com/user-attachments/assets/7f9851d7-7d74-433c-9ab3-379ad1997a23)

3. Name the gateway and click **Create**.
   ![image](https://github.com/user-attachments/assets/1c8cef1d-be06-4c8c-894c-e7488bdef5fe)

4. Attach the gateway to the VPC:
   - Select the Internet Gateway.
   - Click **Actions** > **Attach to VPC**.
   - Choose the created VPC and attach it.
   ![image](https://github.com/user-attachments/assets/6acecd14-b762-44b9-a73c-0a7d3a87846c)
   ![image](https://github.com/user-attachments/assets/30538228-ac84-462a-937e-4ea9eabed613)


---

### Step 4: Create Public Subnets

A public subnet is a subnet in a VPC that has a route to the internet through an internet gateway, allowing direct communication with external networks.
As highlighted in the beginning, our VPC resources  would be created of two Availability Zones ( Availability Zone 1a and Availability Zone 1b) for high availability.


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
   ![image](https://github.com/user-attachments/assets/ae8bc545-b1d4-4b53-b6db-d650f49544dc)

2. Select the VPC and specify the subnet details.
   ![image](https://github.com/user-attachments/assets/db93f6ee-856f-451c-9409-ae86a4dca7b2)

3. Enable **Auto-assign public IPv4 address** for each public subnet. Enabling auto-assign 
   IPv4 addresses allows instances to automatically receive public IPs for internet access.
   ![image](https://github.com/user-attachments/assets/11d4ecb8-7f7b-4a24-9f4d-50164adce3e1)
   ![image](https://github.com/user-attachments/assets/245ded94-e891-4119-863e-50eb6dccb8b0)


---

### Step 5: Create Route Tables

A route table is like a map that tells data where to go across a network, defining how traffic is directed between subnets, networks, or devices based on destination IP addresses.

#### Instructions:
1. Navigate to **Route Tables** > **Create Route Table**.
   ![image](https://github.com/user-attachments/assets/f9d934b8-beba-47f8-832e-c11eca0aa2d5)

3. Name the route table and associate it with the VPC.
   ![image](https://github.com/user-attachments/assets/55e7afe8-8761-4c6d-90e5-ed94d2aef9c4)

5. Add a route for internet traffic:
   - Destination: 0.0.0.0/0
   - Target: Internet Gateway
6. Associate the route table with the public subnets. By default, our Public subnet cannot access the internet, so any resources created on them cannot access the internet. To all internet access on our public subnet
   •	Go to subnet association then click on edit subnet association
   ![image](https://github.com/user-attachments/assets/2e25104c-b255-4e3c-9961-0a73d3850af2)
   
   •	Select our two created Public Subnet and click on save association
   ![image](https://github.com/user-attachments/assets/b74614f4-5da5-439b-b4e6-2d33a490248c)

---

### Step 6: Create Private Subnets

A private subnet is a segment of a network that is isolated from the internet, allowing resources within it to communicate internally while restricting direct external access for security purposes.
As highlighted in the beginning, our VPC resources  would be created of two Availability Zones ( Availability Zone 1a and Availability Zone 1b) for high availability.

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

Any subnets that have not been explicitly associated with any route tables are associated with the main route table

---

## Conclusion
The outlined steps provide a structured approach to setting up a secure and functional networking environment in AWS. By creating a Virtual Private Cloud (VPC), enabling DNS hostnames, and configuring public and private subnets, this project ensures both accessibility for public-facing resources and isolation for critical backend components. The integration of an Internet Gateway, route tables, and automated IP assignment enhances connectivity and resource management.
This setup establishes a robust foundation for hosting scalable and secure applications, meeting both operational and security requirements.

