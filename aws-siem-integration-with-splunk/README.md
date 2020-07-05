<p align="center">
</p>

# Automating AWS SIEM Integration with Splunk. Stream and Visualize AWS CloudWatch logs in Splunk

Provides full automation for near real-time data ingestion into Splunk without the need of installing, orchestrating or managing Splunk forwarders in the customer’s AWS environment. Uses Splunk HEC (HTTP Event Collector) and the out of the box Splunk Lambda BluePrint for CloudWatch Logs. The CFT below can be configured for logs from any AWS Service (for e.g. demonstrates CloudTrail events into CW logs here). Finally, the same approach can be used to leverage other Splunk blueprints (for e.g. for Kinesis Firehose)

## Manual Steps (Splunk) - Configure Splunk HEC
1. Follow steps as outlined here - https://docs.splunk.com/Documentation/Splunk/latest/Data/UsetheHTTPEventCollector#Configure_the_HTTP_Event_Collector_in_Splunk_Web
2. Modify/augment steps above to ensure the following-
* Open port 8088 in the security group for the Splunk AMI (if the default SSL port of 8088 is selected in the HEC configuration). The HEC URL for the lambda would be https://<splunk ami public ip/dns>:8080/events/collector
* In the global settings, select sourcetype as _json
* In the HEC confguration (Settings->Data Input), ensure that sourcetype is set to "aws:cloudwatchlogs"
* To visualize and for dashbaording simply search for sourcetype="aws:cloudwatchlogs"

## Solution Design

![Solution Design](https://github.com/kmahajan11/awstransformation/blob/master/aws-siem-integration-with-splunk/images/arch-diagram.png)

## How To Install

1. **Template 1 of 1: streaming-siem-splunk-v1.yaml**. 
* Pre-req- Create s3 and upload enclosed lambda zip to s3. 
* Enter S3 bucket, s3 key from above; HEC URL, token from Splunk set up and name of cloudwatch logs to be used as a trigger


## Author

Kanishk Mahajan; kanishk.mahajan@gmail.com

