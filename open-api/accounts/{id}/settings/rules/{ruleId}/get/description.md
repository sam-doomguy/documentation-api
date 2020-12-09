A `GET` request to this endpoint allows you to get configured rule setting for the specified rule Id of the specified account.

If a specific rule has never been configured, the request will result in a `404` error.

For example, even if our bots run rule `RDS-018` for your account hourly, if you have never configured it, trying to get rule settings for `RDS-018` will result in a `404` error.

**Note:** If the rule setting being retrieved from the account is marked as deprecated and has not been disabled (`enabled`: `false`), the following meta warning will be included in the response:

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
