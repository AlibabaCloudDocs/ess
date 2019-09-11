# AttachInstances {#doc_api_Ess_AttachInstances .reference}

You can call this operation to add an ECS instance to a scaling group.

## Description {#description .section}

The restrictions on ECS instances to be added are as follows:

-   The ECS instances and the scaling group must be in the same region.
-   The ECS instances must be running.
-   The ECS instances have not been added to any scaling group.
-   The ECS instances support subscription and pay-as-you-go billing methods.
-   If the VSwitchId parameter is specified for a scaling group, ECS instances that belong to a classic network or in different VPCs cannot be added to the scaling group.
-   If the VSwitchId parameter is not specified for a scaling group, ECS instances that belong to a VPC cannot be added to the scaling group.

    This operation can only be called when the scaling group is active.


This operation can only be called when the scaling group does not have any scaling activities in progress.

If the scaling group does not have any scaling activities in progress, the operation can be immediately executed without waiting for the cooldown period to expire.

If the call is successful, it indicates that Auto Scaling has accepted the request. However, this does not mean that the scaling activity will succeed. You can determine the status of the scaling activity based on the returned value of the ScalingActivityId parameter.

If the sum of the number of instances to be added specified by this operation and the number of ECS instances currently in the scaling group is greater than the MaxSize value, the call fails.

Manually added ECS instances are not associated with the active scaling configuration of the scaling group.

## Debugging {#api_explorer .section}

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=AttachInstances&type=RPC&version=2014-08-28)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|ScalingGroupId|String|Yes|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|The ID of the scaling group.

 |
|InstanceId.1|String|Yes|i-28wt4\*\*\*\*|The ID of ECS instance N to be added. Valid values of N: 1 to 20.

 |
|Action|String|No|AttachInstances|The operation that you want to perform. Set the value to AttachInstances.

 |
|LoadBalancerWeight.1|Integer|No|50|The weight of ECS backend server N. Valid values of N: 1 to 20. Valid values for this parameter: 0 to 100.

 Default value: 50.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request.

 |
|ScalingActivityId|String|bybj9OcaOT4ucPMbFhcq\*\*\*\*|The ID of the scaling activity.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=AttachInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&InstanceId.1=i-28wt4****
&<Common request parameters>

```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
<AttachInstancesResponse>
      <ScalingActivityId>bybj9OcaOT4ucPMbFhcqHfA3</ScalingActivityId>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</AttachInstancesResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"ScalingActivityId":"bybj9OcaOT4ucPMbFhcq****"
}
```

## Error codes { .section}

|HTTP status code

|Error code

|Error message

|Description

|
|------------------|------------|---------------|-------------|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist in the current account.

|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned because Auto Scaling is not authorized to call the specified operation.

|
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|The error message returned because the specified scaling group is not active.

|
|404

|InvalidInstanceId.NotFound

|Instance "XXX" does not exist.

|The error message returned because the specified ECS instance does not exist in the current account.

|
|400

|InvalidInstanceId. RegionMismatch

|Instance "XXX" and the specified scaling group are not in the same Region.

|The error message returned because the specified ECS instance and the scaling group are not in the same region.

|
|400

|InvalidInstanceId.InstanceTypeMismatch

|Instance "XXX" and existing active scaling configurations have different instance types.

|The error message returned because the type of the specified ECS instance is different from that in the active scaling configuration.

|
|400

|IncorrectInstanceStatus

|The current status of instance "XXX" does not support this action.

|The error message returned because the specified ECS instance is not running.

|
|400

|InvalidInstanceId. NetworkTypeMismatch

|The network type of instance "XXX" does not support this action.

|The error message returned because the network type of the specified ECS instance is different from that of the scaling group.

|
|400

|InvalidInstanceId.VPCMismatch

|Instance "XXX" and the specified scaling group are not in the same VPC.

|The error message returned because the added ECS instance and the specified scaling group are not in the same VPC.

|
|400

|InvalidInstanceId.InUse

|Instance "XXX" is already attached to another scaling group.

|The error message returned because the specified ECS instance is already added to another scaling group.

|
|400

|ScalingActivityInProgress

|You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress for the specified scaling group.

|The error message returned because the specified scaling group has scaling activities in progress.

|
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|The error message returned because the SLB instance associated with the specified scaling group is not active.

|
|400

|IncorrectLoadBalancerHealthCheck

|The current health check type of specified load balancer does not support this action.

|The error message returned because health check is not enabled for the SLB instance associated with the specified scaling group.

|
|400

|InvalidLoadBalancerId.IncorrectInstanceNetworkType

|The network type of the instance in specified load balancer does not support this action.

|The error message returned because the network type of the ECS instance attached to the specified SLB instance is different from that of the scaling group.

|
|400

|InvalidLoadBalancerId.VPCMismatch

|The specified virtual switch and the instance in specified load balancer are not in the same VPC.

|The error message returned because the ECS instance attached to the specified SLB instance is not in the same VPC as the VSwitch specified by VSwitchID.

|
|400

|IncorrectDBInstanceStatus

|The current status of DB instance "XXX" does not support this action.

|The error message returned because the RDS instance in the specified scaling group is not running.

|
|400

|QuotaExceeded.DBInstanceSecurityIP

|Security IP quota exceeded in DB instance "XXX".

|The error message returned because the number of IP addresses in the specified RDS instance whitelist reaches the upper limit.

|
|400

|QuotaExceeded.SecurityGroupInstance

|Instance quota exceeded in the specified security group.

|The error message returned because the number of ECS instances in the specified security group reaches the upper limit.

|
|400

|IncorrectCapacity.MaxSize

|To attach the instances, the total capacity will be greater than the MaxSize.

|The error message returned because the total number of ECS instances \(Total Capacity\) exceeds the specified value of MaxSize after ECS instances are added to the specified scaling group.

|

