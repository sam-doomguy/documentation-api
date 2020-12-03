This endpoint allows you to invite a user to your organisation.

Please note only accounts (listed inside the `accessList`) in the request will get updated, existing account permissions are retained.
If a new user is invited with the role of `USER` and an `accessList` is not provided, the users level permission for all accounts will default to `NONE`
If a user is re-invited with the role of `USER`, the user will maintain the old account level permissions, unless an `accessList` is provided to update the permission.

Example Request for inviting a user as an ADMIN:

```
curl -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
-d
'{
    "data": {
        "attributes": {
            "firstName": "Cool",
            "lastName": "Claude",
            "role": "ADMIN",
            "email": "cc_user@cloudconformity.com"
        }
    }
}'
\
https://us-west-2-api.cloudconformity.com/v1/users
```

Example Response:

```
{
    "data": {
        "type": "users",
        "id": "OhnzPVXY",
        "attributes": {
            "first-name": "Cool",
            "last-name": "Claude",
            "role": "ADMIN",
            "email": "cc_user@cloudconformity.com",
            "status": "INVITED",
            "last-login-date": null,
            "created-date": 1575943588002,
            "has-credentials": false
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

Example request for inviting a user with custom permissions:

```
curl -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
-d
'{
    "data": {
        "attributes": {
            "firstName": "Cool",
            "lastName": "Claude",
            "role": "USER",
            "email": "cc_user@cloudconformity.com",
            "accessList": [
                {
                    "account": "A9_DsY12z",
                    "level": "FULL"
                },
                {
                    "account": "BqdYgfas",
                    "level": "NONE"
                },
                {
                    "account": "kPiASD21",
                    "level": "READONLY"
                }
            ]
        }
    }
}'
\
https://us-west-2-api.cloudconformity.com/v1/users
```
