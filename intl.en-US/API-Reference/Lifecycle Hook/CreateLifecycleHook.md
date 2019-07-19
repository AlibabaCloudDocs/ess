# CreateLifecycleHook {#doc_api_1163691 .reference}

You can call this operation to create lifecycle hooks for a scaling group \(CreateLifecycleHook\).

## Description {#description .section}

Each scaling group can have a maximum of six lifecycle hooks. Lifecycle hooks enable instances in a scaling group to remain in a wait state for a finite period of time during a scale-in or scale-out event. You can adjust this time by configuring the `HeartbeatTimeout` parameter. The instances remain in a wait state for a specified period of time, and then the scaling group continues the scale-in or scale-out process. While the instances are in the wait state, scaling activities are not performed until they are manually continued or until the wait period times out. During a scale-out process, ECS instances enter the wait state after their IP addresses are added to the whitelist of a specified ApsaraDB for RDS instance. When the wait state ends, the IP addresses will be added to a specified SLB instance. During a scale-in process, ECS instances enter the wait state after their IP addresses are removed from the whitelist of an SLB instance. When the wait state ends, the IP addresses will be removed from the whitelist of an ApsaraDB for RDS instance. The procedure is as follows. We recommend that you use an Alibaba Cloud Message Service \(MNS\) queue or topic to receive notifications about when ECS instances are started or released.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=CreateLifecycleHook) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|LifecycleTransition|String|Yes|SCALE\_OUT| The type of scaling activity to which lifecycle hooks apply. Valid values:

 -   SCALE\_OUT: scale-out event
-   SCALE\_IN: scale-in event

 |
|ScalingGroupId|String|Yes|AG6CQdPU8OKdwLjgZcJ\*\*\*\*| The ID of the scaling group.

 |
|Action|String|No|CreateLifecycleHook| The operation that you want to perform. Set the value to CreateLifecycleHook.

 |
|DefaultResult|String|No|CONTINUE| The action that the scaling group takes when the lifecycle hook times out. Valid values:

 -   CONTINUE: The scaling group continues the scale-in or scale-out process.
-   ABANDON: The scaling group stops any remaining actions of the scale-in or scale-out event.

 Default value: CONTINUE.

 During a scale-in event \(`SCALE_IN`\), if the scaling group has multiple lifecycle hooks and one of them is terminated by the `DefaultResult=ABANDON` parameter, the remaining lifecycle hooks in the same scaling group are also terminated. Otherwise, the scaling activity will proceed normally after the wait period expires and continue with the action specified in the DefaultResult parameter.

 |
|HeartbeatTimeout|Integer|No|600| The time that can elapse before the lifecycle hook times out. If the lifecycle hook times out, the scaling group performs the default action \(DefaultResult\). Valid values: 30 to 21600. Unit: seconds. Default value: 600. You can prevent the lifecycle hook from timing out by calling the [RecordLifecycleActionHeartbeat](~~73846~~) operation. You can also terminate the lifecycle action by calling the [CompleteLifecycleAction](~~73847~~) operation.

 |
|LifecycleHook.N.DefaultResult|String|No|CONTINUE| The action that the scaling group takes when the lifecycle hook times out. Valid values:

 -   CONTINUE: The scaling group continues the scale-in or scale-out process.
-   ABANDON: The scaling group stops any remaining actions of the scale-in or scale-out event.

 Default value: CONTINUE.

 During a scale-in event \(`SCALE_IN`\), if the scaling group has multiple lifecycle hooks and one of them is terminated by the `DefaultResult=ABANDON` parameter, the remaining lifecycle hooks in the same scaling group are also terminated. Otherwise, the scaling activity will proceed normally after the wait period expires and continue with the action specified in the DefaultResult parameter.

 |
|LifecycleHook.N.HeartbeatTimeout|Integer|No|600| The time that can elapse before the lifecycle hook times out. If the lifecycle hook times out, the scaling group performs the default action \(DefaultResult\). Valid values: 30 to 21600. Unit: seconds. Default value: 600. You can prevent the lifecycle hook from timing out by calling the [RecordLifecycleActionHeartbeat](~~73846~~) operation. You can also terminate the lifecycle action by calling the [CompleteLifecycleAction](~~73847~~) operation.

 |
|LifecycleHook.N.LifecycleHookName|String|No|TESTSCALE\_OUT| The name of the lifecycle hook. Each lifecycle hook name must be unique within a scaling group. The name must be 2 to 40 characters in length and can contain letters, digits, and special characters including underscores \(\_\), hyphens \(-\), and periods \(.\). The default name is the ID of the lifecycle hook.

 |
