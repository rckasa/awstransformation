<p align="center">
</p>

## Automated Remediations for AWS GuardDuty 

 Provides automated Remediations for GuardDuty for EC2 and IAM. Provides samples for EC2 Recon Attack and IAM Password Policy change. Can be extended for any GuardDuty EC2 or IAM related threat findings. Automates Finding generation

## How it Works

1. Triggers CW Event rules for GuardDuty Events
2. Provides Remediation lambdas for EC2 event and IAM events
3. Provides dummy EC2 instances ( malicious and compromised) with self contained user data sections to generate events


## How To Install

1. **Template 1 of 2:** vpc-setup-v1.json
* Provisions a multiple VPC environment to provide an AWS environment with built-in security groups and networking


2. **Template 2 of 2:** aws-guardduty-remediations-ec2-v2
* Provisions AWS GuardDuty events and remediation for EC2 and IAM for sample events (ec2 recon event and iam password policy change)


## Author

Kanishk Mahajan; kanishk.mahajan@gmail.com

