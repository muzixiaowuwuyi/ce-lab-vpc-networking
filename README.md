# Lab M3.01 - VPC Networking Foundations

This project covers the fundamental setup of an AWS Virtual Private Cloud (VPC). It establishes a secure, highly available network foundation using a multi-tier architecture across two Availability Zones (Multi-AZ).

## 📁 Project Structure

*   **architecture-diagram.png**: Logic diagram showing VPC, Subnets, and IGW.
*   **network-config/**: Contains configuration details for the VPC, Subnets, and Route Tables.
*   **screenshots/**: AWS Console verification of the network resources and Resource Map.

---

## 🧠 Reflection & Key Concepts

### 1. Why use 10.0.0.0/16 instead of 10.0.0.0/24?
A `/16` CIDR block provides **65,536** IP addresses, while a `/24` only provides **256**. Using `/16` follows the principle of planning for **future growth**, allowing us to create dozens of subnets for different tiers (web, app, db) as the infrastructure scales.

### 2. What's the difference between public and private subnets?
The primary difference is the **Route Table**. 
*   **Public Subnets** are associated with a route table that has a route to the **Internet Gateway (IGW)** (0.0.0.0/0 -> igw). 
*   **Private Subnets** do not have a direct route to the IGW, making them isolated from direct internet access.

### 3. Why deploy across multiple Availability Zones?
To ensure **High Availability (HA)** and Fault Tolerance. If one AWS data center (Availability Zone) experiences an outage, the resources in the second AZ will remain operational, preventing a total service failure.

### 4. How many usable IP addresses are in 10.0.1.0/24?
There are **251 usable IP addresses**. 
Although a `/24` has 256 total addresses, **AWS reserves 5 IPs** in every subnet for specific networking purposes (Network address, VPC router, DNS, future use, and Broadcast address).

### 5. Could you add more subnets later without changing the VPC?
**Yes.** Since the VPC uses a large `/16` block and we have only utilized a few `/24` segments so far, there is a significant amount of **reserved IP space**. We can add many more subnets in the future as long as their CIDR blocks do not overlap with existing ones.

---

## ✅ Final Verification
*   **Network Isolation**: Verified that private subnets are logically separated from the public tier.
*   **Redundancy**: Confirmed subnets are distributed across two different AZs (e.g., eu-central-1a and eu-central-1b).