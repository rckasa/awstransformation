<p align="center">
</p>

# Secure Landing Zone and Self Service with AWS Control Tower

Provides CloudFormation automation for AWS Control Tower Account Factory. Provides automation to create, share and import Service Catalog with member accounts. 


## Install

1. **Pre-req:** Console
* Set up organization structure in AWS Control Tower - for e.g. 2 container OUs under Root - sales and marketing ous

2. **Template 1 of 3:**  awscontroltower-customize-accountfactory.yml
* Provide cloudformation automation for Quick Account Provisioning. Enter account email, account name, SSO User first and last name, OU for account
* Leverages AWS CloudFormationProvisionedProduct to vend account 
* Leverages custom resource to obtain provisioning artifiact based on product and portfolio identifiers

3. **Template 2 of 3:**  awscontroltower-servicecatalog-masteraccount -v1.yml
* Provide the OU of the marketing OU (as e.g.) as input. Accept all defaults
* Provisions a Service Catalog with Portfolio and Product and shares the catalog with marketing OU
* Leverages custom resource to share portfolio with member OU
* Leverages AWS Service Catalog CloudFormation for Portfolio Product Associations

3. **Template 3 of 3:**  awscontroltower-import-servicecatalog-memberaccount.yml
* Provide the OU of the marketing OU (as e.g.) as input. Accept all defaults. **Use Stack Sets** to run this template and provide member OU or member accounts and regions as input.
* Leverages custom resource to import portfolio into member OU and create launch constraints for the catalog in each member OU

## Leverage AWS Control Tower Landing Zone in conjunction with these templates


1. **Create/Update Organization Structure:** - Use Control Tower to create an organizational hierarchy in AWS that mirrors the structure/set up of the enterprise. The organization is set up as a hierarchy of organization units (OUs). Each organization unit can contain multiple AWS accounts
2. **Create/Update Guardrails:** Use Control Tower to apply guardrails to the organizational structure. Multiple guardrails are attached to the Organizational Unit (OU). Each AWS account automatically inherits the guardrails defined for its OU.
3. **Create/Update AWS Accounts:**  Use the Account Provisioning Template (template 1) provided here to provision AWS accounts within each organizational unit in the organization.  The template leverages Service Catalog Provisioned Product. (AWS Control Tower provides an Account Factory as a product in a built-in service catalog portfolio)
4. **Create/Update and Distribute Service Catalog:** Use the Service Catalog templates (templates 2 and 3) here to create a catalog in a master account and then share and import local copies in member accounts.  The templates also create launch constraints for end user access in the next step. 
5. **End User Select/Launches Product:**  Non AWS access. End user Selects an AWS Service or offering for consumption from service catalog interface


## Solution Design

![Solution Design](https://github.com/kmahajan11/awstransformation/blob/master/aws-controltower-securelandingzone/images/arch-diagram1.png)

## Author

Kanishk Mahajan; kanishk.mahajan@gmail.com

