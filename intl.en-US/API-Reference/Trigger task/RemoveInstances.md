# RemoveInstances {#doc_api_Ess_RemoveInstances .reference}

You can call this operation to remove an ECS instance from a specified scaling group.

## Description {#description .section}

-   When an automatically created ECS instance is removed from a scaling group, the instance is stopped and released.
-   When a manually attached ECS instance is removed from a scaling group, the instance is not stopped or released.
-   The operation can be called only when the scaling group is in the **Active** state.
-   The operation can be called only when the scaling group does not have any scaling activities in progress.
-   If the scaling group does not have any scaling activities in progress, the operation can be immediately executed without the need to wait for the cooldown period to expire.
-   When this operation is called, Auto Scaling has received the request. However, it is not guaranteed that the scaling activity can be executed as intended. You can determine the status of the scaling activity based on the returned ScalingActivityId parameter value.
-   When the number of ECS instances to be removed would leave the number of ECS instances in the specified scaling group smaller than MinSize, the operation fails.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=RemoveInstances) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|InstanceId.N|RepeatList|Yes|i-28wt4\*\*\*\*|The IDs of ECS instances. You can enter a maximum of 20 IDs.

 |
|ScalingGroupId|String|Yes|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|The ID of the scaling group.

 |
|Action|String|No|RemoveInstances|The operation that you want to perform. Set the value to RemoveInstances.

 |
|RemovePolicy|String|No|release|Indicates the policy used to remove an instance. Valid values:

 -   recycle: indicates that the instance is stopped and then removed.

**Note:** This value can be used only when the **ScalingPolicy** parameter is set to recycle.

-   release: indicates that the instance is released and then removed.

 Default value: release.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |
|ScalingActivityId|String|bybj9OcaOT4ucPMbFhcq\*\*\*\*|The ID of the scaling activity.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=RemoveInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ**** 
&InstanceId. 1=i-28wt4****
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<RemoveInstancesResponse> 
  <ScalingActivityId>bybj9OcaOT4ucPMbFhcqHfA3</ScalingActivityId> 
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</RemoveInstancesResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Ess)

|HTTP status code

|Error code

|Error message

|Description

|
|------------------|------------|---------------|-------------|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned when the specified scaling group does not exist in the current account.

|
|404

|InvalidInstanceId.NotFound

|Instance "XXX" does not exist.

|The error message returned when the specified ECS instance does not exist in the scaling group.

|
|400

|InvalidParameter

|The specified group does not support the specified RemovePolicy.

|The error message returned when the specified scaling group does not support the specified value of the RemovePolicy parameter.

|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned when Auto Scaling is not authorized to call the specified operation.

|
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|The error message returned when the specified scaling group is not active.

|
|400

|ScalingActivityInProgress

|You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress for the specified scaling group.

|The error message returned when the specified scaling group currently has a scaling activity in progress.

|
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|The error message returned when an SLB instance for the scaling group to which the specified scaling rule belongs is not active.

|
|400

|IncorrectDBInstanceStatus

|The current status of DB instance "XXX" does not support this action.

|The error message returned when an ApsaraDB for RDS instance for the scaling group to which the specified scaling rule belongs is not running.

|
|400

|IncorrectCapacity.MinSize

|To remove the instances, the total capacity will be lesser than the MinSize.

|The error message when the number of ECS instances to be removed would leave the number of ECS instances in the specified scaling group smaller than MinSize.

|