|LifecycleHook.N.LifecycleTransition|String|No|SCALE\_OUT| The type of scaling activity to which lifecycle hooks apply. Valid values:

 -   SCALE\_OUT: scale-out event
-   SCALE\_IN: scale-in event

 |
|LifecycleHook.N.NotificationArn|String|No|acs:ess:cn-hangzhou:1111111111:queue/queue1| The Alibaba Cloud Resource Name \(ARN\) of the notification target that Auto Scaling uses to notify you when an instance is in the transition state for a lifecycle hook. This target can be either an MNS queue or an MNS topic. The format of the parameter value is acs:ess:\{region\}:\{account-id\}:\{resource-relative-id\}.

 -   `region:`the region where the scaling group is located.
-   `account-id:`the ID of the Alibaba Cloud account.

 Example:

 -   MNS queue: acs:ess:\{region\}:\{account-id\}:queue/\{queuename\}
-   MNS topic: acs:ess:\{region\}:\{account-id\}:topic/\{topicname\}

 |
|LifecycleHook.N.NotificationMetadata|String|No|Test| The fixed string that you want to include when Auto Scaling sends a message about the wait state of a scaling activity to the notification target. The parameter value can be up to 128 characters in length. Auto Scaling sends the specified `NotificationMetadata` parameter value along with the notification message so that you can easily categorize notifications. After you set the `NotificationArn` parameter, the `NotificationMetadata` parameter takes effect.

 |
|LifecycleHookName|String|No|TESTSCALE\_OUT| The name of the lifecycle hook. Each lifecycle hook name must be unique within a scaling group. The name must be 2 to 40 characters in length and can contain letters, digits, and special characters including underscores \(\_\), hyphens \(-\), and periods \(.\). The default name is the ID of the lifecycle hook.

 |
|NotificationArn|String|No|acs:ess:cn-hangzhou:1111111111:queue/queue1| The Alibaba Cloud Resource Name \(ARN\) of the notification target that Auto Scaling uses to notify you when an instance is in the transition state for the lifecycle hook. This target can be either an MNS queue or an MNS topic. The format of the parameter value is acs:ess:\{region\}:\{account-id\}:\{resource-relative-id\}.

 -   `region:`the region where the scaling group is located.
-   `account-id:`the ID of the Alibaba Cloud account.

 Example:

 -   MNS queue: acs:ess:\{region\}:\{account-id\}:queue/\{queuename\}
-   MNS topic: acs:ess:\{region\}:\{account-id\}:topic/\{topicname\}

 |
|NotificationMetadata|String|No|Test| The fixed string that you want to include when Auto Scaling sends a message about the wait state of the scaling activity to the notification target. The parameter value can be up to 128 characters in length. Auto Scaling sends the specified `NotificationMetadata` parameter value along with the notification message so that you can easily categorize notifications. After you set the `NotificationArn` parameter, the `NotificationMetadata` parameter takes effect.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|LifecycleHookId|String|ash-\*\*\*\*| The ID of the lifecycle hook.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=CreateLifecycleHook
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ**** 
&LifecycleHookName=TESTSCALE_OUT
&LifecycleTransition=SCALE_OUT
&NotificationArn=acs:ess:cn-hangzhou:1111111111:queue/queue1 
&NotificationMetadata=Test
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CreateLifecycleHookResponse> 
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
  <LifecycleHookId>ash-****</LifecycleHookId>
</CreateLifecycleHookResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"LifecycleHookId":"ash-****",
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes {#section_m0m_uc8_xye .section}

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

 | The error message returned when the specified parameter value is invalid.

 |
| 400

 | InvalidNotificationArn

 | The specified parameter notificationArn is invalid.

 | The error message returned when the specified value of the NotificationArn parameter is invalid.

 |
| 400

 | UnsupportedNotificationType.CurrentRegion

 | The notificationType is not supported in the special region which scalingGroup belongs to.

 | The error message returned when the specified notification type is not supported in the region.

 |
| 400

 | QueueNotExist

 | The specified queue does not exist.

 | The error message returned when the specified MNS queue does not exist.

 |
| 400

 | TopicNotExist

 | The specified topic does not exist.

 | The error message returned when the specified MNS topic does not exist.

 |
| 400

 | InvalidLifecycleHookName.Duplicate

 | The specified value of parameter lifecycleHookName is duplicated.

 | The error message returned when the specified value of the LifecycleHookName parameter already exists.

 |
| 400

 | QuotaExceeded.LifecycleHook

 | Lifecycle hook quota exceeded in the specified scaling group.

 | The error message returned when the number of lifecycle hooks in the specified scaling group reaches the upper limit.

 |

