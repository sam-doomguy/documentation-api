Managing users.

### User Privileges

There are 4 possible Cloud Conformity roles. Each role grants different levels of access via the api. The roles are:

- **organisation admin**
- **organisation user with full access to account**
- **organisation user with read-only access to account**
- **organisation user with no access to account**

User access to each endpoint is listed below:

| Endpoint                                                    | admin | full access user | read-only user | no access user |
| ----------------------------------------------------------- | :---: | :--------------: | :------------: | :------------: |
| GET /api-keys _(get a list of your api keys)_               |   Y   |        Y         |       Y        |       Y        |
| GET /api-keys/id _(get details about an api key)_           |   Y   |        Y         |       Y        |       Y        |
| POST /accounts _(create a new account)_                     |   Y   |        N         |       N        |       N        |
| GET /accounts _(get a list of accounts you have access to)_ |   Y   |        Y         |       Y        |       Y        |
| GET /accounts/id                                            |   Y   |        Y         |       Y        |       N        |
| POST /accounts/id/scan _(run the conformity bot)_           |   Y   |        Y         |       N        |       N        |
| PATCH /accounts/id/subscription                             |   Y   |        N         |       N        |       N        |
| PATCH /accounts/id                                          |   Y   |        Y         |       N        |       N        |
| GET /accounts/id/settings/rules/ruleId                      |   Y   |        Y         |       Y        |       N        |
| PATCH /accounts/id/settings/rules/ruleId                    |   Y   |        Y         |       N        |       N        |
| GET /accounts/id/settings/rules                             |   Y   |        Y         |       Y        |       N        |
| PATCH /accounts/id/settings/rules                           |   Y   |        Y         |       N        |       N        |
| GET /checks \*                                              |   Y   |        Y         |       Y        |       N        |
| POST /checks                                                |   Y   |        Y         |       N        |       N        |
| DELETE /checks/id                                           |   Y   |        Y         |       N        |       N        |
| GET /events \*\*\*                                          |   Y   |        Y         |       Y        |       N        |
| POST /external-ids                                          |   Y   |        N         |       N        |       N        |
| GET /groups                                                 |   Y   |        Y         |       Y        |       N        |
| POST /groups                                                |   Y   |        N         |       N        |       N        |
| PATCH /groups                                               |   Y   |        N         |       N        |       N        |
| DELETE /groups                                              |   Y   |        N         |       N        |       N        |
| GET /resources                                              |   Y   |        Y         |       N        |       N        |
| GET /settings/communication/accountId \*\*                  |   Y   |        Y         |       Y        |       N        |
| POST /settings/communication \*\*                           |   Y   |        Y         |       N        |       N        |
| PATCH /settings/communication/settingId \*\*                |   Y   |        Y         |       N        |       N        |
| DELETE /settings/settingId \*\*                             |   Y   |        Y         |       N        |       N        |
| GET /users/whoami                                           |   Y   |        Y         |       Y        |       Y        |
| GET /users/id                                               |   Y   |        Y         |       Y        |       Y        |
| GET /users                                                  |   Y   |        N         |       N        |       N        |
| POST /users                                                 |   Y   |        N         |       N        |       N        |
| POST /users/sso                                             |   Y   |        N         |       N        |       N        |
| PATCH /users/id                                             |   Y   |        N         |       N        |       N        |
| DELETE /users/id                                            |   Y   |        N         |       N        |       N        |

- The response will depend on the AccountIds added to the query parameter. For example, if a user has no access to an account and they add that account to the AccountIds array, an error will be thrown.

\*\* User role will limit the amount of data they can GET or POST/PATCH. For more information, consult the [Settings ReadMe](./Settings.md#).

\*\*\* If user role is ADMIN, organisation-level events will also be returned.
