<p align="center">
</p>

# Enabling Secure Hybrid Networking with AWS Transit Gateway

Provides full automation for setting up AWS Site to Site VPN and then extending that same configuration with AWS Transit Gateway and AWS Transit Gateway VPC and VPN attachments.

## How it Works

1. Provisions customer gateway, vpn gateway and a site to site vpn connection
2. Provisions Transit Gateway, Transit Gateway VPC Attachments 
3. Provisions custom lambda for Transit Gateway VPN Attachments and corresponding site to site vpn (not currently supported in CloudFormation)
4. Updates route tables in EC2 Subnets and Transit Gateway Route Table to demonstrate VPC1-VPC3 private connectivity and VPC3-VPN private connectivity via Transit Gateway. Demonstrates VPC1-VPN connectivity via Site to Site VPN 

## Why we do we care about Transit Gateways in Migration Engagements 
1. Implements a Hub and Spoke Topology. Each VPC connection and VPN connection is a spoke that connects into a scalable, cross account Hub
2. Provides a phased migration approach that moves individually connected, full mesh VPN - VPC and VPC-VPC topologies to a hub and spoke topology. For a network with n VPC and n VPN, this would mean O(n) connections instead of O(n*2) connections
3. Extends transitory routing to VPC, VPN and other TGW (for cross region connectivity) via "attachments" for VPC, VPN and other Transit Gateways as well as extends transitory routing to dedicated connections via Direct Connect Gateway 
4. Allows further scaling migration engagements by allowing onpremise networks to connect to multiple VPCs via 1 VIF connection (Transit VIF) into the Direct Connect Gateway--so 1 VIF connection establishes connectivity to multiple, potentially expanding set of VPCs.

## Solution Design

![Solution Design](https://github.com/kmahajan11/awstransformation/blob/master/aws-sharednetworking-transitgateway/images/pic-shared%20networking.png?raw=true)

## How To Install

1. **Template 1 of 2:** vpc-setup-v1.json
* Verify that 2 vpcs (vpc1, vpc3) are setup with corresponding subnets, route tables and security groups per vpc. No input parameters needed. Installs in 2-3 minutes.

2. **Template 2 of 2:**  tgw-vpn-setup-v1.yml
* Accept defaults. Modify onpremise network CIDR and BGP ASN as per your onpremise network.
* Verify what gets provisioned: vgw, cgw and sitetosite vpn; tgw, tgw attachments (vpc1, vpc3 and vpn); tgw route table ( associations, propagations and routes). Installs in 4-5 minutes.
* Route tables for subnet A1 in vpc1 and vpc3 have routes to each other and the onpremise cidr
* **For demo purposes** - 2 demo ec2 instances are provisioned in subnet A1 of each vpc (vpc1, vpc3). The template also sets up the routes in routing tables for these subnets to the transit gateway attachment targets -- to enable each VPC to route to the other VPC or the onpremise network as destinations 


3. **Manual Steps**
* OnPremise ( specfic to your onpremise router)
1. Configure tunnel with onpremise router for tgw-cgw vpn connection
2. Configure tunnel with onpremise router for vgw-cgw vpn connection
* AWS (CloudFormation limitations)
1. Go to tgw route table- add route to the onpremise network via the vpn attachment 
2. Go to site to site vpn for vgw - configure static ip address for the onpremise network



## Author

Kanishk Mahajan; kanishk.mahajan@gmail.com

