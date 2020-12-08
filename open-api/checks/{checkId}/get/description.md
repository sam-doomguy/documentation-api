This endpoint allows you to get the details of the specified check.

**Note:**

The Cloud Conformity ID of a check for an Azure account contains the forward slash character `/` which needs to be replaced with the encoded character `%2F` when passed in the request URL.

Example Request to view details of a check for an AWS account:

```
curl -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
'https://us-west-2-api.cloudconformity.com/v1/checks/ccc:r2gyR4cqg:IAM-017:IAM:global:groups-test'
```

Example Response:

```
{
    "data": {
        "type": "checks",
        "id": "ccc:r2gyR4cqg:IAM-017:IAM:global:groups-test",
        "attributes": {
            "region": "global",
            "status": "FAILURE",
            "risk-level": "LOW",
            "pretty-risk-level": "High",
            "message": "IAM Group test contains no user",
            "last-modified-date": 1500166639466,
            "created-date": 1500166639466
            "last-updated-date": 1500166639466,
            "failure-discovery-date": 1498910777689,
            "last-updated-by": "SYSTEM",
            "resolved-date": 1518409298274,
            "resolved-by": null,
            "ccrn": "ccrn:aws:r1gyR4cqg:IAM:global:groups-test",
            "extradata": null,
            "tags": [],
            "cost": 0,
            "waste": 0,
            "not-scored": false,
            "ignored": null,
            "rule-title": "Password Policy Present",
            "resolution-page-url": "https://www.cloudconformity.com/conformity-rules/IAM/unused-iam-group.html#",
            "uuid": "arn:aws:iam::1234567890:group/groups-test"
        },
        "relationships": {
            "rule": {
                "data": {
                    "type": "rules",
                    "id": "IAM-017"
                }
            },
            "account": {
                "data": {
                    "type": "accounts",
                    "id": "r1gyR4cqg"
                }
            }
        }
    }
}
```

Example Request to view details of a check for an Azure account with ID <br />
`ccc:r2gyR4cqg:SecurityCenter-008:SecurityCenter:global:/subscriptions/9f7bcadb-3626-46dx-9917-1397384797f40/providers/Microsoft.Authorization/policyAssignments/SecurityCenterBuiltIn`:

```shell script
curl -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
'https://us-west-2-api.cloudconformity.com/v1/checks/ccc:r2gyR4cqg:SecurityCenter-008:SecurityCenter:global:%2Fsubscriptions%2F9f7bcadb-3626-46dx-9917-1397384797f40%2Fproviders%2FMicrosoft.Authorization%2FpolicyAssignments%2FSecurityCenterBuiltIn'
```
