A `PATCH` request to this endpoint allows you to customize rule settings for the specified account.

This feature is used in conjunction with the `GET` request to the same endpoint for copying rule settings from one account to another. An example of this function is provided in the examples folder.

**IMPORTANT:**
&nbsp;&nbsp;&nbsp;To copy rule settings from one account to another, you first need to:

1. Obtain rule settings from the desired account. [Get rule settings](#tag/Accounts/paths/~1accounts~1{id}~1settings~1rules/get)
1. Paste rule settings as is into the body of the PATCH request following the format below.

**Note:** If the account contains rule settings that are marked as deprecated and have not been disabled, the following meta warning will be included in the response:

```json
{
  "meta": {
    "deprecation": {
      "warning": {
        "message": "1 manually configured rule in this account is deprecated. Refer to our Help Pages for instructions.",
        "link": "https://www.cloudconformity.com/help/rules.html",
        "rules": [
          {
            "riskLevel": "LOW",
            "id": "RuleID-001",
            "extraSettings": null,
            "provider": "aws",
            "enabled": true,
            "exceptions": { "resources": null, "tags": null }
          }
        ]
      }
    }
  }
}
```

#### Errors:

Some errors thrown from rule settings validation may need further clarification. Below is a list.
For more information about specific rule configurations, consult [Cloud Conformity Services Endpoint](https://us-west-2.cloudconformity.com/v1/services)

| Error Details                                                                                             | Resolution                                                                                                                |
| --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| This Real-Time Threat Monitoring (or cost) package rule `rule.id` is not part of the account subscription | Remove that rule setting from the array                                                                                   |
| `ruleId` is not configurable from this endpoint.                                                          | This is either a cost-setting or organisation-setting which you cannot configure via this account rule settings endpoint. |
| Rule risk level missing for `ruleId`                                                                      | `ruleSetting.riskLevel` is a required parameter                                                                           |
| Rule risk level provided for `ruleId` is incorrect                                                        | only "LOW", "MEDIUM", "HIGH", "VERY_HIGH", and "EXTREME" are accepted risk levels                                         |
| Rule enable status is not valid for `ruleId`                                                              | `ruleSetting.enabled` is a required boolean parameter                                                                     |
| One or more rule setting property is invalid for `ruleId`                                                 | remove the `ruleSetting` property if it is not `id`, `enabled`, `riskLevel`, `extraSettings`, or `ruleExists`             |
| Provider `XXX` is invalid for `ruleId`                                                                    | `provider` must match the cloud provider for the rule                                                                     |

**Extra Settings**
Rule `ruleId` is not configurable | remove `ruleSetting.extraSettings`, you may only change risk level or enable/disable this rule. If you are directly copying this rule from another account and getting this message, this rule may have been previously configurable and is no longer.
