# CreateNotificationConfiguration {#concept_71114_zh .concept}

You can call this operation to create scaling events and resource change notifications \(`CreateNotificationConfiguration`\).

## Description {#section_kyv_sjl_lgb .section}

You can receive notifications by using CloudMonitor, MNS queues, or MNS topics. When a scaling event or resource change with the specified type occurs in a scaling group, Auto Scaling will send notifications to CloudMonitor or MNS.

Currently, you cannot use MNS queues and MNS topics in several Alibaba Cloud regions. For more information, visit the [MNS console](https://partners-intl.console.aliyun.com/#/mns).

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set the value to CreateNotificationConfiguration.|
|ScalingGroupId|String|Yes|The ID of the scaling group.|
|NotificationArn|String|Yes|The identifier for the notification object. The format is: `acs:ess:{region}:{account-id}:{resource-relative-id}`. -   The `region` is the ID of the region where the scaling group is located. For more information, see [Regions and Zones](../../../../../reseller.en-US/General Reference/Regions and Zones.md#).
-   The `account-id` is the account ID.
-   The `resource-relative-id` is the notification method. Valid values: `cloudmonitor` \(system events of CloudMonitor\), `queue/{queuename}` \(MNS queues\), and `topic/{topicname}` \(MNS topics\).

|
|NotificationType.N|String|Yes|One or more types of scaling events and resource change notifications. Valid values of `N`: 1 to 8. Multiple values are organized in an ordered list.You can call the [DescribeNotificationTypes](reseller.en-US/API-Reference/Event notification/DescribeNotificationTypes.md#) operation to query parameter values.

|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|RequestId|String|The request ID.|

## Examples { .section}

Sample requests

```
http://ess.aliyuncs.com/?Action=CreateNotificationConfiguration
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ 
&NotificationArn=acs:ess:cn-hangzhou:123456:cloudmonitor
&NotificationType. 1=AUTOSCALING:SCALE_OUT_SUCCESS
&NotificationType. 2=AUTOSCALING:SCALE_IN_SUCCESS
&NotificationType. 3=AUTOSCALING:SCALE_OUT_ERROR
&NotificationType. 4=AUTOSCALING:SCALE_IN_ERROR
&NotificationType. 5=AUTOSCALING:SCALE_REJECT
& <Common request parameters>
```

Successful response examples

`XML` format

```
<CreateNotificationConfigurationResponse> 
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId> 
</CreateNotificationConfigurationResponse> 
```

`JSON` format

```
{
    "requestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## Error codes { .section}

|HttpCode|Error code|Error message|Description|
|--------|:---------|:------------|:----------|
|400|InvalidNotificationArn|The specified parameter notificationArn is invalid.|The error message returned when the specified `NotificationArn` is invalid.|
|400|InvalidNotificationTypes|The specified notificationType is invalid.|The error message returned when the specified `NotificationType.N` is invalid.|
|400|NotificationConfigurationExist|The specified notificationConfiguration already exist for the scalingGroup.|The error message returned when the specified event notification exists in the scaling group.|
|400|NotificationConfigurationQuotaExceed.ForScalingGroup|NotificationConfiguration num exceed for the specified scalingGroup.|The error message returned when the number of event notifications you specify for a scaling group exceeds the maximum number.|
|400|QueueNotExist|The specified queue queuename does not exist.|The error message returned when the specified MNS queue does not exist.|
|400|TopicNotExist|The specified topic topicname does not exist.|The error message returned when the specified MNS topic does not exist.|
|400|UnsupportedNotificationType.CurrentRegion|The notificationType is not supported in the special region which scalingGroup belongs to.|The error message returned when the specified notification type is not supported in the region.|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|The error message returned when the specified scaling group does not exist.|

