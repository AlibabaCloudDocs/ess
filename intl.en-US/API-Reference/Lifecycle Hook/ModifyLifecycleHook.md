# ModifyLifecycleHook {#concept_73844_zh .concept}

Modify the property of a lifecycle hook \(`ModifyLifecycleHook`\).

You can modify the property of a lifecycle hook using either of the following methods:

-   Specify the parameter `LifecycleHookId`. `ScalingGroupId` and `LifecycleHookName` are ignored.
-   Specify the parameters `ScalingGroupId` and `LifecycleHookName`.

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: ModifyLifecycleHook|
|LifecycleHookId|String|No|The ID of the lifecycle hook|
|ScalingGroupId|String|No|The ID of the scaling group|
|LifecycleHookName|String|No|The name of the lifecycle hook. Each name must be unique within a scaling group. The name must 2 to 40 characters in length and can contain letters, numbers, Chinese characters, and special characters including underscores \(\_\), hyphens \(-\), and periods \(.\).|
|LifecycleTransition|String|No|The scaling activities to which the lifecycle hooks apply Value range:-   SCALE\_OUT: scale-out event
-   SCALE\_IN: scale-in event

|
|HeartbeatTimeout|Integer|No|The time, in seconds, that can elapse before the lifecycle hook times out. If the lifecycle hook times out, the scaling group performs the default action \(DefaultResult\). The range is from 30 to 21,600 seconds. The default is 600 seconds. You can prevent the lifecycle hook from timing out by calling the [RecordLifecycleActionHeartbeat](reseller.en-US/API-Reference/Lifecycle Hook/RecordLifecycleActionHeartbeat.md#) API. You can also terminate the lifecycle action by calling the [CompleteLifecycleAction](reseller.en-US/API-Reference/Lifecycle Hook/CompleteLifecycleAction.md#) API.|
|DefaultResult|String|No|The action that the scaling group takes when the lifecycle hook times out Value range:-   CONTINUE: the scaling group continues with the scale-in or scale-out process.
-   ABANDON: the scaling group stops any remaining action of the scale-in or scale-out event.

Default value: CONTINUE

If the scaling group has multiple lifecycle hooks and one of them is terminated by the `DefaultResult=ABANDON` parameter during a scale-in event \(`SCALE_IN`\), the remaining lifecycle hooks under the same scaling group will also stop working. Otherwise, the action following the wait state is the next action, as specified in the parameter DefaultResult, after the last lifecycle event under the same scaling group.

|
|NotificationArn|String|No|The Alibaba Cloud Resource Name \(ARN\) of the notification target that Auto Scaling will use to notify you when an instance is in the transition state for the lifecycle hook. This target can be either an MNS queue or an MNS topic. The format of the parameter value is acs:ess:\{region\}:\{account-id\}:\{resource-relative-id\}.-   `region`: the region to which the scaling group belongs
-   `account-id`: Alibaba Cloud ID

For example:

-   MNS queue: acs:ess:\{region\}:\{account-id\}:queue/\{queuename\}
-   MNS topic: acs:ess:\{region\}:\{account-id\}:topic/\{topicname\}

|
|NotificationMetadata|String|No|The fixed string that you want to include when Auto Scaling sends a message about the wait state of the scaling activity to the notification target. The length of the parameter can be up to 128 characters. Auto Scaling will send the specified `NotificationMetadata` parameter along with the notification message so that you can easily categorize your notifications. The `NotificationMetadata` parameter only takes effect after you specify the `NotificationArn` parameter.|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|RequestId|String|The Request ID|

## Request example { .section}

```
http://ess.aliyuncs.com/?Action=ModifyLifecycleHook
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&LifecycleHookName=testSCALE_IN
&LifecycleTransition=SCALE_IN
&DefaultResult=ABANDON
&NotificationArn=acs:ess:cn-hangzhou:1111111111:queue/queue2
&NotificationMetadata=Test
&<Public request parameter>
```

## Response example { .section}

XML format:

```
<ModifyLifecycleHookResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyLifecycleHookResponse>
```

JSON format:

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## Error codes { .section}

Error codes that are specific to this interface are as follows. For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|Error code|Error message|HTTP status code|Description|
|:---------|:------------|:---------------|:----------|
|InvalidParamter|The specified value of parameter is not valid.|400|The specified value of the parameter is invalid.|
|InvalidLifecycleHookId.NotExist|The specified lifecycleHookId not exist.|400|The specified `LifecycleHookId` does not exist.|
|InvalidLifecycleHookName.NotExist|The specified lifecycleHookName you provided not exist.|400|The specified `LifecycleHookName` does not exist.|
|InvalidNotificationArn|The specified parameter notificationArn is invalid.|400|The specified `NotificationArn` does not exist.|
|UnsupportedNotificationType.CurrentRegion|The notificationType is not supported in the special region which scalingGroup belongs to.|400|The type of notification that is supported depends on the region to which the scaling group belongs.|
|LifecycleHook|The specified queue does not exist.|400|The specified MNS queue does not exist.|
|TopicNotExist|The specified topic does not exist.|400|The specified MNS topic does not exist.|

