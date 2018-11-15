# Remove an ECS instance {#concept_25955_zh .concept}

Removes an ECS instance from a specified scaling group.

## Description {#section_pdw_1bl_sfb .section}

-   When the ECS instance automatically created by the Auto Scaling service is removed from the scaling group, the ECS instance is disabled and released.
-   When the manually attached ECS instance is removed from the scaling group, the ECS instance is neither disabled nor released.
-   The interface can be called only when the scaling group is active.
-   The interface can be called only when no scaling activity in the scaling group is in progress.
-   When no scaling activity in the scaling group is in progress, the interface can be directly executed without cooldown.
-   Successfully calling this interface only means that the Auto Scaling service has accepted the call request, and the scaling activity can be executed, but does not necessarily mean that the scaling activity can be successfully executed. You can use the returned ScalingActivityId to check the status of the scaling activity.
-   When the total capacity of instances of the scaling group minus instances specified by this interface is smaller than than MinSize, the call fails.

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|Operation interface name, required parameter. Value: RemoveInstances.|
|ScalingGroupId|String|Yes|Scaling group ID.|
|InstanceId.N|String|Yes|ECS instance ID. You can input up to 20 IDs.|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|ScalingActivityId|String|Scaling activity ID|

## Error codes { .section}

For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|Error message|Error code|Description|HTTP status code|
|:------------|:---------|:----------|:---------------|
|The specified scaling group does not exist in this account.|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|404|
|The specified ECS instance does not exist in the scaling group.|InvalidInstanceId.NotFound|Instance "XXX" does not exist.|404|
|API is not fully authorized to the Auto Scaling service.|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|403|
|The specified scaling group is not active.|IncorrectScalingGroupStatus|The current status of the specified scaling group does not support this action.|400|
|The specified scaling group has an in-progress scaling activity.|ScalingActivityInProgress|You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress for the specified scaling group.|400|
|The Server Load Balancer instance in the scaling group to which the scaling rule belongs is not active.|IncorrectLoadBalancerStatus|The current status of the specified load balancer does not support this action.|400|
|The RDS instance in the scaling group to which the specified scaling rule belongs is not running.|IncorrectDBInstanceStatus|The current status of DB instance "XXX" does not support this action.|400|
|After instance removal, the total capacity is lower than MinSize.|IncorrectCapacity.MinSize|To remove the instances, the total capacity will be lesser than the MinSize.|400|

## Request example { .section}

```
http://ess.aliyuncs.com/?Action=RemoveInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&InstanceId. 1=i-28wt48iaa
&<Public Request Parameters>
```

## Response example { .section}

XML format:

```
<RemoveInstancesResponse>
    <ScalingActivityId>bybj9OcaOT4ucPMbFhcqHfA3</ScalingActivityId>
    <RequestId>DD0309B7-2613-4792-9B86-275906695253</RequestId>
</RemoveInstancesResponse>
```

JSON format:

```
"RequestId": "6469DCD0-13AC-487E-85A0-CE4922908FDE",
"ScalingActivityId": "ebta5WbUzC8gcwUWvfchyT4U"
```

