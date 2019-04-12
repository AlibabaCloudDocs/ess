# DeleteNotificationConfiguration {#concept_71115_zh .concept}

You can call this operation to delete scaling events and resource change notifications \(`DeleteNotificationConfiguration`\).

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set the value to DeleteNotificationConfiguration.|
|ScalingGroupId|String|Yes|The ID of the scaling group.|
|NotificationArn|String|Yes|The identifier for the notification object. The format is: `acs:ess:{region}:{account-id}:{resource-relative-id}`. -   The `region` is the ID of the region where the scaling group is located. For more information, see [Regions and Zones](../../../../../reseller.en-US/General Reference/Regions and Zones.md#).
-   The `account-id` is the account ID.
-   The `resource-relative-id` is the notification method. Valid values: `cloudmonitor` \(system events of CloudMonitor\), `queue/{queuename}` \(MNS queues\), and `topic/{topicname}` \(MNS topics\).

|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|RequestId|String|The request ID|

## Examples { .section}

Sample requests

```
http://ess.aliyuncs.com/?Action=DeleteNotificationConfiguration
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ 
&NotificationArn=acs:ess:cn-hangzhou:123456:cloudmonitor 
&<Common request parameters>
```

Successful response examples

`XML` format

```
<DeleteNotificationConfigurationResponse> 
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId> 
</DeleteNotificationConfigurationResponse> 
```

`JSON` format

```
{
    "requestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|:---------|:------------|:----------|
|400|NotificationConfigurationNotExist|The specified notificationConfiguration not exist for the scalingGroup.|The error message returned when the specified scaling event and resource change notification do not exist in the scaling group.|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|The error message returned when the specified scaling group does not exist.|

