# CreateNotificationConfiguration {#doc_api_Ess_CreateNotificationConfiguration .reference}

You can call this operation to configure notifications of Auto Scaling events and resource changes.

You can configure the event notification function to send notifications to CloudMonitor system events, MNS queues, or MNS topics. When a scaling event or resource change of a specified type occurs in a scaling group, Auto Scaling sends notifications to CloudMonitor or MNS. You cannot use MNS queues or MNS topics in several Alibaba Cloud regions. For more information, see MNS FAQ or visit the MNS console.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=CreateNotificationConfiguration) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|NotificationArn|String|Yes|acs:ess:cn-hangzhou:123456:cloudmonitor|The Alibaba Cloud Resource Name \(ARN\) for the notification object. The format is `acs:ess:{region}:{account-id}:{resource-relative-id}`.

 -   `region`: the ID of the region where the scaling group resides. For more information, see [Regions and zones](~~40654~~).
-   `account-id`: the ID of your account.
-   `resource-relative-id`: the notification method. Valid values: `cloudmonitor`, `queue/{queuename}`, and `topic/{topicname}`.

 |
|NotificationType.N|RepeatList|Yes|AUTOSCALING:SCALE\_OUT\_SUCCESS|The number of types of Auto Scaling events and resource changes. Valid values of N: 1 to 8. Multiple event types are listed in a column.

 You can also call [DescribeNotificationTypes](~~71117~~) to query the parameter values.

 |
|ScalingGroupId|String|Yes|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|The ID of the scaling group.

 |
|Action|String|No|CreateNotificationConfiguration|The operation that you want to perform. Set the value to CreateNotificationConfiguration.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=CreateNotificationConfiguration
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ**** 
&NotificationArn=acs:ess:cn-hangzhou:123456:cloudmonitor 
&NotificationType. 1=AUTOSCALING:SCALE_OUT_SUCCESS
&NotificationType. 2=AUTOSCALING:SCALE_IN_SUCCESS
&NotificationType. 3=AUTOSCALING:SCALE_OUT_ERROR
&NotificationType. 4=AUTOSCALING:SCALE_IN_ERROR
&NotificationType. 5=AUTOSCALING:SCALE_REJECT
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CreateNotificationConfigurationResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</CreateNotificationConfigurationResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"requestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
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
|400

|InvalidNotificationArn

|The specified parameter notificationArn is invalid.

|The error message returned when the specified notification ARN is invalid.

|
|400

|InvalidNotificationTypes

|The specified notificationType is invalid.

|The error message returned when a specified notification type is invalid.

|
|400

|NotificationConfigurationExist

|The specified notificationConfiguration already exist for the scalingGroup.

|The error message returned when the specified event notification function is already configured for the current scaling group.

|
|400

|NotificationConfigurationQuotaExceed.ForScalingGroup

|NotificationConfiguration num exceed for the specified scalingGroup.

|The error message returned when the number of event types set for the scaling group reaches the upper limit.

|
|400

|QueueNotExist

|The specified queue queuename does not exist.

|The error message returned when the specified MNS queue does not exist.

|
|400

|TopicNotExist

|The specified topic topicname does not exist.

|The error message returned when the specified MNS topic does not exist.

|
|400

|UnsupportedNotificationType.CurrentRegion

|The notificationType is not supported in the special region which scalingGroup belongs to.

|The error message returned when the notification type is not supported in the region where the scaling group resides.

|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned when the specified scaling group does not exist.

|

