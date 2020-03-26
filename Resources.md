# Cloud Conformity Resources API

Below is a list of the available API calls:

- [Get Excluded Resources](#get-resources-excluded)

## Get Organisation External ID

This endpoint allows you to get the list of excluded resources due to exceptions been configured.

##### Endpoints

`GET /resources/`.

##### Parameters

- `excluded`: true for returning excluded resources (required).
- `accountIds`: A comma-separated list of Cloud Conformity accountIds. If omitted, results will be returned for all accounts the user has access to.
- `page[size]`: Indicates the number of excluded resources that should be returned. The maximum value is 1000 and defaults to 100 if not specified
- `page[number]`: Indicates the page number, defaults to 0
- `filter`: Optional parameter(s).

###### The distinction of excluded resources is based on configured exception on rules. A resource that was excluded could be due to many rules. There is a 10k limit to the maximum number of rules that can be returned. Paging will not work for excluded resources that contain rules higher than this limit. To fetch larger numbers, segment your requests using account and region filtering. On larger accounts, filter requests per account, per region or provider.

##### Filtering

The `filter` query parameter is reserved to be used as the basis for filtering.

For example, the following is a request for a page of excluded resources filtered by cloud provider `AWS`:

```
GET /resources?excluded=true&accountIds=r1gyR4cqg&page[size]=100&page[number]=0&filter[provider]=aws
```

Multiple filter values can be combined in a comma-separated list. For example the following is a request for a page of excluded resources in `us-west-2` or `us-west-1` regions:

```
GET /resources?excluded=true&accountIds=r1gyR4cqg&page[size]=100&page[number]=0&filter[regions]=us-west-1,us-west-2
```

Furthermore, multiple filters can be applied to a single request. For example, the following is a request to get excluded resources for `us-west-2` region when the provider of the resource is `aws`

```
GET /resources?excluded=true&accountIds=r1gyR4cqg&page[size]=100&page[number]=0&filter[regions]=us-west-2&filter[providers]=aws
```

The table below give more information about filter options:

| Name              | Values                                                                                                                                                                                                                                                                                                                                                                                  |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| filter[regions]   | global \| us-east-2 \| us-east-1 \| us-west-1 \| us-west-2 \| ap-south-1 \| ap-northeast-2 \|<br />ap-southeast-1 \| ap-southeast-2 \| ap-northeast-1 \| ca-central-1 \| eu-central-1 \| eu-west-1 \|<br /> eu-west-2 \| sa-east-1 <br /><br />For more information about regions, please refer to [Cloud Conformity Region Endpoint](https://us-west-2.cloudconformity.com/v1/regions) |
| filter[tags]      | Any assigned metadata tags to your resources. Supports partial matching strategy (e.g. `filter[tags]=ERsion::4,AY` will match tags with `Version::4` or `May`)                                                                                                                                                                                                                          |
| filter[providers] | Cloud providers. Accepted values: ["aws" \| "azure"]                                                                                                                                                                                                                                                                                                                                    |

<br />

Example Request:

```
curl -H "Content-Type: application/vnd.api+json" \
-H "Authorization: ApiKey S1YnrbQuWagQS0MvbSchNHDO73XHqdAqH52RxEPGAggOYiXTxrwPfmiTNqQkTq3p" \
https://us-west-2-api.cloudconformity.com/v1/resources?accountIds=r1gyR4cqg&page[size]=100&page[number]=0&filter[regions]=us-west-2&filter[provider]=aws
```

Example Response:

```
{
  "data": [
    {
      "type": "resources",
      "id": "ccrn:aws:DBOIVgown:VPC:ap-south-1:acl-fa816c00",
      "attributes": {
        "account-id": "DBOIVgown",
        "ccrn": "ccrn:aws:DBOIVgown:VPC:ap-south-1:acl-fa816c00",
        "resource": "acl-fa816c91",
        "region": "ap-south-1",
        "descriptor-type": "vpc-networkacl",
        "link": "https://ap-south-1.console.aws.amazon.com/vpc/home?region=ap-south-1#acls:filter=acl-fa816c00",
        "link-title": "acl-fa816c91",
        "resource-name": "VPC Network ACL",
        "tags": [],
        "provider": "aws",
        "exceptions-configured-on-rule": [
          {
            "rule-id": "VPC-010"
          }
        ]
      }
    }
  ]
}
```
