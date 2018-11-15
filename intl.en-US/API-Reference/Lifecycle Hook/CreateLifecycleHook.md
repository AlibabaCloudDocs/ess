# CreateLifecycleHook {#concept_73839_zh .concept}

Create lifecycle hooks for a scaling group \(`CreateLifecycleHook`\).

## Description {#section_nkw_rml_sfb .section}

Each scaling group can have up to six lifecycle hooks. Lifecycle hooks enable scaling groups to remain in a wait state for a finite period of time during a scale-in or scale-out event. You can adjust this time by configuring the `HeartbeatTimeout` parameter.

A default period of time is specified before a scaling group scales in or out the number of ECS instances. While an ECS instance is in wait state, you can initialize the configuration of the ECS instance or retrieve data of the ECS instance. During a scale-out process, the ECS instance enters a wait state after IP addresses are added to the whitelist of a specified Relational Database Service \(RDS\) instance. When the wait state ends, IP addresses will be added to a specified Server Load Balancer \(SLB\) instance. During a scale-in process, the ECS instance enters a wait state after IP addresses are removed from the whitelist of an SLB instance. When the wait state ends, IP addresses will be removed from the whitelist of an RDS instance. The procedure is as follows.

-   A scale-out event:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40660/154227706132073_en-US.png)

-   A scale-in event:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40660/154227706232072_en-US.png)


We recommend that you use an Alibaba Cloud Message Service \(MNS\) queue or topic to receive notifications about when ECS instances are launched or terminated.

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: CreateLifecycleHook|
|ScalingGroupId|String|Yes|The ID of the scaling group|
|LifecycleHookName|String|No|The name of the lifecycle hook. Each name must be unique within a scaling group. The name must be 2 to 40 characters in length and can contain letters, numbers, Chinese characters, and special characters including underscores \(\_\), hyphens \(-\) and periods \(.\).Default value: Lifecycle Hook ID

|
|LifecycleTransition|String|Yes|The scaling activities to which lifecycle hooks apply Valid values:-   SCALE\_OUT: scale-out event
-   SCALE\_IN: scale-in event

|
|HeartbeatTimeout|Integer|No|The time, in seconds, that can elapse before the lifecycle hook times out. If the lifecycle hook times out, the scaling group performs the default action \(DefaultResult\). The range is from 30 to 21,600 seconds. The default value is 600 seconds. You can prevent the lifecycle hook from timing out by calling the [RecordLifecycleActionHeartbeat](reseller.en-US/API-Reference/Lifecycle Hook/RecordLifecycleActionHeartbeat.md#) API. You can also terminate the lifecycle action by calling the [CompleteLifecycleAction](reseller.en-US/API-Reference/Lifecycle Hook/CompleteLifecycleAction.md#) API.|
|DefaultResult|String|No|The action that the scaling group takes when the lifecycle hook times out. Value range:-   CONTINUE: the scaling group continues with the scale-in or scale-out process.
-   ABANDON: the scaling group stops any remaining action of the scale-in or scale-out event.

Default value: CONTINUE

If the scaling group has multiple lifecycle hooks and one of them is terminated by the `DefaultResult=ABANDON` parameter during a scale-in event \(`SCALE_IN`\), the remaining lifecycle hooks under the same scaling group will also be terminated. Otherwise, the action following the wait state is the next action, as specified in the parameter DefaultResult, after the last lifecycle event under the same scaling group.

|
|NotificationArn|String|No|The Alibaba Cloud Resource Name \(ARN\) of the notification target that Auto Scaling will use to notify you when an instance is in the transition state for the lifecycle hook. This target can be either an MNS queue or an MNS topic. The format of the parameter value is acs:ess:\{region\}:\{account-id\}:\{resource-relative-id\}.-   `region`: the region to which the scaling group locates
-   `account-id`: Alibaba Cloud ID

For example:

-   MNS queue: acs:ess:\{region\}:\{account-id\}:queue/\{queuename\}
-   MNS topic: acs:ess:\{region\}:\{account-id\}:topic/\{topicname\}

|
|NotificationMetadata|String|No|The fixed string that you want to include when Auto Scaling sends a message about the wait state of the scaling activity to the notification target. The length of the parameter can be up to 128 characters. Auto Scaling will send the specified `NotificationMetadata` parameter along with the notification message so that you can easily categorize your notifications The `NotificationMetadata` parameter will only take effect after you specify the `NotificationArn` parameter.|

## Response parameters { .section}

|Name|Type|Required|
|:---|:---|:-------|
|RequestId|String|The request ID|
|LifecycleHookId|String|The lifecycle hook ID|

## Request example { .section}

```
http://ess.aliyuncs.com/?Action=CreateLifecycleHook
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&LifecycleHookName=TESTSCALE_OUT
&LifecycleTransition=SCALE_OUT
&NotificationArn=acs:ess:cn-hangzhou:1111111111:queue/queue1
&NotificationMetadata=Test
&<Public request parameter>
```

## Response example { .section}

XML format:

```
<CreateLifecycleHookResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
    <LifecycleHookId>ash-xxxxxxxxxxxxxxxxx</LifecycleHookId>
</CreateLifecycleHookResponse>
```

JSON format:

```
{
    "requestId": "04F0F334-1335-436C-A1D7-6C044FE73368",
    "lifecycleHookId": "ash-xxxxxxxxxxxxxxxxx"
}
```

## Error codes { .section}

Error codes that are specific to this interface are as follows. For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|Error code|Error message|HTTP status code|Description|
|:---------|:------------|:---------------|:----------|
|InvalidParamter|The specified value of parameter is not valid.|400|The specified value of the parameter is invalid.|
|InvalidNotificationArn|The specified parameter notificationArn is invalid.|400|The specified value of the parameter `NotificationArn` is invalid.|
|UnsupportedNotificationType.CurrentRegion|The notificationType is not supported in the special region which scalingGroup belongs to.|400|The type of notification that is supported depends on the region to which the scaling group belongs.|
|QueueNotExist|The specified queue does not exist.|400|The specified MNS queue does not exist.|
|TopicNotExist|The specified topic does not exist.|400|The specified MNS topic does not exist.|
|InvalidLifecycleHookName.Duplicate|The specified value of parameter lifecycleHookName is duplicated.|400|The specified value of the parameter LifecycleHookName already exists.|
|QuotaExceeded.LifecycleHook|Lifecycle hook quota exceeded in the specified scaling group.|400|Each scaling group can have up to six lifecycle hooks.|

