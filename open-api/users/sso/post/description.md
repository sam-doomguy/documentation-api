This endpoint is only available for organisations with an external identity provider setup.

Only ADMINS from an external identity provider can use this endpoint to add new sso users to their organisation.

Please note only accounts (listed inside the `accessList`) in the request will get updated, existing account permissions are retained.
If a new user is added with the role of `USER` and an `accessList` is not provided, the users level permission for all accounts will default to `NONE`.
If a user is added back into the organisation with the role of `USER`, the user will maintain the old account level permissions, unless an `accessList` is provided to update the permission.

Example request for a user with an ADMIN role:

```
curl -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
-d
'{
    "data": {
        "attributes": {
            "firstName": "sso",
            "lastName": "user",
            "role": "ADMIN",
            "email": "sso_user@cloudconformity.com"
        }
    }
}'
\
https://us-west-2-api.cloudconformity.com/v1/users/sso
```

Example Response:

```
{
    "data": {
        "type": "users",
        "id": "abcdefg",
        "attributes": {
            "first-name": "sso",
            "last-name": "user",
            "role": "ADMIN",
            "email": "sso_user@cloudconformity.com",
            "status": "ACTIVE",
            "last-login-date": null,
            "created-date": 1575943588002,
            "has-credentials": false
        },
        "relationships": {
            "organisation": {
                "data": {
                    "type": "organisations",
                    "id": "hijklmnop"
                }
            }
        }
    }
}
```

Example request for adding a user with custom permissions:

```
curl -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
-d
'{
    "data": {
        "attributes": {
            "firstName": "sso",
            "lastName": "user",
            "role": "USER",
            "email": "sso_user@cloudconformity.com",
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
https://us-west-2-api.cloudconformity.com/v1/users/sso
```
