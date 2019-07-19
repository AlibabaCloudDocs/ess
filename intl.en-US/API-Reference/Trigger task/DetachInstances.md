# DetachInstances {#doc_api_Ess_DetachInstances .reference}

You can call this operation to detach one or more ECS instances from a scaling group.

## Description {#description .section}

After an ECS instance is detached, it can either exist independent of any scaling group or be attached to another scaling group. For more information, see [AttachInstances](~~25954~~). Detaching an ECS instance does not stop or release it. You can manually [stop](~~25501~~) or [release](~~25507~~) an ECS instance as needed.

-   The status of the specified scaling group must be **Enable** \(`Enable`\).
-   Ensure that the specified scaling group does not have any scaling activities in progress.
-   If the specified scaling group does not have any scaling activities in progress, the operation can be immediately executed without the need to wait for the [cooldown period](~~25912~~) to expire.
-   If this operation is called, Auto Scaling has received the request. However, it is not guaranteed that the scaling activity can be executed as intended. You can determine the status of the scaling activity based on the returned `ScalingActivityId` parameter value.
-   The difference between the number of ECS instances currently in the specified scaling group and the number of ECS instances to be detached must not be smaller than `MinSize`.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=DetachInstances) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|InstanceId.N|RepeatList|Yes|i-28wt4\*\*\*\*| The IDs of ECS instances. Valid values of N: 1 to 20.

 |
|ScalingGroupId|String|Yes|AG6CQdPU8OKdwLjgZcJ\*\*\*\*| The ID of the scaling group.

 |
|Action|String|No|DetachInstances| The operation that you want to perform. Set the value to DetachInstances.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |
|ScalingActivityId|String|asa-\*\*\*\*| The ID of the scaling activity.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DetachInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&InstanceId. 1=i-28wt4****
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DetachInstancesResponse> 
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
  <ScalingActivityId>asa-xxxxxxxxx</ScalingActivityId> 
</DetachInstancesResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"ScalingActivityId":"asa-****"
}
```

## Error codes {#section_fbv_1z7_40h .section}

[View error codes](https://error-center.aliyun.com/status/product/Ess)

| HTTP status code

 | Error code

 | Error message

 | Description

 |
|--------------------|--------------|-----------------|---------------|
| 400

 | IncorrectScalingGroupStatus

 | The current status of the specified scaling group does not support this action.

 | The error message returned when the specified scaling group is not enabled.

 |
| 400

 | ScalingActivityInProgress

 | You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress for the specified scaling group.

 | The error message returned when the specified scaling group currently has a scaling activity in progress.

 |
| 400

 | IncorrectLoadBalancerStatus

 | The current status of the specified load balancer does not support this action.

 | The error message returned when an SLB instance for the specified scaling group is not active.

 |
| 400

 | IncorrectDBInstanceStatus

 | The current status of DB instance “XXX” does not support this action.

 | The error message returned when an ApsaraDB for RDS instance for the specified scaling group is not running.

 |
| 400

 | IncorrectCapacity.MinSize

 | To remove the instances, the total capacity will be lesser than the MinSize.

 | The error message returned when the number of ECS instances to be detached would leave the number of ECS instances in the specified scaling group smaller than MinSize.

 |
| 403

 | Forbidden.Unauthorized

 | A required authorization for the specified action is not supplied.

 | The error message returned when you are not authorized to use the DetachInstances operation.

 |
| 404

 | InvalidScalingGroupId.NotFound

 | The specified scaling group does not exist.

 | The error message returned when the specified scaling group does not exist.

 |
| 404

 | InvalidInstanceId.NotFound

 | Instance “XXX” does not exist.

 | The error message returned when the specified ECS instance does not exist.

 |

