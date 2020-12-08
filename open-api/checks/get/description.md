This endpoint allows you to collect checks for specified accounts.

The `filter` query parameter is the basis for filtering.

For example, the following is a request for a page of checks filtered by service `EC2`:

```
GET /checks?accountIds=r1gyR4cqg&page[size]=100&page[number]=0&filter[services]=EC2
```

Multiple filter values can be combined in a comma-separated list. For example the following is a request for a page of checks in `us-west-2` or `us-west-1` regions:

```
GET /checks?accountIds=r1gyR4cqg&page[size]=100&page[number]=0&filter[regions]=us-west-1,us-west-2
```

Furthermore, multiple filters can be applied to a single request. For example, the following is a request to get checks for `us-west-2` region when the status of the check is `SUCCESS`, and it's for `EC2` or `IAM` service in `security` category with `HIGH` risk level

```
GET /checks?accountIds=r1gyR4cqg&page[size]=100&page[number]=0&filter[regions]=us-west-2&filter[statuses]=SUCCESS&filter[categories]=security&filter[riskLevels]=HIGH&filter[services]=EC2,IAM
```

The table below give more information about filter options:

| Name                         | Values                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| filter[regions]              | AWS Regions: global \| us-east-2 \| us-east-1 \| us-west-1 \| us-west-2 \| ap-south-1 \| ap-northeast-2 \|<br />ap-southeast-1 \| ap-southeast-2 \| ap-northeast-1 \| ca-central-1 \| eu-central-1 \| eu-west-1 \|<br /> eu-west-2 \| sa-east-1 <br /><br />Azure Regions: eastasia \| southeastasia \| centralus \| eastus \| eastus2 \| westus \| northcentralus \|<br />southcentralus \| northeurope \| westeurope \| japanwest \| japaneast \| brazilsouth \| australiaeast \| australiasoutheast \|<br />southindia \| centralindia \| westindia \| canadacentral \| canadaeast \| uksouth \| ukwest \| westcentralus \| westus2 \| koreacentral \| koreasouth \| <br />francecentral \| francesouth \| australiacentral \| australiacentral2 \| southafricanorth \| southafricawest \| <br /><br />For more information about regions, please refer to [Cloud Conformity Region Endpoint](https://us-west-2.cloudconformity.com/v1/regions) |
| filter[services]             | AWS Services: AutoScaling \| CloudConformity \|CloudFormation \| CloudFront \| CloudTrail \| CloudWatch \|<br />CloudWatchEvents \| CloudWatchLogs \| Config \| DynamoDB \| EBS \| EC2 \| ElastiCache \| Elasticsearch \| ELB \| IAM \| KMS \| RDS \| Redshift \| ResourceGroup \| Route53 \| S3 \| SES \|<br />SNS \| SQS \| VPC \| WAF \| ACM \| Inspector \| TrustedAdvisor \| Shield \| EMR \| Lambda \|<br />Support \| Organizations \| Kinesis \| EFS<br /><br />Azure Services: StorageAccounts \| SecurityCenter \| ActiveDirectory \| MySQL \| PostgreSQL \|<br />Sql \| Monitor \| AppService \| Network \| ActivityLog \| VirtualMachines \| AKS \| KeyVault \| Locks \| AccessControl<br /><br />For more information about services, please refer to [Cloud Conformity Services Endpoint](https://us-west-2.cloudconformity.com/v1/services)                                                                                         |
| filter[categories]           | security \| cost-optimisation \| reliability \| performance-efficiency \| operational-excellence <br /><br />For more information about categories, please refer to [Cloud Conformity Services Endpoint](https://us-west-2.cloudconformity.com/v1/services)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| filter[riskLevels]           | LOW\| MEDIUM \| HIGH \| VERY_HIGH \| EXTREME <br /><br />For more information about risk levels, please refer to [Cloud Conformity Services Endpoint](https://us-west-2.cloudconformity.com/v1/services)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| filter[statuses]             | SUCCESS \| FAILURE                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| filter[ruleIds]              | AWS Rules: EC2-001 \| EC2-002 \| etc <br /><br />Azure Rules: KeyVault-001 \| StorageAccounts-001 \| etc <br /><br />For more information about rules, please refer to [Cloud Conformity Services Endpoint](https://us-west-2.cloudconformity.com/v1/services)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| filter[resource]             | Filter by resource Id <br /><br />For an exact match, e.g "johnSmith", a wildcard, e.g "joh?Sm*h" or when used with filter[resourceSearchMode]=regex, a regular expression, e.g "joh.?Sm.*h". Regular expressions should be URL encoded before sending.<br /><br />For more information about filters, please refer to [Filter and Search](https://www.cloudconformity.com/help/rules/filter-and-search.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| filter[resourceSearchMode]   | Set the search mode for the resource filter. <br /><br /> Valid values are "text" or "regex". Text supports an exact match or the wildcard characters \* and ?<br /> Defaults to "text"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| filter[message]              | Filter by message. <br /><br /> Will find messages that contain all words regardless of the order. e.g "new message" will find "message new" and "new message"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| filter[suppressedFilterMode] | "v1" \| "v2" <br /><br /> Whether to use the `"v1"` or `"v2"` suppressed functionality. `"v1"`: Using `suppressed=true` will return both suppressed and unsuppressed checks, `suppressed=false` will just return unsuppressed checks. `"v2"`: Using `suppressed=true` return will just return suppressed checks. Defaults to "v1".                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| filter[suppressed]           | true \| false <br /><br /> Whether or not include all suppressed checks. The default value is `true` for "v1" and omitted for "v2"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| filter[createdDate]          | The date when the check was created<br /><br />The numeric value of the specified date as the number of milliseconds since January 1, 1970, 00:00:00 UTC                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| filter[createdLessThanDays]  | Deprecated. Use `filter[newerThanDays]` instead.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| filter[createdMoreThanDays]  | Deprecated. Use `filter[olderThanDays]` instead.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| filter[newerThanDays]        | The filter[olderThanDays] and filter[newerThanDays] range refers to days to go back from today. It converts the number of days entered to the date when the check was created and assigned a status, or where the status changed from "Success" to "Failure" or from "Failure" to "Success". You can use this filter by entering values for the number of days you wish to view before `filter[olderThanDays]` and after `filter[newerThanDays]`. You must pass at least 2 days up to 1 day to see any checks for a specific time duration. To display checks from a particular day up to today, pass the number of days in filter[newerThanDays] and leave filter[olderThanDays] blank. Number. e.g. 5.                                                                                                                                                                                                                                           |
| filter[olderThanDays]        | To display all checks for up to a particular day, pass a number of days to go back from today in filter[olderThanDays] and leave filter[newerThanDays] blank. Number. e.g. 5.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| filter[tags]                 | Any assigned metadata tags to your resources                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| filter[compliances]          | An array of supported standard or framework ids. Possible values: ["AWAF" \| "CISAWSF" \| "CISAZUREF" \| "CISAWSTTW" \| "PCI" \| "HIPAA" \| "GDPR" \| "APRA" \| "NIST4" \| "SOC2" \| "NIST-CSF" \| "ISO27001" \| "AGISM" \| "ASAE-3150" \| "MAS"]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| filter[withChecks]           | true \| false <br /><br /> Displays only controls from PDF reports with one or more associated checks. If `withoutChecks` is also set to true, then filter has no effect and all checks will be displayed. The default value is `false`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| filter[withoutChecks]        | true \| false <br /><br /> Displays only controls from PDF reports with 0 associated checks. If `withChecks` is also set to true, then filter has no effect and all checks will be displayed. The default value is `false`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

<br />

Example Request:

```
curl -g -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
https://us-west-2-api.cloudconformity.com/v1/checks?accountIds=r1gyR4cqg&page[size]=100&page[number]=0&filter[regions]=us-west-2&filter[ruleIds]=EC2-001,EC2-002&filter[statuses]=SUCCESS&filter[categories]=security&filter[riskLevels]=HIGH&filter[services]=EC2&filter[createdDate]=1502572157914
```

Example Response:

###### Note the size of this response can be quite large and the example below is purposefully truncated.

###### The check property `providerResourceId` is only returned for a limited amount of AWS rules. This property represents the [AWS ARN](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html) of the related resource.

```json
{
  "data": [
    {
      "type": "checks",
      "id": "ccc:94qQ4DnOB:AG-003:APIGateway:us-east-1:pl63negesk",
      "attributes": {
        "region": "us-east-1",
        "status": "FAILURE",
        "risk-level": "LOW",
        "pretty-risk-level": "Low",
        "message": "API Security Automations - WAF Bad Bot API has stages without active tracing enabled",
        "resource": "pl63negesk",
        "descriptorType": "apigateway-restapi",
        "resourceName": "API Gateway REST API",
        "last-modified-date": 1561697456359,
        "created-date": 1561697456359,
        "categories": ["operational-excellence"],
        "last-updated-date": null,
        "failure-discovery-date": 1561697456359,
        "ccrn": "ccrn:aws:94qQ4DnOB:APIGateway:us-east-1:pl63negesk",
        "tags": [],
        "cost": 0,
        "waste": 0,
        "rule-title": "Tracing Enabled",
        "link": "https://us-east-1.console.aws.amazon.com/apigateway/home?region=us-east-1#/apis/pl63negesk/resources",
        "provider": "aws",
        "resolutionPageUrl": "https://www.cloudconformity.com/conformity-rules/APIGateway/tracing.html#B1nHYYpwx",
        "providerResourceId": "arn:aws:apigateway:us-west-1::/restapis/pl63negesk/*"
      },
      "relationships": {
        "rule": {
          "data": {
            "type": "rules",
            "id": "AG-003"
          }
        },
        "account": {
          "data": {
            "type": "accounts",
            "id": "94qQ4DnOB"
          }
        }
      }
    }
  ],
  "meta": {
    "total-pages": 714
  }
}
```

Example Request:

```
curl -g -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
https://us-west-2-api.cloudconformity.com/v1/checks?accountIds=e13vR4c3g&page[size]=100&page[number]=0&&filter[regions]=eastus&filter[ruleIds]=KeyVault-004&filter[services]=KeyVault&filter[statuses]=SUCCESS&filter[categories]=security&filter[riskLevels]=HIGH
```

Example Response:

```json
{
  "data": [
    {
      "type": "checks",
      "id": "ccc:5pgWNtDMj:KeyVault-004:KeyVault:eastus:/subscriptions/8dfbsdfe-we13-46we-9963-188128793ef40/resourceGroups/myDevResources/providers/Microsoft.KeyVault/vaults/myDevKeyVault-eastus",
      "attributes": {
        "region": "eastus",
        "status": "FAILURE",
        "risk-level": "MEDIUM",
        "pretty-risk-level": "Medium",
        "message": "AuditEvent logging is not enabled for Azure Key Vault 'myDevKeyVault-eastus'",
        "resource": "/subscriptions/8dfbsdfe-we13-46we-9963-188868997f40/resourceGroups/myDevResources/providers/Microsoft.KeyVault/vaults/myDevKeyVault-eastus",
        "descriptorType": "keyvault-vaults",
        "link-title": "myDevKeyVault-eastus",
        "resourceName": "KeyVault Vault",
        "last-modified-date": 1588560354122,
        "created-date": 1588560354122,
        "categories": ["security"],
        "last-updated-date": null,
        "failure-discovery-date": 1588560354122,
        "ccrn": "ccrn:azure:5pgWNtDMj:KeyVault:eastus:/subscriptions/8dfbsdfe-we13-46we-9963-188868997f40/resourceGroups/myDevResources/providers/Microsoft.KeyVault/vaults/myDevKeyVault-eastus",
        "tags": [],
        "cost": 0,
        "waste": 0,
        "rule-title": "Enable AuditEvent Logging for Azure Key Vaults",
        "link": "https://portal.azure.com/#resource//subscriptions/8dfbsdfe-we13-46we-9963-188868997f40/resourceGroups/myDevResources/providers/Microsoft.KeyVault/vaults/myDevKeyVault-eastus",
        "provider": "azure",
        "resolution-page-url": "https://wdevelopment.cloudconformity.com/knowledge-base/azure/KeyVault/enable-audit-event-logging-for-azure-key-vaults.html#Jo29j"
      },
      "relationships": {
        "rule": { "data": { "type": "rules", "id": "KeyVault-004" } },
        "account": { "data": { "type": "accounts", "id": "dlkf19" } }
      }
    }
  ],
  "meta": { "total": 1 }
}
```
