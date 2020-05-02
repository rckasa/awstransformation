<p align="center">
</p>

# Enabling Secure Hybrid Networking with AWS Transit Gateway

Provides full automation for setting up AWS Site to Site VPN and then extending that same configuration with AWS Transit Gateway and AWS Transit Gateway VPC and VPN attachments.

## How it Works

1. Provisions customer gateway, vpn gateway and a site to site vpn connection
2. Provisions Transit Gateway, Transit Gateway VPC Attachments 
3. Provisions custom lambda for Transit Gateway VPN Attachments and corresponding site to site vpn (not currently supported in CloudFormation)
4. Updates route tables in EC2 Subnets and Transit Gateway Route Table to demonstrate VPC1-VPC3 private connectivity and VPC3-VPN private connectivity via Transit Gateway. Demonstrates VPC1-VPN connectivity via Site to Site VPN 

## How To Install

1. **Template 1 of 2:** vpc-setup-v1.json
* Verify that 2 vpcs (vpc1, vpc3) are setup with corresponding subnets, route tables and security groups per vpc. 
* For the demo, we will use subnet A1 in both VPCs. Check their routing table and verify the current routes that are setup 

2. **Template 2 of 2:**  tgw-vpn-setup-v1.yml
* Accept all defaults 
* Verify/Demo what gets provisioned: vgw, cgw and sitetosite vpn; tgw, tgw attachments (vpc1, vpc3 and vpn); tgw route table (show associations, propagations and routes) 
* Route tables for subnet A1 in vpc1 and vpc3 have routes to each other and the onpremise cidr
* 2 demo ec2 instances are provisioned in each vpc (vpc1, vpc3) that allow ssh and icmp access

3. **Manual Steps**
* OnPremise ( specfic to your onpremise router)
1. Configure tunnel with onpremise router for tgw-cgw vpn connection
2. Configure tunnel with onpremise router for vgw-cgw vpn connection
* AWS (CloudFormation limitations)
1. Go to tgw route table- configure route to onpremise via vpn attachment 
2. Go to site to site vpn for vgw - configure static ip addresses for onpremise subnet



## Author

Kanishk Mahajan; kanishk.mahajan@gmail.com

