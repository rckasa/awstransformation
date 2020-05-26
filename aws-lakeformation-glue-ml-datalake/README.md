<p align="center">
</p>

# Secure Data Transformation with AWS LakeFormation and AWS Glue

Demonstrates a fully automated approach to secure data by applying data transformations as data migrates from onpremise repositories into AWS :

## How it Works

 1. Simulates onpremise data as a large csv uploaded to S3
 2. Leverages AWS LakeFormation as the centralized data repository
 3. Applies LakeFormation Machine Learning Transform to the data. 
 4. The transform performs de-duplication of data using an AWS provided ML based fuzzy logic algorithm.However, this should be considered as a placeholder and can be substituted for any business function (specifically anonymization or data masking)
 5. Uses AWS S3 as the AWS repository to store the final transformed data
 6. Uses AWS Glue to create a data catalog (specifically a Database, Tables and corresponding schema) for the source data as well as the transformed data
 7. Uses AWS Glue ETL to perform an automated transformation of source data to the transformed de-duplicated data based on the LakeFormation ML Transform
 8. Uses AWS Glue Crawler that automatically discovers when the transformed data is populated in S3, creates a catalog (database schema and table) in AWS Glue and allows SQL querying with Athena
 9. Uses AWS Athena for querying both source and transformed data
 10. All aspects of this solution (Steps 1-8 above) are fully automated via AWS CloudFormation


## How To Install

1. **Template 1 of 2:** aws-glue-lakeformation-ml-v2.yml
* Provisions a Glue Data Catalog (Database, Table) from source S3 dataset: (s3-source-duplicaterecords-<AWS:Region>)
* Provisions a LakeFormation ML Transform for fuzzy logic deduplication of data
* Provisions an Empty new Transformed S3 Bucket: (s3-transform-deduplicated-v1-<AWS:AccountID>-<AWS:Region>)
* Provisions a Scheduled Glue Crawler that is scheduled to run on a cron schedule and pick up the data from the new transformed bucket (1c)
* Allows the Glue crawler to periodically check if the new transformed bucket (1c) has been populated
* When the Glue Crawler finds the data in the transformed bucket above (i.e. 1c) on scheduled crawling, it creates a Glue Data Catalog (Database, Table) from the data in the new transformed bucket


2. **Template 2 of 2:** aws-glue-etl-v1.yml
* Creates a Glue ETL job
    - The Glue ETL job incorporates the trained ML Transform from STEP 2
    - The Glue ETL job transforms source data into deduplicated transformed data and populates the transformed bucket
* The Glue Crawler from STEP 1 will eventually discover the populated data in this transformed bucket during
  its scheduled crawling and create the new Glue Catalog (Database, Tables) from this transformed deduplicated data 


## Solution Design

![Solution Design](https://github.com/kmahajan11/awstransformation/blob/master/aws-lakeformation-glue-ml-datalake/images/arch-diagram1.png)

## Author

Kanishk Mahajan; kanishk.mahajan@gmail.com




