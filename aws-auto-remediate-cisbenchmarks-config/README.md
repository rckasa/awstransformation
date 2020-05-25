<p align="center">
</p>

# Automated, Real Time and Continuous Remediations for AWS Security Hub CIS Benchmarks

The CIS Benchmarks for AWS are the only industry standard, objective, consensus-driven security guideline for AWS. They consist of 42 security policies that serve as widely adopted security best practices when configuring AWS deployments and cover all aspects of AWS compute, storage and network configurations. In response to this demand, AWS introduced the AWS Security Hub in 2019. This service however only offers automated detection of findings of configuration non compliance with the CIS Benchmarks. This solution provides a cloud native implementation for automated and continuous real time remediations for each these CIS security policy violations.

## How it Works

1. Leverages the format of AWS Conformance Templates
2. Leverages AWS Config Managed Rules provide automated and continuous detection and recording of CIS Benchmarks - native built-in support from AWS for providing secure compliance baselines
3. Provides NEW AWS Systems Manager Automation Documents for automated remediation for AWS Security Hub CIS Benchmark findings
4. Provides NEW integration of AWS Config Remediations with AWS Systems Manager Automation Documents to provide continuous and real time remediations of AWS Security Hub CIS Benchmark findings

## How To Install

1. **Template 1 of 3:** autoreme-automationcommands-cis-v1
* Provisions AWS Systems Manager automation documents. These documents are used to provide automated remediations within the provisioned AWS Config Rule
* Requires pre-reqs to be provided as input. Accept all defaults.

2. **Template 2 of 3:** autoreme-securityhub-cis-v1
* Provisions AWS Config Rules in the format of a Conformance Template with built-in remediation. 
* Leverages the output from the previous template specifically the AWS Systems Manager Automation documents

3. **Template 3 of 3:** securityhub-logmetricfilters
* Provisions CloudWatch Log Metric Filters  and corresponding CloudWatch Alarms for each of the required CIS Benchmarks 


## Author

Kanishk Mahajan; kanishk.mahajan@gmail.com

