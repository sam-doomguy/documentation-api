This endpoint allows a user to get the details of the specified communication setting.

**Important**: Users with different roles can get different results from this endpoint.

The table below describes the relationship between user role or account access level, and type of data the user can get for account level settings.

| **Role / access to account**   | **Account-Level Settings**       |
| ------------------------------ | -------------------------------- |
| ADMIN                          | Full settings with configuration |
| FULL access to the account     | Full settings with configuration |
| READONLY access to the account | Settings without configuration   |
| NO access to the account       | No settings                      |

For organisation level settings, the ADMIN users are the only users who can access those settings. The table below describes the relationship between user role and type of the data user can get for organisation level settings.

| **Role**                       | **Organisation-Level Settings**  |
| ------------------------------ | -------------------------------- |
| ADMIN                          | Full settings with configuration |
| FULL access to the account     | Full settings with configuration |
| READONLY access to the account | Settings without configuration   |
| NO access to the account       | No settings                      |
