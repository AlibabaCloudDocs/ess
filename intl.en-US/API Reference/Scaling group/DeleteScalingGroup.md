# DeleteScalingGroup

You can call this operation to delete a scaling group.

## Description

When a scaling group is deleted, the scaling configurations, rules, activities, and requests that are associated with the scaling group are also deleted.

The following tasks and instances are not deleted when a scaling group is deleted: scheduled tasks, Cloud Monitor event-triggered tasks, SLB instances, and ApsaraDB RDS instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DeleteScalingGroup&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteScalingGroup|The operation that you want to perform. Set the value to DeleteScalingGroup. |
|ScalingGroupId|String|Yes|asg-bp18p2yfxow2dloq\*\*\*\*|The ID of the scaling group. |
|ForceDelete|Boolean|No|false|Specifies whether to forcibly delete a scaling group and remove and release its ECS instances when ECS instances or ongoing scaling activities exist in the scaling group. Valid values:

-   true: The scaling group is forcibly deleted. First, the scaling group is stopped and new scaling activity requests are rejected. Then, all ECS instances are removed from the scaling group after the ongoing scaling activities are complete. Manually added ECS instances are only removed from the scaling group, whereas instances automatically created by Auto Scaling are deleted. Finally, the scaling group is removed.
-   false: The scaling group is not forcibly deleted. The scaling group is stopped and then deleted when the following conditions are met:
    -   No scaling activities are in process in the scaling group.
    -   The number of ECS instances in the scaling group indicated by the TotalCapacity parameter is 0.

Default value: false. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DeleteScalingGroup
&ScalingGroupId=asg-bp18p2yfxow2dloq****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteScalingGroupResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DeleteScalingGroupResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist in the current account. |
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned because Auto Scaling is not authorized to call the specified operation. |
|400

|InstanceInUse

|You cannot delete a scaling configuration or scaling group while there is an instance associated with it.

|The error message returned because the specified scaling group contains ECS instances. |

