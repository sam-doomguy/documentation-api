Managing Conformity profiles.

### User Privileges

There are 4 possible Cloud Conformity roles. Each role grants different levels of access via the api. The roles are:

- **organisation admin**
- **organisation user with full access to account**
- **organisation user with read-only access to account**
- **organisation user with no access to account**

User access to each endpoint is listed below:

| Endpoint                                                           | admin | full access user | read-only user | no access user |
| ------------------------------------------------------------------ | ----- | ---------------- | -------------- | -------------- |
| GET /profiles _(get a list of profiles)_                           | Y     | N                | N              | N              |
| GET /profiles/id _(get details about a profile and rule settings)_ | Y     | N                | N              | N              |
| POST /profiles _(save a profile and rule settings)_                | Y     | N                | N              | N              |
| PATCH /profiles/id _(update a profile and rule settings)_          | Y     | N                | N              | N              |
| DELETE /profiles/id _(delete a profile and rule settings)_         | Y     | N                | N              | N              |
| POST /profiles/id/apply _(apply a profile to a set of accounts)_   | Y     | N                | N              | N              |

Response will depend on the ProfileId's, Include Settings flag and Types condition added to the query parameter. For example, if a user has no access to a profile and they modify profile details, an error will be thrown. Alternatively, if a user has no access to a profile and they modify rule settings for that profile, an error will be thrown.

| Parameters | Details                                                                                                                          | Value        |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------- | ------------ |
| includes   | This parameter provides the option to include additional information to the profile. Currently, only Rule Settings is supported. | ruleSettings |
