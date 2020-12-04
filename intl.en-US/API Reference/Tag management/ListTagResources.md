# ListTagResources

You can call this operation to query the tags that are bound to one or more Auto Scaling resources.

## Description

-   Set ResourceId.N or set Tag.N that consists of Tag.N.Key and Tag.N.Value in the request to specify query objects.
-   If you set Tag.N and ResourceId.N at the same time, the Auto Scaling resources that match both the parameters are returned.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=ListTagResources&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListTagResources|The operation that you want to perform. Set the value to ListTagResources. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the resource. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ResourceType|String|Yes|scalinggroup|The type of the resource. Only scaling groups are supported. Set the value to scalinggroup. |
|ResourceId.N|RepeatList|No|asg-bp17xb4x1vr29lgt\*\*\*\*|The ID of resource N. Valid values of N: 1 to 50. |
|Tag.N.Key|String|No|TestKey|The key of tag N. It is used for exact match of Auto Scaling resources. The key must be 1 to 128 characters in length. Valid values of N: 1 to 20.

Tag.N is used for exact match of Auto Scaling resources to which the specified tags are bound and consists of one key-value pair.

-   If you specify only Tag.N.Key, all Auto Scaling resources whose tags contain the specified tag key are returned.
-   If you specify only Tag.N.Value, the MissingParameter.TagKey error code is returned.
-   If you specify multiple tag key-value pairs at the same time, only Auto Scaling resources that match all tag key-value pairs are returned. |
|Tag.N.Value|String|No|TestValue|The value of tag N. It is used for exact match of Auto Scaling resources. The value must be 1 to 128 characters in length. Valid values of N: 1 to 20. |
|NextToken|String|No|caeba0bbb2be03f84eb48b699f0a4883|The token that is used to start the next query. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NextToken|String|caeba0bbb2be03f84eb48b699f0a4883|The token that is used to start the next query. |
|RequestId|String|DE65F6B7-7566-4802-9007-96F2494AC5XX|The ID of the request. |
|TagResources|Array of TagResource| |A collection of resources and tags, including the resource ID, resource type, and tag key-value pair. |
|TagResource| | | |
|ResourceId|String|asg-bp17xb4x1vr29lgt\*\*\*\*|The ID of the resource. |
|ResourceType|String|ALIYUN::ESS::SCALINGGROUP|The type of the resource. |
|TagKey|String|TestKey|The key of the tag. |
|TagValue|String|TestValue|The value of the tag. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=ListTagResources
&RegionId=cn-hangzhou
&ResourceType=scalinggroup
&ResourceId.1=asg-bp17xb4x1vr29lgt****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListTagResourcesResponse>
      <RequestId>6E79F465-6101-4071-A852-19B76E238717</RequestId>
      <NextToken></NextToken>
      <TagResources>
            <TagResource>
                  <ResourceId>asg-bp17xb4x1vr29lgt****</ResourceId>
                  <TagKey>TestKey</TagKey>
                  <ResourceType>ALIYUN::ESS::SCALINGGROUP</ResourceType>
                  <TagValue>TestValue</TagValue>
            </TagResource>
      </TagResources> 
</ListTagResourcesResponse>
```

`JSON` format

```
{
    "RequestId": "6E79F465-6101-4071-A852-19B76E238717",
    "NextToken": "",
    "TagResources": {
        "TagResource": [
            {
                "ResourceId": "asg-bp17xb4x1vr29lgt****",
                "TagKey": "TestKey",
                "ResourceType": "ALIYUN::ESS::SCALINGGROUP",
                "TagValue": "TestValue"
            }
        ]
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

