# RemoveInstances

You can call this operation to remove one or more ECS instances from a scaling group.

## Description

Before you call this operation, make sure that the following conditions are met:

-   The scaling group is in the Active state.
-   The scaling group does not have any scaling activities in progress.

If no scaling activity is being executed in the scaling group, this operation can trigger scaling activities immediately without waiting for the cooldown time to expire.

If an ECS instance is automatically created by Auto Scaling, or is manually added to a scaling group and managed by Auto Scaling, the ECS instance enters the No Fees for Stopped Instances \(VPC-Connected\) state or is released when the instance is removed from the scaling group.

If an ECS instance is manually added to a scaling group and is not managed by Auto Scaling, the ECS instance is not stopped or is released when the instance is removed from the scaling group.

If the call is successful, Auto Scaling has accepted the request. However, this does not mean that the scaling activity will succeed. You can determine the status of a scaling activity based on the return value of the ScalingActivityId parameter.

When the difference between the number of existing ECS instances in the scaling group \(total capacity\) and the number of ECS instances to be removed is less than the MinSize value, the call fails.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=RemoveInstances&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RemoveInstances|The operation that you want to perform. Set the value to RemoveInstances. |
|InstanceId.N|RepeatList|Yes|i-28wt4\*\*\*\*|The ID of ECS instance N to be removed. Valid values of N: 1 to 20. |
|ScalingGroupId|String|Yes|asg-bp18p2yfxow2dloq\*\*\*\*|The ID of the scaling group. |
|RemovePolicy|String|No|release|The action to be performed when the ECS instance is removed. Valid values:

 -   recycle: The ECS instance enters the No Fees for Stopped Instances \(VPC-Connected\) state.

**Note:** The value takes effect only when the ScalingPolicy parameter is set to recycle.

-   release: The ECS instance is released.

 The ScalingPolicy parameter of CreateScalingGroup specifies the reclaim mode of the scaling group, but the action to be performed when ECS instances are removed is determined by the RemovePolicy parameter of RemoveInstances. Examples:

 -   If both ScalingPolicy and RemovePolicy are set to recycle, the ECS instance enters the No Fees for Stopped Instances \(VPC-Connected\) state when it is removed.
-   If ScalingPolicy is set to recycle and RemovePolicy is set to release, the ECS instance is released when it is removed.
-   If ScalingPolicy is set to release and RemovePolicy is set to recycle, the ECS instance is released when it is removed.
-   If both ScalingPolicy and RemovePolicy are set to release, the ECS instance is released when it is removed.

 Default value: release. |
|DecreaseDesiredCapacity|Boolean|No|true|Specifies whether to modify the expected number of ECS instances in the scaling group. Valid values:

 -   true: After ECS instances are removed from a scaling group, the expected number of ECS instances in the scaling group decreases accordingly.
-   false: After ECS instances are removed from a scaling group, the expected number of instances in the scaling group remains unchanged.

 Default value: true. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|ScalingActivityId|String|asa-bp175o6f6ego3r2j\*\*\*\*|The ID of the scaling activity. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=RemoveInstances
&ScalingGroupId=asg-bp18p2yfxow2dloq****
&InstanceId.1=i-28wt4****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RemoveInstancesResponse>
      <ScalingActivityId>asa-bp175o6f6ego3r2j****</ScalingActivityId>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</RemoveInstancesResponse>
```

`JSON` format

```
{
    "ScalingActivityId":"asa-bp175o6f6ego3r2j****",
    "RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HttpCode

|Error code

|Error message

|Description |
|----------|------------|---------------|-------------|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist in the current account. |
|404

|InvalidInstanceId.NotFound

|Instance "XXX" does not exist.

|The error message returned because the specified ECS instance does not exist in the scaling group. |
|400

|InvalidParameter

|The specified group does not support the specified RemovePolicy.

|The error message returned because the specified scaling group does not support the specified value of the RemovePolicy parameter. |
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned because Auto Scaling is not authorized to call the specified operation. |
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|The error message returned because the specified scaling group is not in the Active state. |
|400

|ScalingActivityInProgress

|You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress for the specified scaling group.

|The error message returned because the specified scaling group has a scaling activity in progress. |
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|The error message returned because the specified Server Load Balancer \(SLB\) instance associated with the scaling group to which the specified scaling rule belongs is not in the Active state. |
|400

|IncorrectDBInstanceStatus

|The current status of DB instance "XXX" does not support this action.

|The error message returned because the specified ApsaraDB RDS instance of the scaling group to which the specified scaling rule belongs is not in the Running state. |
|400

|IncorrectCapacity.MinSize

|To remove the instances, the total capacity will be lesser than the MinSize.

|The error message returned because the number of ECS instances to be removed will leave the number of ECS instances in the specified scaling group less than the MinSize value. |

