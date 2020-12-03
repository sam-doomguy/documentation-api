This endpoint allows you to get the details of the specified user.

Example Response:

```
{
    "data": {
        "type": "users",
        "id": "CClqMqknVb",
        "attributes": {
            "first-name": "Cool",
            "last-name": "Claude",
            "role": "ADMIN",
            "email": "cc@coolclaude.com",
            "status": "ACTIVE",
            "last-login-date": 1523009079960,
            "created-date": 1499359762438,
            "summary-email-opt-out": true,
            "mobile": "15144008080",
            "mobile-country-code": "CA",
            "mobile-verified": true
        },
        "relationships": {
            "organisation": {
                "data": {
                    "type": "organisations",
                    "id": "A9NDYY12z"
                }
            }
        }
    }
}
```

Example request when an ADMIN queries a USER with custom permissions:

```
curl -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
https://us-west-2-api.cloudconformity.com/v1/users/517uNyIvG
```

Example Response:

```
{
    "data": {
        "type": "users",
        "id": "517uNyIvG",
        "attributes": {
            "first-name": "Scott",
            "last-name": "Tiger",
            "role": "USER",
            "email": "******@cloudconformity.com",
            "status": "ACTIVE",
            "mfa": false,
            "last-login-date": 1503586843842,
            "created-date": 1485834564224
        },
        "relationships": {
            "organisation": {
                "data": {
                    "type": "organisations",
                    "id": "A9NDYY12z"
                }
            },
            "accountAccessList": [
                {
                    "account": "account1",
                    "level": "FULL"
                },
                {
                    "account": "account2",
                    "level": "READONLY"
                },
                {
                    "account": "account3",
                    "level": "FULL"
                },
                {
                    "account": "account4",
                    "level": "NONE"
                },
                {
                    "account": "account5",
                    "level": "NONE"
                },
                {
                    "account": "account6",
                    "level": "NONE"
                }
        }
    }
}
```
