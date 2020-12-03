Managing Conformity reports.

### User Privileges

There are 4 possible Cloud Conformity roles. Each role grants different levels of access via the api. The roles are:

- **administrator**
- **power user**
- **read-only**
- **custom**

Users with **custom** role are managed manually by the **administrator** and can be given the following permissions:

- **full access to an account/s**
- **read-only access to an account/s**
- **no access to an account/s**

User access to each endpoint is listed below:

| Endpoint                                                   | administrator | power user | read-only | custom - full | custom - read only | custom - no access |
| ---------------------------------------------------------- | ------------- | ---------- | --------- | ------------- | ------------------ | ------------------ |
| GET /reports _(get a list reports)_                        | Y             | Y          | Y         | Y             | Y                  | N                  |
| GET /reports/reportId/entityId/type _(downloads a report)_ | Y             | Y          | Y         | Y             | Y                  | N                  |
