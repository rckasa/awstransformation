<p align="center">
</p>

# Enabling Shared Hybrid Networking across an AWS Organization with AWS Transit Gateway

Assumes AWS Organizations OUs are configured that reflect the organization structure of an enterprise. For e.g  a Shared Services OU to host shared services such as DNS, Logging, Networing etc and various other OUs (Sales, Finance, Marketing etc) that may represent a business unit and contain accounts for that OU.

Provides full automation for setting up AWS Transit Gateway in a Shared Services OU. Also provisions TGW VPN attachment in the Shared Services OU. Provisions TGW VPC Attachments in the VPC of member accounts of the other OUs of the AWS Organization.  Allows transitory routing between all VPC of member accounts in an AWS Organization as well as transitory connectivity to VPN---all via the Transit Gateway in the Shared Services OU of the AWS Organization 

## AWS Organization Set up (Pre-req)

1. AWS Organization with 4 OUs - Shared Services, Marketing, Sales, Finance
2. Shared Services OU - Contains 1 Account (Shared Services Account)
3. Marketing OU- Contains 3 Accounts. Uses AWS Resource Access Manager (RAM) to create a shared VPC (VPC1) across all 3 accounts. (Account 1 is the owner and RAM is used to share the VPC across Accounts 2 and 3 )
4. Sales OU- Contains 3 Accounts. Uses AWS Resource Access Manager (RAM) to create a shared VPC (VPC2) across all 3 accounts. (Account 1 is the owner and RAM is used to share the VPC across Accounts 2 and 3 )
5. Finance OU -Contains 3 Accounts. Uses AWS Resource Access Manager (RAM) to create a shared VPC (VPC3) across all 3 accounts. (Account 1 is the owner and RAM is used to share the VPC across Accounts 2 and 3 )

## AWS Shared Networking Automation
1. Provisions AWS Transit Gateway and AWS Transit Gateway VPN attachment in the Shared Services Account of the Shared Services OU
2. Provisions AWS Transit Gateway VPC Attachment in the Shared VPC of Account 1 in the Marketing, Sales and Finance OUs
3. Provisions a demo EC2 instance in the Shared VPC of Account 1 in the Marketing, Sales and Finance OUs. Updates Route Table of the Subnet to allow routing to shared vpc cidrs via Transit Gateway VPC Attachment and to the Onpremise cidr via the Transit Gateway VPN attachment.  Use for DEMO ping test.


## Manual Steps
1. Use RAM to share the Transit Gateway with Shared VPC of Marketing, Sales and Finance OUs (can be automated in the future)
2. Use specific onpremise router configuration steps to configure AWS Site to Site VPN Connection based on AWS Transit Gateway VPN attachment
3. Update AWS Transit Gateway route table with route to onpremise cidr (destination) via AWS Transit Gateway VPN attachment (target) (CloudFormation limitation- can be automated via lambda backed resource in CloudFormation in the future)


## Solution Design

![Solution Design](https://github.com/kmahajan11/awstransformation/blob/master/aws-sharednetworking-transitgateway/images/pic-shared%20networking.png?raw=true)

## How To Install

1. **Template 1 of 3: vpc-setup-v1.json**. Install in Account 1 of member OUs - Marketing, Finance or Sales OUs. Use Stack Sets/manual install
* Verify that shared VPC is setup with corresponding subnets, route tables and security groups. No input parameters needed. Installs in 2-3 minutes.
* Use RAM to share the vpc across all accounts (Accounts 2 and 3) in the OU

2. **Template 2 of 3: tgw-shared-master.yml**. Install in Account 1 (Shared Services Account) of Shared Services OU
* Accept defaults. Modify onpremise network CIDR and BGP ASN as per your onpremise network.
* Verify what gets provisioned: cgw and sitetosite vpn; tgw, tgw vpn attachment; tgw route table ( associations, propagations and routes). Installs in 1-2 minutes.
* Note down Transit Gateway ID (output of cloudformation stack or from the TGW console)
* Use RAM to share the TGW across all OUs in the Organization

3. **Template 3 of 3: tgw-attachments-member.yml**. Install in member accounts--for e.g. Account 1 of member OUs - Marketing, Finance or Sales OUs. 
* Provide Transit Gateway ID of Step 2 as input
* Accept defaults. Provide VPC3 CIDR as the destination CIDR value of remote VPC. For e.g. if this is installed in Account 1 of Marketing OU, then VPC3 CIDR can be the VPC CIDR of the Finance OU. 
* **For demo purposes** - 1 demo ec2 instance is provisioned in subnet A1 of the vpc. The template also sets up the routes in routing tables for these subnets to the transit gateway attachment targets -- to enable each VPC to route to the other VPC or the onpremise network as destinations 


## Author

Kanishk Mahajan; kanishk.mahajan@gmail.com

