# ModifyNotificationConfiguration

You can call this operation to modify a notification for scaling activities or resource changes.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=ModifyNotificationConfiguration&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyNotificationConfiguration|The operation that you want to perform. Set the value to ModifyNotificationConfiguration. |
|NotificationArn|String|Yes|acs:ess:cn-beijing:161456884340\*\*\*\*:cloudmonitor|The Alibaba Cloud Resource Name \(ARN\) of the notified party. The following list describes the formats of this parameter:

-   When the notified party is Cloud Monitor, the parameter format is acs:ess:\{region-id\}:\{account-id\}:cloudmonitor.
-   When the notified party is an MNS queue, the parameter format is acs:mns:\{region-id\}:\{account-id\}:queue/\{queuename\}.
-   When the notified party is an MNS topic, the parameter format is acs:mns:\{region-id\}:\{account-id\}:topic/\{topicname\}.

The variables in the preceding parameter formats have the following meanings:

-   region-id: the region ID of the scaling group
-   account-id: the ID of Alibaba Cloud account
-   queuename: the name of the MNS queue
-   topicname: the name of the MNS topic |
|NotificationType.N|RepeatList|Yes|AUTOSCALING:SCALE\_OUT\_SUCCESS|The type of notification N for scaling activities or resource changes. Valid values of N: 1 to 8. Specify multiple values in the repeated list form.

You can call the [DescribeNotificationTypes](~~71117~~) operation to query the value of this parameter. |
|ScalingGroupId|String|Yes|asg-bp1igpak5ft1flyp\*\*\*\*|The ID of the scaling group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=ModifyNotificationConfiguration
&ScalingGroupId=asg-bp1igpak5ft1flyp****
&NotificationArn=acs:ess:cn-beijing:161456884340****:cloudmonitor
&NotificationType.1=AUTOSCALING:SCALE_OUT_SUCCESS
&NotificationType.2=AUTOSCALING:SCALE_IN_SUCCESS
&NotificationType.3=AUTOSCALING:SCALE_OUT_ERROR
&NotificationType.4=AUTOSCALING:SCALE_IN_ERROR
&NotificationType.5=AUTOSCALING:SCALE_REJECT
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyNotificationConfigurationResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyNotificationConfigurationResponse>
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

|InvalidNotificationTypes

|The specified NotificationType is invalid.

|The error message returned because the specified NotificationType.N parameter is invalid. |
|400

|NotificationConfigurationNotExist

|The specified notificationConfiguration not exist for the scalingGroup.

|The error message returned because the specified notification type for scaling activities and resource changes does not exist in the scaling group. |
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist. |

