<p align="center">
</p>

# Automated, Real Time Remediations for PCI-DSS Findings using AWS Security Hub

AWS provides built-in automated detection of PCI violations via 2 distinct mechanisms - AWS Config Rules or via AWS Security Hub ( that internally leverages Config). However, there's no built-in support for remediations. 

These templates provide real time and automated remediations for each of the PCI-DSS benchmarks by providing a fully automated integration of AWS Security Hub Custom Actions and AWS Systems Manager automation documents.

This is the second of the 2 approaches---the previous templates were built to leverage AWS Config for both detection and automatic, continuous remediation. These set of templates provide an incident response dashboard mechanism  (i.e. not continuous/self healing) that natively uses AWS Security Hub for both detection and automated remediation. 

Templates 1 and 3 are identical in both approaches. These templates provision AWS Systems Manager Automation Documents, AWS Cloud Watch Log Metric Filters and all the required pre-reqs. Template 2 differs. For the AWS Config based approach, Template 2 leverages the same SSM documents but within AWS Config Remediation Rules while for this AWS Security Hub based approach, Template 2 leverages the same SSM documents but within AWS Security Hub Custom Actions.

## How it Works

1. Leverages AWS Security Hub directly to provide automated detection of PCI findings
2. Provides NEW AWS Systems Manager Automation Documents for automated remediation for AWS Security Hub PCI findings. All documents are automatically provisioned via a AWS CloudFormation template.
3. Provides NEW integration of AWS Security Hub Custom Actions with AWS Systems Manager Automation Documents to provide real time remediations of AWS Security Hub PCI findings. Provisions Event based (CloudWatch Events) processing of AWS Security Hub Findings based on the AWS Security Hub Finding Format (ASFF) and packages the finding as input parameters for the associated AWS Systems Manager Automation Document.

## Solution Design


![Solution Design](https://github.com/kmahajan11/awstransformation/blob/master/aws-auto-remediate-cisbenchmarks-securityhub/images/arch-diagram.png)

## How To Install

1. **Template 1 of 3:** aws-pci-systemsmanagerautomations.yml
* Provisions AWS Systems Manager automation documents. These documents are used to provide automated remediations within the provisioned AWS Security Hub Action.
* Provisions with fully built-in pre-reqs. No input parameters required. Simply install on the CloudFormation console (or CLI). Installs in approx 3-4 mins.

2. **Template 2 of 3:** aws-pci-securityhubactions.yml
* Provisions AWS CloudWatch Evemts and AWS Security Hub Custom Actions. No input parameters. Simply install on the CloudFormation console (or CLI). Installs in approx 3-4 mins.
* Leverages the output from the previous template specifically the AWS Systems Manager Automation documents

3. **Template 3 of 3:** aws-pci-cloudwatchlogmetricfilters.yml
* Provisions CloudWatch Log Metric Filters and corresponding CloudWatch Alarms for each of the required CIS Benchmarks. Installs independently of templates 1 and 2.  Provide email as input for SNS notification. Installs in approx 2-3 mins. 


## Author

Kanishk Mahajan; kanishk.mahajan@gmail.com

