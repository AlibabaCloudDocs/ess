# AttachInstances

You can call this operation to add ECS instances to a scaling group.

## Description

Before you call this operation, make sure that the following conditions are met:

-   The scaling group is in the Active state.
-   The scaling group does not have scaling activities in progress.

The following limits apply to ECS instances to be added:

-   The instances are located in the same region as the scaling group.
-   The instances are in the Running state.
-   The instances are not added to any other scaling group.
-   The instances use the subscription or pay-as-you-go billing method or are preemptible instances.
-   If the VSwitchId parameter is specified for a scaling group, ECS instances in the classic network or not in the same VPC as the specified vSwitch cannot be added to the scaling group.
-   If the VSwitchId parameter is not specified for a scaling group, VPC-type ECS instances cannot be added to the scaling group.

If the specified scaling group does not have any scaling activities in progress, the operation can immediately trigger scaling activities without waiting for the cooldown period to expire.

If the call is successful, Auto Scaling has accepted the request. However, this does not mean that the scaling activity will succeed. You can determine the status of a scaling activity based on the return value of the ScalingActivityId parameter.

If the sum of the number of ECS instances to be added and the number of existing ECS instances in the scaling group is greater than the MaxSize value, the call fails.

ECS instances manually added by calling the AttachInstances operation are not associated with the active scaling configuration of the scaling group.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=AttachInstances&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AttachInstances|The operation that you want to perform. Set the value to AttachInstances. |
|ScalingGroupId|String|Yes|asg-bp18p2yfxow2dloq\*\*\*\*|The ID of the scaling group. |
|InstanceId.N|RepeatList|No|i-28wt4\*\*\*\*|The ID of ECS instance N to be added. Valid values of N: 1 to 20. |
|LoadBalancerWeight.N|RepeatList|No|50|The weight of ECS instance N as an SLB backend server. Valid values of N: 1 to 20. Valid values of this parameter: 1 to 100.

 Default value: 50. |
|Entrusted|Boolean|No|false|Specifies whether to enable Auto Scaling to manage the lifecycle of ECS instances when you manually add the ECS instances to a scaling group. Valid values:

 -   true: enables Auto Scaling to manage the lifecycle of the instances in the scaling group. The lifecycle of the instances is managed by Auto Scaling and is the same as that of automatically created instances. When the instances are removed from the scaling group, the instances are automatically released. When the instances are removed from the scaling group by using calls to DetachInstances, the instances are not released.
-   false: does not enable Auto Scaling to manage the lifecycle of the instances in the scaling group. After the instances are removed from the scaling group, the instances are not released.

 **Note:** This parameter is not applicable to subscription instances.

 Default value: false. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|ScalingActivityId|String|asa-bp1crxor24s28xf1\*\*\*\*|The ID of the scaling activity. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=AttachInstances
&ScalingGroupId=asg-bp18p2yfxow2dloq****
&InstanceId.1=i-28wt4****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<AttachInstancesResponse>
      <ScalingActivityId>asa-bp1crxor24s28xf1****</ScalingActivityId>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</AttachInstancesResponse>
```

`JSON` format

```
{"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E","ScalingActivityId":"asa-bp1crxor24s28xf1****"}
```

## Error codes

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

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
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned because Auto Scaling is not authorized to call the specified operation. |
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|The error message returned because the specified scaling group is not in the Active state. |
|404

|InvalidInstanceId.NotFound

|Instance “XXX” does not exist.

|The error message returned because the specified ECS instance does not exist in the current account. |
|400

|InvalidInstanceId. RegionMismatch

|Instance “XXX” and the specified scaling group are not in the same Region.

|The error message returned because the specified ECS instance and the scaling group are not in the same region. |
|400

|InvalidInstanceId.InstanceTypeMismatch

|Instance "XXX" and existing Active scaling configurations have different instance types.

|The error message returned because the instance type of the specified ECS instance is different from the instance types specified in the active scaling configuration. |
|400

|IncorrectInstanceStatus

|The current status of instance "XXX" does not support this action.

|The error message returned because the specified ECS instance is not in the Running state. |
|400

|InvalidInstanceId. NetworkTypeMismatch

|The network type of instance “XXX” does not support this action.

|The error message returned because the network type of the specified ECS instance is different from that of the scaling group. |
|400

|InvalidInstanceId.VPCMismatch

|Instance "XXX" and the specified scaling group are not in the same VPC.

|The error message returned because the added ECS instance and the specified scaling group are not in the same VPC. |
|400

|InvalidInstanceId.InUse

|Instance "XXX" is already attached to another scaling group.

|The error message returned because the specified ECS instance is already added to another scaling group. |
|400

|ScalingActivityInProgress

|You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress for the specified scaling group.

|The error message returned because the specified scaling group has scaling activities in progress. |
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|The error message returned because the specified SLB instance associated with the scaling group is not in the Active state. |
|400

|IncorrectLoadBalancerHealthCheck

|The current health check type of specified load balancer does not support this action.

|The error message returned because health check is not enabled for the SLB instance associated with the specified scaling group. |
|400

|InvalidLoadBalancerId.IncorrectInstanceNetworkType

|The network type of the instance in specified load balancer does not support this action.

|The error message returned because the network type of the ECS instances associated with the specified SLB instance is different from that of the scaling group. |
|400

|InvalidLoadBalancerId.VPCMismatch

|he specified virtual switch and the instance in specified load balancer are not in the same VPC.

|The error message returned because the ECS instances associated with the specified SLB instance are not in the same VPC as the vSwitch specified by VSwitchID. |
|400

|IncorrectDBInstanceStatus

|The current status of DB instance “XXX” does not support this action.

|The error message returned because the specified ApsaraDB RDS instance associated with the scaling group is not in the Running state. |
|400

|QuotaExceeded.DBInstanceSecurityIP

|Security IP quota exceeded in DB instance “XXX”.

|The error message returned because the maximum number of IP addresses added to the whitelist of the ApsaraDB RDS instance associated with the specified scaling group has been reached. |
|400

|QuotaExceeded.SecurityGroupInstance

|Instance quota exceeded in the specified security group.

|The error message returned because the maximum number of ECS instances in the specified security group has been reached. |
|400

|IncorrectCapacity.MaxSize

|To attach the instances, the total capacity will be greater than the MaxSize.

|The error message returned because the total number of ECS instances \(total capacity\) exceeds the specified value of MaxSize after ECS instances are added to the specified scaling group. |

