# ModifyNotificationConfiguration {#concept_71118_zh .concept}

You can call this operation to modify scaling events and resource change notifications \(`ModifyNotificationConfiguration`\).

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set the value to ModifyNotificationConfiguration.|
|ScalingGroupId|String|Yes|The ID of the scaling group.|
|NotificationArn|String|Yes|The identifier for the notification object. The format is: `acs:ess:{region}:{account-id}:{resource-relative-id}`. -   The `region` is the ID of the region where the scaling group is located. For more information, see [Regions and Zones](../../../../../reseller.en-US/General Reference/Regions and Zones.md#).
-   The `account-id` is the account ID.
-   The `resource-relative-id` is the notification method. Valid values: `cloudmonitor` \(system events of CloudMonitor\), `queue/{queuename}` \(MNS queues\), and `topic/{topicname}` \(MNS topics\).

|
|NotificationType.N|String|Yes|Includes one or more types of scaling event notifications. Valid values of `N`: 1 to 5. Multiple values are listed in ascending order. You can call the [DescribeNotificationTypes](reseller.en-US/API-Reference/Event notification/DescribeNotificationTypes.md#) operation to query parameter values.|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|RequestId|String|The request ID.|

## Examples { .section}

Sample requests

```
http://ess.aliyuncs.com/?Action=ModifyNotificationConfiguration
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
<ModifyNotificationConfigurationResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyNotificationConfigurationResponse>
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
|400|InvalidNotificationTypes|The specified notificationType is invalid.|The error message returned when the specified `NotificationType.N` is invalid.|
|400|NotificationConfigurationNotExist|The specified notificationConfiguration not exist for the scalingGroup.|The error message returned when the specified scaling event and the notification type of the resource change do not exist.|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|The error message returned when the specified scaling group does not exist.|

