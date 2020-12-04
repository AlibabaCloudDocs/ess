# ListTagValues

You can call this operation to query the tag values of Auto Scaling tag keys.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=ListTagValues&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListTagValues|The operation that you want to perform. Set the value to ListTagValues. |
|Key|String|Yes|ESS|The key of the tag. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the Auto Scaling resource. |
|ResourceType|String|Yes|scalinggroup|The type of the Auto Scaling resource. Set the value to scalinggroup, which indicates that the tag is bound to a scaling group. |
|NextToken|String|No|caeba0bbb2be03f84eb48b699f0a\*\*\*\*|The token that is used to start the next query. If the NextToken parameter is empty, no subsequent requests are sent. |
|PageSize|Integer|No|10|The number of entries to return on each page. Valid values: 1 to 50.

Default value: 10 |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NextToken|String|caeba0bbb2be03f84eb48b699f0a\*\*\*\*|The token that is used to start the next query. If the NextToken parameter is empty, no subsequent requests are sent. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|AB444F46-1CFF-4B06-B8F0-B45D3158F95B|The ID of the request. |
|Values|List|Doc|The information of the tag values. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=ListTagValues
&RegionId=cn-hangzhou
&ResourceType=scalinggroup
&Key=ESS
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListTagValuesResponse>
    <RequestId>178E635A-11AF-4214-A65E-50B67B3CA548</RequestId>
    <NextToken></NextToken>
    <PageSize>1</PageSize>
    <Values>
        <Value>Doc</Value>
    </Values>
</ListTagValuesResponse>
```

`JSON` format

```
{
    "RequestId": "178E635A-11AF-4214-A65E-50B67B3CA548",
    "NextToken": "",
    "PageSize": 1,
    "Values": {
        "Value": [
            "Doc"
        ]
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HTTP sta

|Error code

|Error message

|Description |
|----------|------------|---------------|-------------|
|400

|InvalidResourceType.NotFound

|The ResourceType provided does not exist in our records.

|The error message returned because the specified the ResourceType parameter is invalid. |
|400

|InvalidTagKey.Malformed

|The specified tag key \\"%s\\" is not valid.

|The error message returned because the specified Tag.N.Key parameter does not exist. |

