# CreateLifecycleHook

You can call this operation to create one or more lifecycle hooks for a scaling group.

## Description

You can create a maximum of six lifecycle hooks for each scaling group. After a lifecycle hook is created for a scaling group, ECS instances in the scaling group are put into the wait state during scaling activities. You can use the HeartbeatTimeout parameter to specify the timeout period of the lifecycle hook. While an ECS instance is in the wait state, you can perform operations such as downloading data and initializing the configurations of the instance.

During a scale-out event, ECS instances enter the wait state after their IP addresses are added to the whitelist of a specified ApsaraDB for RDS instance. When the wait state ends, the ECS instances will be added to a specified SLB backend server group. During a scale-in event, ECS instances enter the wait state after they are removed from the SLB backend server group. When the wait state ends, their IP addresses are removed from the whitelist of the ApsaraDB for RDS instance.

We recommend that you use an Alibaba Cloud Message Service \(MNS\) queue or topic to create notifications about lifecycle hooks. Then, you can learn when ECS instances are started or released.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=CreateLifecycleHook&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateLifecycleHook|The operation that you want to perform. Set the value to CreateLifecycleHook. |
|LifecycleTransition|String|Yes|SCALE\_OUT|The type of scaling activities to which the lifecycle hook applies. Valid values:

-   SCALE\_OUT: scale-out events of the scaling group
-   SCALE\_IN: scale-in events of the scaling group |
|ScalingGroupId|String|Yes|asg-bp1eyv4qn8ssgv43\*\*\*\*|The ID of the scaling group. |
|LifecycleHookName|String|No|lifecyclehook\*\*\*\*|The name of the lifecycle hook. Each lifecycle hook name must be unique within a scaling group. The name must be 2 to 64 characters in length and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a letter or digit.

The default value is the value of the LifecycleHookId parameter. |
|DefaultResult|String|No|CONTINUE|The action that the scaling group takes when the lifecycle hook times out. Valid values:

-   CONTINUE: The scaling group continues to respond to a scale-in or scale-out event.
-   ABANDON: The scaling group releases the created ECS instances if the scaling activity type is scale-out or removes the ECS instances to be scaled in if the scaling activity type is scale-in.

If a scaling group has multiple lifecycle hooks and one of them is terminated when the DefaultResult parameter is set to ABANDON during a scale-in event, the remaining lifecycle hooks in the same scaling group are also terminated. Otherwise, the scaling activity will proceed normally after the wait period times out and continue with the action specified by the DefaultResult parameter.

Default value: CONTINUE. |
|HeartbeatTimeout|Integer|No|600|The wait period before the lifecycle hook times out. When the lifecycle hook times out, the scaling group performs the default action. Valid values: 30 to 21600. Unit: seconds.

After you create a lifecycle hook, you can call the [RecordLifecycleActionHeartbeat](~~73846~~) operation to extend the timeout period and keep the instance in the wait state. You can also call the [CompleteLifecycleAction](~~73847~~) operation to terminate the wait state of a scaling activity.

Default value: 600. |
|NotificationMetadata|String|No|Test lifecycle hook.|The fixed string to include when Auto Scaling sends a notification about the wait state of a scaling activity. The parameter value cannot exceed 4,096 characters in length.

Auto Scaling sends the specified NotificationMetadata parameter value along with the notification message so that you can categorize your notifications. The NotificationMetadata parameter is valid only after you set the NotificationArn parameter. |
|NotificationArn|String|No|acs:mns:cn-beijing:161456884340\*\*\*\*:queue/modifyLifecycleHo\*\*\*\*|The Alibaba Cloud Resource Name \(ARN\) of the notification object that Auto Scaling uses to notify you when ECS instances are put into the wait state by the lifecycle hook. If you do not set this parameter, Auto Scaling does not send you notifications. If you set this parameter, Auto Scaling sends you notifications of the following types:

-   MNS queue. The format of the parameter value is acs:mns:\{region-id\}:\{account-id\}:queue/\{queuename\}.
-   MNS topic. The format of the parameter value is acs:mns:\{region-id\}:\{account-id\}:topic/\{topicname\}.
-   Operation Orchestration Service \(OOS\) template. The format of the parameter value is acs:oos:\{region-id\}:\{account-id\}:template/\{templatename\}.

The variables in the preceding parameter formats have the following meanings:

-   region-id: the region ID of the scaling group
-   account-id: the ID of Alibaba Cloud account
-   queuename: the name of the MNS queue
-   topicname: the name of the MNS topic
-   templatename: the name of the OOS template |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|LifecycleHookId|String|ash-bp1at9ufhmcf9cmy\*\*\*\*|The ID of the lifecycle hook. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=CreateLifecycleHook
&ScalingGroupId=asg-bp1eyv4qn8ssgv43****
&LifecycleHookName=lifecyclehook****
&LifecycleTransition=SCALE_OUT
&NotificationArn=acs:mns:cn-beijing:161456884340****:queue/modifyLifecycleHo****
&NotificationMetadata=Test lifecycle hook.
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateLifecycleHookResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <LifecycleHookId>ash-bp1at9ufhmcf9cmy****</LifecycleHookId>
</CreateLifecycleHookResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "LifecycleHookId": "ash-bp1at9ufhmcf9cmy****"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|400

|InvalidParamter

|The specified value of parameter is not valid.

|The error message returned because the specified parameter is invalid. |
|400

|InvalidNotificationArn

|The specified parameter notificationArn is invalid.

|The error message returned because the specified NotificationArn parameter is invalid. |
|400

|UnsupportedNotificationType.CurrentRegion

|The notificationType is not supported in the special region which scalingGroup belongs to.

|The error message returned because the notification type is not supported in the region to which the scaling group belongs. |
|400

|QueueNotExist

|The specified queue does not exist.

|The error message returned because the specified MNS queue does not exist. |
|400

|TopicNotExist

|The specified topic does not exist.

|The error message returned because the specified MNS topic does not exist. |
|400

|InvalidLifecycleHookName.Duplicate

|The specified value of parameter lifecycleHookName is duplicated.

|The error message returned because the specified lifecycle hook name already exists. |
|400

|QuotaExceeded.LifecycleHook

|Lifecycle hook quota exceeded in the specified scaling group.

|The error message returned because the number of lifecycle hooks that can be created for a scaling group has exceeded the maximum value of six. |

