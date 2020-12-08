Cloud Conformity provides Template Scanner capability as a preventative measure to ensure your AWS infrastructure remains compliant by detecting risks in template files before they are launched into AWS.

This API endpoint is suitable for CI/CD pipelines and automation.

This endpoint is used to scan a template file. Currently, CloudFormation template is supported.

### Supported resource types:

- APIGateway
  - RestApi
- CloudFormation
  - Stack
- CloudTrail
  - Trail
- DynamoDB
  - Table
- EC2
  - Instance
  - NatGateway
  - NetworkAcl
  - RouteTable
  - SecurityGroup
  - Subnet
  - VPCEndpoint
- EFS
  - FileSystem
- ELB
  - LoadBalancer
- ELBv2
  - LoadBalancer
- IAM
  - Group
  - ManagedPolicy
  - Role
- Kinesis
  - Stream
- KMS
  - Key
- Lambda
  - Function
- RDS
  - DBCluster
  - DBInstance
- S3Bucket
  - S3Bucket
- SNS
  - Topic
- WorkSpaces
  - WorkSpace

### Supported rules:

All resource level rules are supported.
Refer to [Cloud Conformity rule catalogue](https://us-west-2.cloudconformity.com/v1/services)
for the list of rules.

### Examples:

- [Scan a CloudFormation template using Bash](../../examples/bash/template-scanner/scan.sh)
- [Scan a CloudFormation template using Python](examples/python/template-scanner/scan.py)
