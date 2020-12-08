This endpoint allows ADMIN, POWER USERS, and users with CUSTOM access to accounts to get the current setting that Cloud Conformity uses to determine when Conformity Bot is run and on which regions the Conformity Bot is disabled. This endpoint also supports updating single attributes under the `settings` field (see below) in which case, only attributes passed in the request body will be updated.

Example Request to update all attributes:<br />
This request disables the Conformity Bot for two accounts. Conformity Bot is disabled in all regions until the specified date-time, after which it will run every 10 hours for all regions besides `us-west-2`.

```shell script
curl -X PATCH \
-H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey eab0b7914c3ebv45bcK02cW33ff9564cec8" \
-d '
{
  "data": {
    "type": "accounts",
    "attributes": {
      "settings": {
        "bot": {
          "delay": 10,
          "disabledRegions": {
             "us-west-2": true
           },
           "disabled": true,
           "disabledUntil": 1591751339519,
        }
      }
    }
  },
  "meta": {
       "otherAccounts": ["cfe80897"]
  }
};' \
https://us-west-2-api.cloudconformity.com/v1/accounts/2fwmithMj/settings/bot
```

Example Response:

```json5
{
  data: [
    {
      type: "accounts",
      id: "2fwmithMj",
      attributes: {
        name: "Test AWS Account",
        // ...
        settings: {
          rules: [
            // ...
          ],
          bot: {
            lastModifiedFrom: "12.345.67.890",
            delay: 10,
            disabledRegions: {
              "us-west-2": true
            },
            disabled: true,
            disabledUntil: 1591751339519,
            lastModifiedBy: "3456d0"
          }
        },
        // ...
        "cloud-type": "aws",
        "managed-group-id": "23784h"
      },
      relationships: {
        organisation: {
          data: {
            type: "organisations",
            id: "moid324"
          }
        }
      }
    },
    {
      type: "accounts",
      id: "cfe80897",
      attributes: {
        name: "Test Azure Account",
        // ...
        settings: {
          rules: [
            // ...
          ],
          bot: {
            lastModifiedFrom: "12.345.67.890",
            delay: 10,
            disabled: true,
            disabledUntil: 1591751339519,
            lastModifiedBy: "3456d0"
          }
        },
        // ...
        "cloud-type": "azure",
        "managed-group-id": "23784h"
      },
      relationships: {
        organisation: {
          data: {
            type: "organisations",
            id: "moid324"
          }
        }
      }
    }
  ]
}
```

Other requests for example use cases:<br />
Temporarily disable Conformity Bot until the specified date-time:

```shell script
curl -X PATCH \
-H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey eab0b7914c3ebv45bcK02cW33ff9564cec8" \
-d '
{
  "data": {
    "type": "accounts",
    "attributes": {
      "settings": {
        "bot": {
          "disabled": true,
          "disabledUntil": 1591751339519,
        }
      }
    }
  }
};' \
https://us-west-2-api.cloudconformity.com/v1/accounts/2fwmithMj/settings/bot
```

Disable Conformity Bot indefinitely:

```shell script
curl -X PATCH \
-H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey eab0b7914c3ebv45bcK02cW33ff9564cec8" \
-d '
{
  "data": {
    "type": "accounts",
    "attributes": {
      "settings": {
        "bot": {
          "disabled": true
        }
      }
    }
  }
};' \
https://us-west-2-api.cloudconformity.com/v1/accounts/2fwmithMj/settings/bot
```

Disable Conformity Bot runs for a few regions and increase delay between enabled regions:

```shell script
curl -X PATCH \
-H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey eab0b7914c3ebv45bcK02cW33ff9564cec8" \
-d '
{
  "data": {
    "type": "accounts",
    "attributes": {
      "settings": {
        "bot": {
          "delay": 10,
          "disabledRegions": {
            "us-east-1": true,
            "us-east-2": true,
            "us-west-2": true,
            "ap-southeast-2": true
          }
        }
      }
    }
  }
};' \
https://us-west-2-api.cloudconformity.com/v1/accounts/2fwmithMj/settings/bot
```
