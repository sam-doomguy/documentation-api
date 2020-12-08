This endpoint is used to create a custom checks. You may pass one check or an array of checks in the JSON body.

**IMPORTANT:**
&nbsp;&nbsp;&nbsp;Some guidelines about using this endpoint:

1. Checks are created as long as your inputs are valid. The onus is on you to ensure the checks you enter are meaningful and useful.
2. Each check object you enter will require a `check.relationships.account`. If you provide an account which you don't have WRITE access to, the check will not be saved.
3. Check Ids are constructed from the parameters entered and follow the format:
   1. **ccc:accountId:ruleId:service:region:resourceId**
   2. If you add a check with the same `accountId`, `ruleId`, `service`, `region`, AND `resourceId` as another existing check in the database, this new check WILL write over the existing check.
   3. Since resource is an optional attribute, checks entered without resource will not have the `resourceId` part of the check Id.
