This endpoint allows you to create a new profile and subsequently add rule settings to the new profile. Saving rule settings via this endpoint will overwrite existing settings with those passed in the request. This allows for the following requests to be made:

| Request                                                                                       | Details                                                                                                             | Parameters                                      |
| --------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| [Saving a new profile](#saving-a-new-profile)                                                 | Save a new profile with name and description                                                                        | Profile name and description                    |
| [Save new profile with rule settings included](#save-new-profile-with-rule-settings-included) | Save a new profile and a batch of configured rule settings upon profile creation                                    | Profile name and description, and rule settings |
| [Save rule settings to an existing Profile](#save-rule-settings-to-an-existing-profile)       | Add a batch of configured rule settings to an empty profile or overwrite existing rule settings and profile details | Profile details and Rule settings               |
| [Delete all settings](#tag/Profiles/paths/~1profiles~1{id}/delete)                            | Retain the profile but clear all rule settings                                                                      | Profile ID                                      |

### Saving a new Profile

The expected behavior of this request is to create a new profile.

Example request for saving a new profile:

```
curl -X POST -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey YOUR-API-KEY" \
-d '
{
  "data": {
    "type": "profiles",
    "attributes": {
      "name": "New-Test-Profile",
      "description": "A test description for a new profile."
    }
  }
}' \
https://us-west-2-api.cloudconformity.com/v1/profiles/
```

Example Response:

```
{
  "data": {
    "type": "profiles",
    "id": {profile-id},
    "attributes": {
      "name": "New-Test-Profile",
      "description": "A test description for a new profile."
    }
  }
}

```

### Saving Rule Settings to your Profile

This option allows you to add rule settings to your profile at creation or afterwards.

#### Rule Settings

There are some attributes you need to pass inside the rule settings attributes object. The table below provides more information about attributes options:

| Attribute             | Details                                                                  | Accepted Values                                  |
| --------------------- | ------------------------------------------------------------------------ | ------------------------------------------------ |
| enabled               | This attribute determines whether this setting is enabled                | true, false                                      |
| riskLevel             | This attribute configures the level of risk assigned to the rule         | "EXTREME", "VERY_HIGH", "HIGH", "MEDIUM", "LOW"  |
| extraSettings         | This array stores objects that configure the extra settings to this rule | {name: "ttl", type: "ttl", value: 72, ttl: true} |
| exceptions            | This array stores objects that configure exceptions to this rule         |                                                  |
| exceptions: tags      | This attribute tags this exception                                       | "NewS3BucketTag" or "tagKey::tagValue"           |
| exceptions: resources | This attribute applies this exception to the following resources         | "i-xxxx"                                         |

### Save new profile with rule settings included

The expected behavior of this request is to save a new profile and configure new rule settings associated with that profile.

Example request for new profile creation including rule settings:

```
curl -X POST -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey YOUR-API-KEY" \
-d '
{
  "included": [
    {
      "type": "rules",
      "id": "EC2-001",
      "attributes": {
        "enabled": false,
        "exceptions": {
          "tags": ["TestUpdateTags"],
          "resources": []
        },
        "extraSettings": [],
        "riskLevel": "LOW"
      }
    },
    {
      "type": "rules",
      "id": "RTM-002",
      "attributes": {
        "enabled": true,
        "exceptions": {
          "tags": [],
          "resources": []
        },
        "extraSettings": [
          {
            "name": "ttl",
            "type": "ttl",
            "value": 72,
            "ttl": true
          }
        ],
        "riskLevel": "MEDIUM"
      }
    }
  ],
  "data": {
    "type": "profiles",
    "attributes": {
      "name": "New-Test-Profile",
      "description": "A test description for a new profile."
    },
    "relationships": {
      "ruleSettings": {
        "data": [
          {
            "type": "rules",
            "id": "EC2-001"
          },
          {
            "type": "rules",
            "id": "RTM-002"
          }
        ]
      }
    }
  }
}
'\
https://us-west-2-api.cloudconformity.com/v1/profiles/
```

Example Response:

```
{
  "included": [
    {
      "type": "rules",
      "id": "EC2-001",
      "attributes": {
        "enabled": false,
        "exceptions": {
          "tags": ["TestUpdateTags"],
          "resources": []
        },
        "extraSettings": [],
        "riskLevel": "LOW"
      }
    },
    {
      "type": "rules",
      "id": "RTM-002",
      "attributes": {
        "enabled": true,
        "exceptions": {
          "tags": [],
          "resources": []
        },
        "extraSettings": [
          {
            "name": "ttl",
            "type": "ttl",
            "value": 72,
            "ttl": true
          }
        ],
        "riskLevel": "MEDIUM"
      }
    }
  ],
  "data": {
    "type": "profiles",
    "id": {profile-id},
    "attributes": {
      "name": "Test-Profile-1",
      "description": "A test profile with rule settings."
    },
    "relationships": {
      "ruleSettings": {
        "data": [
          {
            "type": "rules",
            "id": "EC2-001"
          },
          {
            "type": "rules",
            "id": "RTM-002"
          }
        ]
      }
    }
  }
}

```

### Save rule settings to an existing Profile

The expected behavior of this is request to overwrite all existing rule settings to a configured profile or write new rule settings to an existing empty profile.

You must indicate the profile id in the request body otherwise a new profile will be created with the indicated rule settings configured.

Example request for saving rule settings:

```
curl -X POST -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey YOUR-API-KEY" \
-d '
{
  "included": [
    {
      "type": "rules",
      "id": "EC2-001",
      "attributes": {
        "enabled": false,
        "exceptions": {
          "tags": ["TestUpdateTags"],
          "resources": []
        },
        "extraSettings": [],
        "riskLevel": "LOW"
      }
    },
    {
      "type": "rules",
      "id": "RTM-002",
      "attributes": {
        "enabled": true,
        "exceptions": {
          "tags": [],
          "resources": []
        },
        "extraSettings": [
          {
            "name": "ttl",
            "type": "ttl",
            "value": 72,
            "ttl": true
          }
        ],
        "riskLevel": "MEDIUM"
      }
    }
  ],
  "data": {
    "type": "profiles",
    "id": {profile-id},
    "attributes": {
      "name": "Test-Profile-1",
      "description": "A test description for a profile."
    },
    "relationships": {
      "ruleSettings": {
        "data": [
          {
            "type": "rules",
            "id": "EC2-001"
          },
          {
            "type": "rules",
            "id": "RTM-002"
          }
        ]
      }
    }
  }
}' \
https://us-west-2-api.cloudconformity.com/v1/profiles/
```

Example Response:

```
{
  "included": [
    {
      "type": "rules",
      "id": "EC2-001",
      "attributes": {
        "enabled": false,
        "exceptions": {
          "tags": ["TestUpdateTags"],
          "resources": []
        },
        "extraSettings": [],
        "riskLevel": "LOW"
      }
    },
    {
      "type": "rules",
      "id": "RTM-002",
      "attributes": {
        "enabled": true,
        "exceptions": {
          "tags": [],
          "resources": []
        },
        "extraSettings": [
          {
            "name": "ttl",
            "type": "ttl",
            "value": 72,
            "ttl": true
          }
        ],
        "riskLevel": "MEDIUM"
      }
    }
  ],
  "data": {
    "type": "profiles",
    "id": {profile-id},
    "attributes": {
      "name": "Test-Profile-1",
      "description": "A test profile with rule settings."
    },
    "relationships": {
      "ruleSettings": {
        "data": [
          {
            "type": "rules",
            "id": "EC2-001"
          },
          {
            "type": "rules",
            "id": "RTM-002"
          }
        ]
      }
    }
  }
}
```
