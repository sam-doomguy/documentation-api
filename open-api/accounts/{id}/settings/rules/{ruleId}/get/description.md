A `GET` request to this endpoint allows you to get configured rule setting for the specified rule Id of the specified account.

If a specific rule has never been configured, the request will result in a `404` error.

For example, even if our bots run rule `RDS-018` for your account hourly, if you have never configured it, trying to get rule settings for `RDS-018` will result in a `404` error.
