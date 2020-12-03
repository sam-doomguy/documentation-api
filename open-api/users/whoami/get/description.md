Gets current user.

Example Response:

```
{
    "data": {
        "type": "users",
        "id": "517uNyIvG",
        "attributes": {
            "first-name": "Scott",
            "last-name": "Tiger",
            "role": "ADMIN",
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
            }
        }
    }
}
```

Example Request for a USER with custom permissions:

```
curl -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
https://us-west-2-api.cloudconformity.com/v1/users/whoami
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
                    "account": "acc1abc",
                    "level": "FULL"
                },
                {
                    "account": "acc2abc",
                    "level": "READONLY"
                },
                {
                    "account": "acc3abc",
                    "level": "FULL"
                }
        }
    }
}
```
