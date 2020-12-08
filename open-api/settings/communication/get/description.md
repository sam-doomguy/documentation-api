This endpoint allows you to get communication settings. This feature can be used in conjunction with a POST request to copy communication settings from one account to others.

**IMPORTANT:**
&nbsp;&nbsp;&nbsp;Users with different roles can get different results from this endpoint.

The table below describes the relationship between user role or account access level, and type of data the user can get for account level settings.

| Role / access to the account   | Account-Level Settings           |
| ------------------------------ | -------------------------------- |
| ADMIN                          | Full settings with configuration |
| FULL access to the account     | Full setting with configurations |
| READONLY access to the account | Setting without configurations   |
| NO access to the account       | No setting                       |

For organisation level settings, the ADMIN users are the only users who can access those settings. The table below describes the relationship between user role and type of the data user can get for organisation level settings.

| Role       | Organisation-Level Settings      |
| ---------- | -------------------------------- |
| ADMIN      | Full settings with configuration |
| POWER USER | No setting                       |
| READONLY   | No setting                       |
| USER       | No setting                       |

Example request for email-only settings:

```

curl -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
https://us-west-2-api.cloudconformity.com/v1/settings/communication?accountId=H19NxM15-&channel=email&includeParents=true
```

Example Response for an ADMIN user:
(**Note:** The first object is for an organisation-level setting: `setting.relationships.account.data` is NULL)

```
{
    "data": [
        {
            "type": "settings",
            "id": "communication:email-HJgeFWmpVf",
            "attributes": {
                "type": "communication",
                "manual": false,
                "enabled": true,
                "filter": {
                    "services": [
                        "Organizations"
                    ],
                    "suppressed": false
                },
                "configuration": {
                    "users": [
                        "BJlqMqknVb"
                    ]
                },
                "channel": "email"
            },
            "relationships": {
                "organisation": {
                    "data": {
                        "type": "organisations",
                        "id": "ryqMcJn4b"
                    }
                },
                "account": {
                    "data": null
                }
            }
        },
        {
            "type": "settings",
            "id": "ryqs8LNKW:communication:email-Ske1cKKEvM",
            "attributes": {
                "type": "communication",
                "manual": false,
                "enabled": true,
                "filter": {
                    "categories": [
                        "security"
                    ],
                    "suppressed": false
                },
                "configuration": {
                    "users": [
                        "HyL7K6GrZ"
                    ]
                },
                "channel": "email"
            },
            "relationships": {
                "organisation": {
                    "data": {
                        "type": "organisations",
                        "id": "ryqMcJn4b"
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
    ]
}
```

Example response for a user with FULL access to the acount:
(**Note:** The list does not contain organisation-level settings as only ADMIN users have access to organisation-level settings).

```
{
    "data": [
        {
            "type": "settings",
            "id": "ryqs8LNKW:communication:email-Ske1cKKEvM",
            "attributes": {
                "type": "communication",
                "manual": false,
                "enabled": true,
                "filter": {
                    "categories": [
                        "security"
                    ],
                    "suppressed": false
                },
                "configuration": {
                    "users": [
                        "HyL7K6GrZ"
                    ]
                },
                "channel": "email"
            },
            "relationships": {
                "organisation": {
                    "data": {
                        "type": "organisations",
                        "id": "ryqMcJn4b"
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
    ]
}
```

Example request for **organisation-level** email-only settings:

```

curl -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
https://us-west-2-api.cloudconformity.com/v1/settings/communication?channel=email
```

Example Response for an ADMIN user:

```
{
    "data": [
        {
            "type": "settings",
            "id": "communication:email-HJgeFWmpVf",
            "attributes": {
                "type": "communication",
                "manual": false,
                "enabled": true,
                "filter": {
                    "services": [
                        "Organizations"
                    ],
                    "suppressed": false
                },
                "configuration": {
                    "users": [
                        "BJlqMqknVb"
                    ]
                },
                "channel": "email"
            },
            "relationships": {
                "organisation": {
                    "data": {
                        "type": "organisations",
                        "id": "ryqMcJn4b"
                    }
                },
                "account": {
                    "data": null
                }
            }
        }
    ]
}
```

Example request for **account-level** email-only settings:

```

curl -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
https://us-west-2-api.cloudconformity.com/v1/settings/communication?accountId=H19NxM15-&channel=email
```

Example Response for an ADMIN user:
(**Note:** Without the `includeParents` parameter, no organisation-level settings are shown.)

```
{
    "data": [
        {
            "type": "settings",
            "id": "ryqs8LNKW:communication:email-Ske1cKKEvM",
            "attributes": {
                "type": "communication",
                "manual": false,
                "enabled": true,
                "filter": {
                    "categories": [
                        "security"
                    ],
                    "suppressed": false
                },
                "configuration": {
                    "users": [
                        "HyL7K6GrZ"
                    ]
                },
                "channel": "email"
            },
            "relationships": {
                "organisation": {
                    "data": {
                        "type": "organisations",
                        "id": "ryqMcJn4b"
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
    ]
}
```
