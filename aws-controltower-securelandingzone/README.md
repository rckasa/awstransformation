<p align="center">
</p>

# Secure Landing Zone and Self Service with AWS Control Tower

Provides CloudFormation automation for AWS Control Tower Account Factory. Provides automation to create, share and import Service Catalog with member accounts. 

## Demo and Install


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
* Provide the OU of the marketing OU (as e.g.) as input. Accept all defaults
* Leverages custom resource to import portfolio into member OU and create launch constraints for the catalog in each member OU



## Author

Kanishk Mahajan; kanishk.mahajan@gmail.com

