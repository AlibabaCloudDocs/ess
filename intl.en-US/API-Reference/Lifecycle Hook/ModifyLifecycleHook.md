# ModifyLifecycleHook {#doc_api_1163748 .reference}

You can call this operation to modify the properties of a lifecycle hook.

## Description {#description .section}

You can use either of the following methods to modify the properties of a lifecycle hook:

-   Specify the lifecycle hook ID \(`LifecycleHookId`\). This way, you do not need to specify the`ScalingGroupId` or`LifecycleHookName`parameters.
-   Specify the`ScalingGroupId` and`LifecycleHookName`parameters at the same time.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=ModifyLifecycleHook) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|No|ModifyLifecycleHook| The operation that you want to perform. Set the value to ModifyLifecycleHook.

 |
|DefaultResult|String|No|CONTINUE| The action that the scaling group takes when the wait state terminates. Valid values:

 -   CONTINUE: The scaling group continues with the scale-in or scale-out process.
-   ABANDON: The scaling group stops the ongoing scale-in or scale-out event.

 Default value: CONTINUE

 If the scaling group has multiple lifecycle hooks and one of them is terminated by the `SCALE_IN`parameter during a scale-in event \(`DefaultResult=ABANDON`\), the wait states triggered by remaining lifecycle hooks in the same scaling group are also terminated. Otherwise, the action following the wait state is the next action, as specified in the DefaultResult parameter, after the last lifecycle event in the same scaling group.

 |
|HeartbeatTimeout|Integer|No|600| The time that can elapse before the lifecycle hook times out. If the lifecycle hook times out, the scaling group performs the default action \(DefaultResult\). Valid values: 30-21600. Default value: 600. Unit: seconds.

 You can call[RecordLifecycleActionHeartbeat](~~73846~~) to prevent the lifecycle hook from timing out. You can also call[CompleteLifecycleAction](~~73847~~)to terminate the lifecycle action.

 |
|LifecycleHookId|String|No|ash-\*\*\*| The ID of the lifecycle hook. Each ID must be unique within a scaling group. The ID cannot be modified if it is set.

 |
|LifecycleHookName|String|No|hook\_name\_test| The name of the lifecycle hook. Each name must be unique within a scaling group. The name cannot be modified if it is set.

 |
|LifecycleTransition|String|No|SCALE\_IN| The type of the scaling activity to which the lifecycle hook corresponds. Valid values:

 -   SCALE\_OUT: indicates a scale-out event.
-   SCALE\_IN: indicates a scale-in event.

 |
|NotificationArn|String|No|acs:ess:cn-hangzhou:1111111111:queue/queue2| The Alibaba Cloud Resource Name \(ARN\) of the notification object that Auto Scaling uses to notify you when an instance is in the transition state for the lifecycle hook. This object can be either an MNS queue or an MNS topic. The format of the parameter value is acs:ess:\{region\}:\{account-id\}:\{resource-relative-id\}.

 -   `region`: the region where the scaling group resides.
-   `account-id`: the ID of the Alibaba Cloud account.

 Example:

 -   MNS queue: acs:ess:\{region\}:\{account-id\}:queue/\{queuename\}
-   MNS topic: acs:ess:\{region\}:\{account-id\}:topic/\{topicname\}

 |
|NotificationMetadata|String|No|Test| The fixed string that is included in the message that is sent by Auto Scaling about the wait state of a scaling activity to the notification object. The parameter value must be 1 to 128 characters in length. Auto Scaling sends the specified `NotificationMetadata`parameter value along with the notification message so that you can easily categorize your notifications. The`NotificationArn`parameter is applicable only after you set the `NotificationMetadata` parameter.

 |
|ScalingGroupId|String|No|AG6CQdPU8OKdwLjgZcJ2\*\*\*| The ID of the scaling group. Each ID must be unique within a scaling group. The ID cannot be modified if it is set.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=ModifyLifecycleHook
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ**** 
&LifecycleHookName=hook_name_test
&LifecycleTransition=SCALE_IN
&DefaultResult=ABANDON 
&NotificationArn=acs:ess:cn-hangzhou:1111111111:queue/queue2
&NotificationMetadata=Test
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyLifecycleHookResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</ModifyLifecycleHookResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes {#section_tqm_iw0_2fs .section}

[View error codes](https://error-center.aliyun.com/status/product/Ess)

| HTTP status code

 | Error code

 | Error message

 | Description

 |
|--------------------|--------------|-----------------|---------------|
| 400

 | InvalidParamter

 | The specified value of parameter is not valid.

 | The error message returned when the value of the parameter is invalid.

 |
| 400

 | InvalidLifecycleHookId.NotExist

 | The specified lifecycleHookId not exist.

 | The error message returned when the specified lifecycle hook ID does not exist.

 |
| 400

 | InvalidLifecycleHookName.NotExist

 | The specified lifecycleHookName you provided not exist.

 | The error message returned when the specified lifecycle hook name does not exist.

 |
| 400

 | InvalidNotificationArn

 | The specified parameter \*\*notificationArn\*\* is invalid.

 | The error message returned when the specified Alibaba Cloud Resource Name \(ARN\) of the notification object does not exist.

 |
| 400

 | UnsupportedNotificationType.CurrentRegion

 | The \*\*notificationType\*\* is not supported in the special region which scalingGroup belongs to.

 | The error message returned when the notification type is not supported in the region where the scaling group resides.

 |
| 400

 | LifecycleHook

 | The specified queue does not exist.

 | The error message returned when the specified MNS queue does not exist.

 |
| 400

 | TopicNotExist

 | The specified topic does not exist.

 | The error message returned when the specified MNS topic does not exist.

 |

