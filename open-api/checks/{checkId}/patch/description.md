This endpoint is used to either update one custom check OR suppress/unsuppressed one normal check.

**IMPORTANT:**
&nbsp;&nbsp;&nbsp;Some guidelines about using this endpoint:

1. When updating a custom check, you must leave `region`, `resource`, `service` attributes and `relationship.account` and `relationship.rule` unchanged. These are unique identifier parameters for custom checks and must be always present and unchanged once check is created.
2. Suppression of check via this endpoint only works with FAILING checks and not successful checks.

**Note:**
the Cloud Conformity ID of a check for an Azure account contains the forward slash character `/` which needs to be replaced with the encoded character `%2F` when passed in the request URL.
e.g to update a check for an Azure account with the ID:
`ccc:r2gyR4cqg:SecurityCenter-008:SecurityCenter:global:/subscriptions/9f7bcadb-3626-46dx-9917-1397384797f40/providers/Microsoft.Authorization/policyAssignments/SecurityCenterBuiltIn`
the URL in the request body should be:
`https://us-west-2-api.cloudconformity.com/v1/checks/ccc:r2gyR4cqg:SecurityCenter-008:SecurityCenter:global:%2Fsubscriptions%2F9f7bcadb-3626-46dx-9917-1397384797f40%2Fproviders%2FMicrosoft.Authorization%2FpolicyAssignments%2FSecurityCenterBuiltIn`

Example request for updating a custom check:

```
curl -X PATCH \
-H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
-d '
{
    "data": {
        "type": "checks",
        "attributes": {
            "region": "us-west-2",
            "resource": "sg-956d00ea",
            "risk-level": "VERY_HIGH",
            "status": "FAILURE",
            "service": "EC2",
            "categories": ["security"],
            "rule-title": "Custom Rule about EC2 SGs",
            "message": "Updated message about this check",
            "resolution-page-url": "https://test.com/custom-001.html#"
            "extradata": [
                {
                    "label": "This will show up on the UI",
                    "name": "nameForReference",
                    "type": "META",
                    "value": "string or number or boolean"
                },
                {
                    "label": "It is good to be descriptive",
                    "name": "forReference",
                    "type": "META",
                    "value": "hello world!"
                }
            ],
            "tags": ["key0::value0", "key1::value1"]
        },
        "relationships": {
            "rule": {
                "data": {
                    "type": "rules",
                    "id": "CUSTOM-001"
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
}' \
https://us-west-2-api.cloudconformity.com/v1/checks/ccc:H19NxM15-:CUSTOM-001:EC2:us-west-2:sg-956d00ea
```

Example Response:

```
{
    "data": {
        "type": "checks",
        "id": "ccc:H19NxM15-:CUSTOM-001:EC2:us-west-2:sg-956d00ea",
        "attributes": {
            "region": "us-west-2",
            "status": "FAILURE",
            "service": "EC2",
            "risk-level": "VERY_HIGH",
            "pretty-risk-level": "Very High",
            "rule-title": "Custom Rule about EC2 SGs",
            "message": "Updated message about this check",
            "resource": "sg-956d00ea",
            "categories": ["security"],
            "last-modified-date": 1526566995282,
            "created-date": 1521660152755,
            "failure-discovery-date": 1521660152755,
            "resolution-page-url": "https://test.com/custom-001.html#",
            "extradata": [
                {
                    "label": "This will show up on the UI",
                    "name": "nameForReference",
                    "type": "META",
                    "value": "string or number or boolean"
                },
                {
                    "label": "It is good to be descriptive",
                    "name": "forReference",
                    "type": "META",
                    "value": "hello world!"
                }
            ],
            "tags": ["key0::value0", "key1::value1"]
        },
        "relationships": {
            "rule": {
                "data": {
                    "type": "rules",
                    "id": "CUSTOM-001"
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
```

Example request for suppressing a check:

```
curl -X PATCH \
-H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
-d '
{
    "data": {
        "type": "checks",
        "attributes": {
            "suppressed": true,
            "suppressed-until": 1526574705655
        }
    },
    "meta": {
        "note": "suppressed for 1 week, failure not-applicable during project xyz"

    }
}; \

https://us-west-2-api.cloudconformity.com/v1/checks/ccc:H19NxM15:EC2-013:EC2:ap-southeast-2:
```

Example Response:

```
{
    "data": {
        "type": "checks",
        "id": "ccc:H19NxM15:Config-001:Config:us-west-2:",
        "attributes": {
            "region": "us-west-2",
            "status": "FAILURE",
            "risk-level": "HIGH",
            "pretty-risk-level": "High",
            "message": "AWS Config is not enabled for us-west-2 region ",
            "last-modified-date": 1526571108174,
            "created-date": 1513472920569,
            "categories": [
                "security"
            ],
            "suppressed": true,
            "last-updated-date": null,
            "failure-discovery-date": 1526571108174,
            "failure-introduced-by": null,
            "resolved-by": null,
            "last-updated-by": null,
            "extradata": null,
            "tags": [],
            "cost": 0,
            "waste": 0,
            "suppressed-until": 1526574705655,
            "not-scored": false,
            "rule-title": "AWS Config Enabled",
            "resolution-page-url": "https://www.cloudconformity.com/conformity-rules/Config/aws-config-enabled.html#"
        },
        "relationships": {
            "rule": {
                "data": {
                    "type": "rules",
                    "id": "Config-001"
                }
            },
            "account": {
                "data": {
                    "type": "accounts",
                    "id": "HJtqfslfG"
                }
            }
        }
    }
}
```
