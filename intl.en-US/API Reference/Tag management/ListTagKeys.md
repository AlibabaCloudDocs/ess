# ListTagKeys

You can call this operation to query the tag keys of Auto Scaling resources.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=ListTagKeys&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListTagKeys|The operation that you want to perform. Set the value to ListTagKeys. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the Auto Scaling resource. |
|ResourceType|String|Yes|scalinggroup|The type of the Auto Scaling resource. Set the value to scalinggroup, which indicates that the tag is bound to a scaling group. |
|NextToken|String|No|caeba0bbb2be03f84eb48b699f0a\*\*\*\*|The token that is used to start the next query. If the NextToken parameter is empty, no subsequent requests are sent. |
|PageSize|Integer|No|10|The number of entries to return on each page. Valid values: 1 to 50.

Default value: 10 |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Keys|List|ESS|The information of the tag keys. |
|NextToken|String|caeba0bbb2be03f84eb48b699f0a\*\*\*\*|The token that is used to start the next query. If the NextToken parameter is empty, no subsequent requests are sent. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|DC09A6AA-2713-4E10-A2E9-E6C5C43A8842|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=ListTagKeys
&RegionId=cn-hangzhou
&ResourceType=scalinggroup
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListTagKeysResponse>
    <RequestId>CA84E8A6-A2BB-41B6-896F-C62987A8BAFE</RequestId>
    <NextToken></NextToken>
    <PageSize>10</PageSize>
    <Keys>
        <Key>ESS</Key>
        <Key>Tag002</Key>
        <Key>Tag001</Key>
    </Keys>
</ListTagKeysResponse>
```

`JSON` format

```
{
    "RequestId": "CA84E8A6-A2BB-41B6-896F-C62987A8BAFE",
    "NextToken": "",
    "PageSize": 10,
    "Keys": {
        "Key": [
            "ESS",
            "Tag002",
            "Tag001"
        ]
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|400

|InvalidResourceType.NotFound

|The ResourceType provided does not exist in our records.

|The error message returned because the specified the ResourceType parameter is invalid. |

