Update the role and permissions of the specified user.
Only ADMINs can perform the update to other users within the same organisation.

Please note only accounts (listed inside the `accessList`) in the request will get updated, existing account permissions are retained.

Example Request to set the user's role to ADMIN | POWER_USER | READ_ONLY:

```
curl -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
-d '
{
    "data": {
        "role": "ADMIN"
    }
}
' \
https://us-west-2-api.cloudconformity.com/v1/users/CClqMqknVb \

```

Example Response

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

Example request to set the user's role to USER and account level access:

```
curl -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
-d '
{
    "data": {
        "role": "USER",
        "accessList": [
            {
                "account": "ad03IHuI_",
                "level": "FULL"
            },
            {
                "account": "Oa1j-gGTX",
                "level": "READONLY"
            },
            {
                "account": "Pa_dgRTA",
                "level": "NONE"
            }
        ]
    }
}
' \
https://us-west-2-api.cloudconformity.com/v1/users/CClqMqknVb \

```

Example request to set the user's role to USER and updating a specific account level access:

```
curl -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
-d '
{
    "data": {
        "role": "USER",
        "accessList": [
            {
                "account": "ad03IHuI_",
                "level": "READONLY"
            }
        ]
    }
}
' \
https://us-west-2-api.cloudconformity.com/v1/users/CClqMqknVb \

```

Example Response

```
{
    "data": {
        "type": "users",
        "id": "CClqMqknVb",
        "attributes": {
            "first-name": "Cool",
            "last-name": "Claude",
            "role": "USER",
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
