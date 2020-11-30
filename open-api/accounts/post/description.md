This endpoint is used to register a new AWS account with Cloud Conformity.

**IMPORTANT:**
&nbsp;&nbsp;&nbsp;In order to register a new AWS account, you need to:

1. Obtain your External ID from [Get Organisation External ID](./ExternalId.md#get-organisation-external-id)
2. Configure your account using CloudFormation automation (**Note:** You need to specify **`ExternalID`** parameter for both options)

   1. Option 1 Launch stack via the console:

      [![API Keys](../../../images/cloudformation-launch-stack.png)](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/review?templateURL=https:%2F%2Fs3-us-west-2.amazonaws.com%2Fcloudconformity%2FCloudConformity.template&stackName=CloudConformity&param_AccountId=717210094962&param_ExternalId=THE_EXTERNAL_ID)

   2. Option 2 via the AWS CLI:
      ```shell script
      aws cloudformation create-stack --stack-name CloudConformity  --region us-east-1  --template-url https://s3-us-west-2.amazonaws.com/cloudconformity/CloudConformity.template --parameters ParameterKey=AccountId,ParameterValue=717210094962 ParameterKey=ExternalId,ParameterValue=THE_EXTERNAL_ID  --capabilities CAPABILITY_NAMED_IAM
      ```

3. Verify stack creation is completed, and then create a new account (see below) with Cloud Conformity using your roleArn and externalId.
