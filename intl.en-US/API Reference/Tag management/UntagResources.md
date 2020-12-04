# UntagResources

You can call this operation to unbind tags from the specified Auto Scaling resources. After a tag is unbound, the tag is automatically deleted if it is not bound to any other resources.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=UntagResources&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UntagResources|The operation that you want to perform. Set the value to UntagResources. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the resource. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ResourceId.N|RepeatList|Yes|asg-bp17xb4x1vr29lgt\*\*\*\*|The ID of resource N. Valid values of N: 1 to 50. |
|ResourceType|String|Yes|scalinggroup|The type of the resource. Only scaling groups are supported. Set the value to scalinggroup. |
|TagKey.N|RepeatList|No|TestKey|The key of tag N of the resource. Valid values of N: 1 to 20. |
|All|Boolean|No|false|Specifies whether to unbind all tags from the resource. This parameter takes effect only when the TagKey.N parameter is not specified. Valid values:

 -   true: All tags are unbound from the resource.
-   false: No tags are unbound.

 Default value: false |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|3AEBB1B9-5B13-4311-951F-C3C7FA2B73ED|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=UntagResources
&RegionId=cn-hangzhou
&ResourceType=scalinggroup
&ResourceId.1=asg-bp17xb4x1vr29lgt****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UntagResourcesResponse>
      <RequestId>3AEBB1B9-5B13-4311-951F-C3C7FA2B73ED</RequestId>
</UntagResourcesResponse>
```

`JSON` format

```
{
	"RequestId": "3AEBB1B9-5B13-4311-951F-C3C7FA2B73ED"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

