# ModifyNotificationConfiguration {#doc_api_Ess_ModifyNotificationConfiguration .reference}

You can call this operation to modify notification configurations for scaling events and resource changes.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=ModifyNotificationConfiguration) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|NotificationArn|String|Yes|acs:ess:cn-hangzhou:123456:cloudmonitor|The identifier of the notification object. The value must be in the `acs:ess:{region}:{account-id}:{resource-relative-id}` format.

 -   `region` is the ID of the region where the scaling group is located. For more information, see [Regions and zones](~~40654~~).
-   `account-id` is your account ID.
-   `resource-relative-id`is the notification method. Valid values: `cloudmonitor`, `queue/{queuename}`, and `topic/{topicname}`.

 |
|NotificationType.N|RepeatList|Yes|AUTOSCALING:SCALE\_OUT\_SUCCESS|One or more types of scaling event notifications. Valid values of N: 1 to 5. Multiple values must be listed in ascending order. You can call the [DescribeNotificationTypes](~~71117~~) operation to query parameter values.

 |
|ScalingGroupId|String|Yes|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|The ID of the scaling group.

 |
|Action|String|No|ModifyNotificationConfiguration|The operation that you want to perform. Set the value to ModifyNotificationConfiguration.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=ModifyNotificationConfiguration
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
<ModifyNotificationConfigurationResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</ModifyNotificationConfigurationResponse> 

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

|InvalidNotificationTypes

|The specified notificationType is invalid.

|The error message returned when the specified value

`of the NotificationType.N parameter`is invalid.

|
|400

|NotificationConfigurationNotExist

|The specified notificationConfiguration not exist for the scalingGroup.

|The error message returned when the specified notification configuration does not exist in the scaling group.

|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned when the specified scaling group does not exist.

|

