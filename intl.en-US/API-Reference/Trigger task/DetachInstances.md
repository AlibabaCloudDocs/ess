# DetachInstances {#concept_72453_zh .concept}

You can call this operation to detach one or more ECS instances from a scaling group.

## Description {#section_qq4_5bl_sfb .section}

After you detach an ECS instance, the ECS instance can exist independently without attaching a scaling group. You can attach the ECS instance to another scaling group \([AttachInstances](reseller.en-US/API-Reference/Trigger task/Attach an ECS instance.md#)\). Detaching an ECS instance will not stop or release the ECS instance. If applicable, you can manually [stop](../../../../../reseller.en-US/API Reference/Instances/StopInstance.md#) or [release](../../../../../reseller.en-US/API Reference/Instances/DeleteInstance.md#) an ECS instance.

**Note:** 

-   The status of the target scaling group must be **Enable** \(`Enable`\).
-   Ensure that no in-progress scaling activity exists in the target scaling group.
-   When no in-progress scaling activity exists in the target scaling group, you can immediately perform the operation without following the [cool-down time](../../../../../reseller.en-US/User Guide/Usage notes/Cool-down time.md#).
-   Successfully calling an operation only means the calling request of the operation is received. You can trigger a scaling activity as usual, but you cannot ensure that the scaling activity is executed. You must view the status of the scaling activity based on the returned result of `ScalingActivityId`.
-   The remaining number of ECS instances cannot be less than the minimum number of the scaling group \(`MinSize`\). The remaining number of ECS instances is the total number of ECS instances of the target scaling group minus the number of detached ECS instances.

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set the value to DetachInstances.|
|ScalingGroupId|String|Yes|The ID of the scaling group.|
|InstanceId.N|String|Yes|The ID of the ECS instance. Valid values of `N`: 1 to 20.|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|RequestId|String|The request ID.|
|ScalingActivityId|String|The ID of the scaling activity.|

## Examples { .section}

Sample requests

```
http://ess.aliyuncs.com/?Action=DetachInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJXXXXX
&InstanceId. 1=i-28wt48iaa
&<Common request parameters>
```

Successful response examples

`XML` format

```
<DetachInstancesResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId> 
    <ScalingActivityId>asa-xxxxxxxxx</ScalingActivityId>
</DetachInstancesResponse> 
```

`JSON` format

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368",
    "ScalingActivityId": "asa-xxxxxxxxx"
}
```

## Error codes { .section}

|HttpCode|Error code|Error message|Description|
|--------|:---------|:------------|:----------|
|400|IncorrectScalingGroupStatus|The current status of the specified scaling group does not support this action.|The status of the target scaling group must be **Enable** `Enable`.|
|400|ScalingActivityInProgress|You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress.|The error message returned when the specified scaling group is currently undergoing a scaling activity.|
|400|IncorrectLoadBalancerStatus|The current status of the specified load balancer does not support this action.|The status of SLB instances in the target scaling group must be **Running**`Running`.|
|400|IncorrectDBInstanceStatus|The current status of DB instance “XXX” does not support this action.|The status of RDS instances in the target scaling group must be **Running**`Running`.|
|400|IncorrectCapacity.MinSize|To remove the instances, the total capacity will be lesser than the MinSize.|The remaining number of ECS instances cannot be less than the minimum number of the scaling group \(`MinSize`\). The remaining number of ECS instances is the total number of ECS instances of the target scaling group minus the number of detached ECS instances.|
|403|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|The error message returned when you have not been authorized to use the `DetachInstances` operation.|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|The error message returned when the specified scaling group does not exist.|
|404|InvalidInstanceId.NotFound|Instance “XXX” does not exist.|The error message returned when the specified ECS instance does not exist.|

