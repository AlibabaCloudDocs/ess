# DetachInstances

You can call this operation to remove one or more ECS instances from a scaling group.

## Description

After ECS instances are removed, the instances are independent of the scaling group. You can call the [AttachInstances](~~25954~~) operation to add the instances to another scaling group.

After you remove an ECS instance by calling the DetachInstances operation, the ECS instance is not stopped or released.

Before you call this operation, make sure that the following conditions are met:

-   The specified scaling group is enabled.
-   The specified scaling group does not have any scaling activities in progress.

If the specified scaling group does not have any scaling activities in progress, the operation can immediately trigger scaling activities without waiting for the cooldown period to expire.

If the call is successful, Auto Scaling has accepted the request. However, this does not mean that the scaling activity will succeed. You can determine the status of a scaling activity based on the return value of the ScalingActivityId parameter.

The difference between the number of existing ECS instances in the specified scaling group and the number of ECS instances to be removed must not be less than the MinSize value.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DetachInstances&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DetachInstances|The operation that you want to perform. Set the value to DetachInstances. |
|InstanceId.N|RepeatList|Yes|i-bp109k5j3dum1ce6\*\*\*\*|The ID of ECS instance N to be removed. Valid values of N: 1 to 20. |
|ScalingGroupId|String|Yes|asg-bp1igpak5ft1flyp\*\*\*\*|The ID of the scaling group. |
|DecreaseDesiredCapacity|Boolean|No|true|Specifies whether to modify the expected number of ECS instances in the scaling group. Valid values:

 -   true: After ECS instances are removed from a scaling group, the expected number of ECS instances in the scaling group decreases accordingly.
-   false: After ECS instances are removed from a scaling group, the expected number of instances in the scaling group remains unchanged.

 Default value: true. |
|DetachOption|String|No|both|Specifies whether to remove the ECS instance from the default server groups and vServer groups of the SLB instances associated with the scaling group, and whether to remove the ECS instance from the whitelists of the ApsaraDB RDS instances associated with the scaling group. After the ECS instance is removed from the default server group and the vServer group of an SLB instance, the ECS instance is no longer used as a backend server of the SLB instance.

 -   Set the value to both. The value specifies to remove the ECS instance from the default sever groups and vServer groups of the associated SLB instances and from the whitelists of the associated ApsaraDB RDS instances. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|ScalingActivityId|String|asa-bp1gbswjhjrw8tko\*\*\*\*|The ID of the scaling activity. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DetachInstances
&ScalingGroupId=asg-bp1igpak5ft1flyp****
&InstanceId.1=i-bp109k5j3dum1ce6****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DetachInstancesResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <ScalingActivityId>asa-bp1gbswjhjrw8tko****</ScalingActivityId>
</DetachInstancesResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "ScalingActivityId": "asa-bp1gbswjhjrw8tko****"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HttpCode

|Error code

|Error message

|Description |
|----------|------------|---------------|-------------|
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|The error message returned because the specified scaling group is not enabled. |
|400

|ScalingActivityInProgress

|You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress for the specified scaling group.

|The error message returned because the specified scaling group has a scaling activity in progress. |
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|The error message returned because the specified SLB instance associated with the scaling group is not in the Active state. |
|400

|IncorrectDBInstanceStatus

|The current status of DB instance “XXX” does not support this action.

|The error message returned because the specified ApsaraDB RDS instance associated with the scaling group is not in the Running state. |
|400

|IncorrectCapacity.MinSize

|To remove the instances, the total capacity will be lesser than the MinSize.

|The error message returned because the number of ECS instances in the scaling group will be less than the MinSize value after the specified number of ECS instances are removed. |
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned because you are not authorized to call this operation. |
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist. |
|404

|InvalidInstanceId.NotFound

|Instance “XXX” does not exist.

|The error message returned because the specified ECS instance does not exist. |

