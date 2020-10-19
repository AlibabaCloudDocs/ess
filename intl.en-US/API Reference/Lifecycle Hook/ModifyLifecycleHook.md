# ModifyLifecycleHook

You can call this operation to modify the properties of a lifecycle hook.

## Description

You can use one of the following methods to specify the lifecycle hook to be modified:

-   Specify the lifecycle hook ID by using the LifecycleHookId parameter. Then, the scaling group ID specified by ScalingGroupId and the lifecycle hook name specified by LifecycleHookName will be ignored.
-   Specify the scaling group ID by using the ScalingGroupId parameter and the lifecycle hook name by using the LifecycleHookName parameter.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=ModifyLifecycleHook&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyLifecycleHook|The operation that you want to perform. Set the value to ModifyLifecycleHook. |
|LifecycleHookId|String|No|ash-bp1fxuqyi98w0aib\*\*\*\*|The ID of the lifecycle hook that you want to modify. |
|ScalingGroupId|String|No|asg-bp18p2yfxow2dloq\*\*\*\*|The ID of the scaling group to which the lifecycle hook belongs. |
|LifecycleHookName|String|No|test\_SCALE\_IN|The name of the lifecycle hook that you want to modify. |
|DefaultResult|String|No|CONTINUE|The action that the scaling group takes when the lifecycle hook times out. Valid values:

-   CONTINUE: The scaling group continues to respond to a scale-in or scale-out event.
-   ABANDON: The scaling group releases the created ECS instances if the scaling activity type is scale-out or removes the ECS instances to be scaled in if the scaling activity type is scale-in.

If a scaling group has multiple lifecycle hooks and one of them is terminated when the DefaultResult parameter is set to ABANDON during a scale-in event, the remaining lifecycle hooks in the same scaling group are also terminated. Otherwise, the scaling activity will proceed normally after the lifecycle hook times out and continue with the action specified by the DefaultResult parameter. |
|HeartbeatTimeout|Integer|No|600|The wait period before the lifecycle hook times out. When the lifecycle hook times out, the scaling group performs the default action. Valid values: 30 to 21600. Unit: seconds.

You can call the [RecordLifecycleActionHeartbeat](~~73846~~) operation to extend the timeout period and keep the instance in the wait state. You can also call the [CompleteLifecycleAction](~~73847~~) operation to terminate the wait state of a scaling activity. |
|LifecycleTransition|String|No|SCALE\_IN|The type of scaling activities to which the lifecycle hook applies. Valid values:

-   SCALE\_OUT: scale-out events of the scaling group
-   SCALE\_IN: scale-in events of the scaling group |
|NotificationMetadata|String|No|Test|The fixed string to include when Auto Scaling sends a notification about the wait state of a scaling activity. The parameter value cannot exceed 4,096 characters in length.

Auto Scaling sends the specified NotificationMetadata parameter value along with the notification message so that you can categorize your notifications. The NotificationMetadata parameter is valid only after you set the NotificationArn parameter. |
|NotificationArn|String|No|acs:mns:cn-beijing:161456884340\*\*\*\*:queue/modifyLifecycleHo\*\*\*\*|The Alibaba Cloud Resource Name \(ARN\) of the notification object that Auto Scaling uses to notify you when ECS instances are put into the wait state by the lifecycle hook. The following list describes the formats of this parameter:

-   When the notification method is set to MNS queue, the format of this parameter is acs:mns:\{region-id\}:\{account-id\}:queue/\{queuename\}.
-   When the notification method is set to MNS topic, the format of this parameter is acs:mns:\{region-id\}:\{account-id\}:topic/\{topicname\}.
-   When the notification method is set to Operation Orchestration Service \(OOS\) template, the format of this parameter is acs:oos:\{region-id\}:\{account-id\}:template/\{templatename\}.

The variables in the preceding parameter formats have the following meanings:

-   region-id: the region ID of the scaling group
-   account-id: the ID of the Alibaba Cloud account
-   queuename: the name of the MNS queue
-   topicname: the name of the MNS topic
-   templatename: the name of the OOS template |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=ModifyLifecycleHook
&ScalingGroupId=asg-bp18p2yfxow2dloq****
&LifecycleHookName=test_SCALE_IN
&LifecycleTransition=SCALE_IN
&DefaultResult=ABANDON
&NotificationArn=acs:mns:cn-beijing:161456884340****:queue/modifyLifecycleHo****    
&NotificationMetadata=Test
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyLifecycleHookResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyLifecycleHookResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
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

|InvalidLifecycleHookId.NotExist

|The specified lifecycleHookId not exist.

|The error message returned because the specified LifecycleHookId parameter does not exist. |
|400

|InvalidLifecycleHookName.NotExist

|The specified lifecycleHookName you provided not exist.

|The error message returned because the specified LifecycleHookName parameter does not exist. |
|400

|InvalidNotificationArn

|The specified parameter NotificationArn is invalid.

|The error message returned because the specified NotificationArn parameter is invalid. |
|400

|UnsupportedNotificationType.CurrentRegion

|The NotificationType is not supported in the special region which scalingGroup belongs to.

|The error message returned because the notification type is not supported in the region to which the scaling group belongs. |
|400

|LifecycleHook

|The specified queue does not exist.

|The error message returned because the specified MNS queue does not exist. |
|400

|TopicNotExist

|The specified topic does not exist.

|The error message returned because the specified MNS topic does not exist. |

