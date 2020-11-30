A `GET` request to this endpoint allows you to get rule settings for all configured rules of the specified account.

If a rule has never been configured, it will not show up in the resulting data.
For example, even if our bots run rule `RDS-018` for your account hourly, if you have never configured it, it will not be part of the data body we send back.

This endpoint only returns configured rules. If you want to include default rule settings, set `includeDefaults=true` in query parameters.

Details of rule setting types used by Cloud Conformity are available [here](#fix-me)
