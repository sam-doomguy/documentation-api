This endpoint allows you to update a specific communication setting.

**IMPORTANT**: User role defines how they may use this endpoint:

1. Only ADMIN users can update organisation-level settings.
2. For an account-level setting, both ADMINs and users with FULL access to the account can update it.

### Filtering

The table below give more information about filter options:

| Name                | Values                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `filter.regions`    | An array of valid region strings. e.g. for AWS ["us-west-1", "us-west-2"], for Azure ["eastus", "westus"] <br /><br /> For more information about regions, please refer to [Cloud Conformity Region Endpoint](https://us-west-2.cloudconformity.com/v1/regions)                                                                                                                                                                                                                                                                                                                                                                                              |
| `filter.services`   | An array of AWS service strings from the following: <br />AutoScaling \| CloudConformity \| CloudFormation \| CloudFront \| CloudTrail \| CloudWatch \|<br />CloudWatchEvents \| CloudWatchLogs \| Config \| DynamoDB \| EBS \| EC2 \| ElastiCache \|<br />Elasticsearch \| ELB \| IAM \| KMS \| RDS \| Redshift \| ResourceGroup \| Route53 \| S3 \| SES \| SNS \| SQS \| VPC \| WAF \| ACM \| Inspector \| TrustedAdvisor \| Shield \| EMR \| Lambda \| Support \| Organizations \| Kinesis \| EFS<br /><br />For more information about services, please refer to [Cloud Conformity Services Endpoint](https://us-west-2.cloudconformity.com/v1/services) |
| `filter.ruleIds`    | An array of valid AWS rule Ids (e.g. ["S3-016", "EC2-001"]). For more information about rules, please refer to [Cloud Conformity Rules API](https://github.com/cloudconformity/documentation-api/blob/master/Rules.md).                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `filter.categories` | An array of category (AWS well-architected framework category) strings from the following:<br /> security \| cost-optimisation \| reliability \| performance-efficiency \| operational-excellence <br />                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `filter.riskLevels` | An array of risk-level strings from the following: <br /> LOW\| MEDIUM \| HIGH \| VERY_HIGH \| EXTREME                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `filter.statuses`   | _(only used for SNS and webhook channels)_ An array of statuses strings from the following: SUCCESS \| FAILURE                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `filter.tags`       | An array of any assigned metadata tags to your resources                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

### Configuration

The table below give more information about configuration options:

| Channel    | Configuration                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _all_      | `configuration.channelName` is the label to display in the application (to distinguish between multiple instances of the same channel type). It is optional                                                                                                                                                                                                                                                                              |
| email      | `configuration.key` is "users", `configuration.value` is an array of verified users that have at least readOnly access to the account                                                                                                                                                                                                                                                                                                    |
| sms        | `configuration.key` is "users", `configuration.value` is an array of users with verified mobile numbers that have at least readOnly access to the account                                                                                                                                                                                                                                                                                |
| slack      | `{ "url": "https://hooks.slack.com/services/your-slack-webhook",` <br>`"channel": "#your-channel",` <br>`"displayIntroducedBy": false,` Boolean, true for adding user to message<br>`"displayResource": false,` Boolean, true for adding resource to message<br>`"displayTags": false}` Boolean, true for adding associated tags to message                                                                                              |
| pager-duty | `{ "serviceName": "yourServiceName", "serviceKey": "yourServiceKey" }`                                                                                                                                                                                                                                                                                                                                                                   |
| sns        | `{ "arn": "arn:aws:sns:REGION:ACCOUNT_ID:TOPIC_NAME"}`                                                                                                                                                                                                                                                                                                                                                                                   |
| ms-teams   | `{ "url": "https://outlook.office.com/webhook/your-msteams-webhook",` <br>`"channel": "#your-channel",` <br>`"displayIntroducedBy": false,` Boolean, true for adding user to message<br>`"displayResource": false,` Boolean, true for adding resource to message<br>`"displayTags": false` Boolean, true for adding associated tags to message<br>`"displayExtraData": false}` Boolean, true for adding associated extra data to message |
| webhook    | `{ "url": "https://your-webhook-url.com", "securityToken": "yourSecurityToken" }`                                                                                                                                                                                                                                                                                                                                                        |

Example request to update an account level pager-duty setting:

```
curl -X PATCH \
-H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
-d '
{
    "data": {
        "type": "settings",
        "attributes": {
            "type": "communication",
            "enabled": true,
            "configuration": {
                "serviceName": "SomeOtherName",
                "serviceKey": "anotherpagerdutyservicekey"
            },
            "channel": "pager-duty"
        }
    }
}' \
https://us-west-2-api.cloudconformity.com/v1/settings/communication/H19NxM15-:communication:pager-duty-S1xvk1zGwM
```

Example Response:

```
  [
    {
        "data": {
            "type": "settings",
            "id": "H19NxM15-:communication:pager-duty-S1xvk1zGwM",
            "attributes": {
                "type": "communication",
                "manual": "",
                "enabled": true,
                "configuration": {
                    "serviceName": "SomeOtherName",
                    "serviceKey": "anotherpagerdutyservicekey"
                },
                "channel": "pager-duty"
            },
            "relationships": {
                "organisation": {
                    "data": {
                        "type": "organisations",
                        "id": "ryqMcJn4b"
                    }
                },
                "account": {
                    "data": {
                        "type": "accounts",
                        "id": "H19NxM15-"
                    }
                }
            }
        }
    }
]
```
