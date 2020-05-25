<p align="center">
</p>

# Automated, Real Time and Continuous Remediations for CIS Benchmarks using AWS Config

The CIS Benchmarks for AWS are the only industry standard, objective, consensus-driven security guideline for AWS. They consist of 42 security policies that serve as widely adopted security best practices when configuring AWS deployments and cover all aspects of AWS compute, storage and network configurations. AWS provides built-in automated detection of CIS violations via 2 distinct mechanisms - AWS Config Rules or via AWS Security Hub ( that internally leverages Config). However, there's no built-in support for remediations. 

These templates provide real time, continuous and automated remediations for each of the CIS benchmarks by providing a fully automated  integration with AWS Config Remediation and AWS Systems Manager automation documents.

This is the first of the 2 approaches---these templates are built to leverage AWS Config for both detection and automatic, continuous remediation. Another set of templates in this repository  provide an incident response dashboard mechanism  (i.e. not continuous/self healing) that natively uses AWS Security Hub for both detection and automated remediation. 

Templates 1 and 3 are identical in both approaches. These 2 templates provision AWS Systems Manager Automation Documents. AWS Cloud Watch Log Metric Filters and all the required pre-reqs. Template 2 differs. For this AWS Config based approach, Template 2 leverages the same SSM documents but within AWS Config Remediation Rules while for the AWS Security Hub based approach, Template 2 leverages the same SSM documents but within AWS Security Hub Custom Actions.


## How it Works

1. Leverages the format of AWS Conformance Templates
2. Leverages AWS Config Managed Rules provide automated and continuous detection and recording of CIS Benchmarks - native built-in support from AWS for providing secure compliance baselines
3. Provides NEW AWS Systems Manager Automation Documents for automated remediation for AWS Security Hub CIS Benchmark findings
4. Provides NEW integration of AWS Config Remediations with AWS Systems Manager Automation Documents to provide continuous and real time remediations of AWS Security Hub CIS Benchmark findings

## [Click to watch a Demo of continuous compliance based on these templates](https://awscisautoreme.com/overview.html)


## How To Install

1. **Template 1 of 3:** aws-cis-systemsmanagerautomations.yml
* Provisions AWS Systems Manager automation documents. These documents are used to provide automated remediations within the provisioned AWS Config Rule.
* Provisions with fully built-in pre-reqs. No input parameters required. Simply install on the CloudFormation console (or CLI). Installs in approx 3-4 mins.

2. **Template 2 of 3:** aws-cis-configremediations.yml
* Provisions AWS Config Rules in the format of a Conformance Template with built-in remediation. No input parameters. Simply install on the CloudFormation console (or CLI). Installs in approx 3-4 mins.
* Leverages the output from the previous template specifically the AWS Systems Manager Automation documents

3. **Template 3 of 3:** aws-cis-cloudwatchlogmetricfilters.yml
* Provisions CloudWatch Log Metric Filters and corresponding CloudWatch Alarms for each of the required CIS Benchmarks. Installs independently of templates 1 and 2.  Provide email as input for SNS notification. Installs in approx 2-3 mins. 


## Author

Kanishk Mahajan; kanishk.mahajan@gmail.com

