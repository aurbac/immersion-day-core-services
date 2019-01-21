# VPC Hands-On Lab

## 1. Create a VPC from scratch

1.1\. Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.

1.2\. In the navigation pane, choose Your VPCs and click on **Create VPC**.

1.3\. For the Name tag type `My VPC` and use the IPv4 CIDR block of `10.1.0.0/16`, click on **Create** and click on **Close**.

1.4\. In the navigation pane, choose Subnets, we are going to create four subnets as follows:

| Name tag | VPC | Availability Zone | IPv4 CIDR block |
| ------:| -----------:| -----------:| -----------:|
| Public Subnet 01  | My VPC | us-east-1a | 10.1.0.0/24 |
| Public Subnet 02  | My VPC | us-east-1b | 10.1.1.0/24 |
| Private Subnet 01  | My VPC | us-east-1a | 10.1.2.0/24 |
| Private Subnet 02  | My VPC | us-east-1b | 10.1.3.0/24 |

1.5\. In the navigation pane, choose Route Tables and click **Create route table**.

1.6\. For the Name tag type `Public Route` and select `My VPC`, click on **Create** and click on **Close**.

1.7\. In the navigation pane, choose Internet Gateways and click **Create Internet gateway**, type Name Tag with `My IG`, click on **Create** and click on **Close**.

1.8\. Select `My IG` and click on **Actions > Attach to VPC**, choose `My VPC` and click **Attach**.

1.9\. In the navigation pane, choose NAT Gateways and click **Create NAT Gateway**.

1.10\. Select the Subnet ID for your Public Subnet 01 that you copied earlier, click on **Create New IP** and click on **Create a NAT Gateway** and click on **Close**.

1.11\. In the navigation pane, choose Route Tables and apply a filter using the VPC ID that you copied earlier, select the **Public Route**, click on **Routes** and click on **Edit Routes**, apply the following routes and click **Save routes**.

| Destination | Target | 
| ------:| -----------:| 
| 10.1.0.0/16 | local | 
| 0.0.0.0/0  | My IG (Internet Gateway) | 

1.12\. In the **Public Route**, click on **Subnet Associations** and click on **Edit subnet associations**, select the subnets **10.1.0.0/24** and **10.1.1.0/24** and click on **Save**.

1.13\. Now select the **Main** route table, this is our route table for private subnets, click on **Routes** and click on **Edit Routes**, apply the following routes and click **Save routes**.

| Destination | Target | 
| ------:| -----------:| 
| 10.1.0.0/16 | local | 
| 0.0.0.0/0  | NAT Gateway (Select the only one) |

## 2. Create a bastion instance

**Bastion Hosts**: Including bastion hosts in your VPC environment enables you to securely connect to your Linux instances without exposing your environment to the Internet. After you set up your bastion hosts, you can access the other instances in your VPC through Secure Shell (SSH) connections on Linux. Bastion hosts are also configured with security groups to provide fine-grained ingress control.

