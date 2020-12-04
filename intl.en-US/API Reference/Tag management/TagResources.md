# TagResources

You can call this operation to create and bind tags to specified Auto Scaling resources.

## Description

-   A maximum of 20 tags can be bound for a scaling group.
-   Before you bind a tag to a resource, Alibaba Cloud checks the number of existing tags that are bound to the resource. An error message is returned if the maximum number is reached.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=TagResources&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|TagResources|The operation that you want to perform. Set the value to TagResources. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the resource. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ResourceId.N|RepeatList|Yes|asg-bp17xb4x1vr29lgt\*\*\*\*|The ID of resource N. Valid values of N: 1 to 50. |
|ResourceType|String|Yes|scalinggroup|The type of the resource. Only scaling groups are supported. Set the value to scalinggroup. |
|Tag.N.Key|String|No|TestKey|The key of tag N of the resource. Valid values of N: 1 to 20. The tag key cannot be an empty string. It can be up to 128 characters in length and cannot start with acs: or aliyun. It cannot contain http:// or https://. |
|Tag.N.Value|String|No|TestValue|The value of tag N of the resource. Valid values of N: 1 to 20. The tag value can be an empty string. It can be up to 128 characters in length and cannot start with acs: or aliyun. It cannot contain http:// or https://. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|74C4E313-8570-479F-8791-DC25360D5627|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=TagResources
&RegionId=cn-hangzhou
&ResourceId.1=asg-bp17xb4x1vr29lgt****
&ResourceId.2=asg-bp12qqpsd8bzra3t****
&ResourceType=scalinggroup
&<Common request parameters>
```

Sample success responses

`XML` format

```
<TagResourcesResponse>
    <RequestId>74C4E313-8570-479F-8791-DC25360D5627</RequestId>
</TagResourcesResponse>
```

`JSON` format

```
{
    "RequestId": "74C4E313-8570-479F-8791-DC25360D5627"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

