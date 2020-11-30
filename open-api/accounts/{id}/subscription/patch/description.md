A PATCH request to this endpoint allows you to change the add-on package subscription of the specified account.

We recommend you first [Get account details](#tag/Accounts/paths/~1accounts~1{id}/get) to verify that the subscription needs to be updated.

**IMPORTANT:**
&nbsp;&nbsp;&nbsp;Only ADMIN users can use this endpoint.

_Please note the server will not accept both hasRealTimeMonitoring and subscriptionType in the request body. Please provide either hasRealTimeMonitoring or subscriptionType_

Example Request with the old field hasRealTimeMonitoring:

```shell script
curl -X PATCH \
-H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
-d '
{
  "data": {
    "attributes": {
      "costPackage": true,
      "hasRealTimeMonitoring": false
    }
  }
}' \
https://us-west-2-api.cloudconformity.com/v1/accounts/AgA12vIwb/subscription
```

Example Request with new field subscriptionType:

````shell script
curl -X PATCH \
-H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
Example Request with the old field hasRealTimeMonitoring:

```shell script
curl -X PATCH \
-H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
-d '
{
  "data": {
    "attributes": {
      "costPackage": true,
      "hasRealTimeMonitoring": false
    }
  }
}' \
https://us-west-2-api.cloudconformity.com/v1/accounts/AgA12vIwb/subscription
````

Example Request with new field subscriptionType:

```shell script
curl -X PATCH \
-H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
-d '
{
  "data": {
    "attributes": {
      "costPackage": true,
      "subscriptionType": "essentials"
    }
  }
}' \
https://us-west-2-api.cloudconformity.com/v1/accounts/AgA12vIwb/subscription
```

Example Response:

```json5
{
  data: {
    type: "accounts",
    id: "AgA12vIwb",
    attributes: {
      name: "myCCaccount",
      environment: "myAWSenv",
      "awsaccount-id": "123456789101",
      status: "ACTIVE",
      "has-real-time-monitoring": false, // **Note:** This field is planned to be replaced with subscription-type in the future.
      "cost-package": true,
      "last-notified-date": 1504113512701,
      "last-checked-date": 1504113511956,
      "available-runs": 5,
      "subscription-type": "essentials"
    },
    relationships: {
      organisation: {
        data: {
          type: "organisations",
          id: "B1nHYYpwx"
        }
      }
    }
  }
}
```
