# DeleteNotificationConfiguration

You can call this operation to delete a notification for scaling activities or resource changes.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DeleteNotificationConfiguration&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteNotificationConfiguration|The operation that you want to perform. Set the value to DeleteNotificationConfiguration. |
|NotificationArn|String|Yes|acs:ess:cn-beijing:161456884340\*\*\*\*:cloudmonitor|The Alibaba Cloud Resource Name \(ARN\) of the notified party. The following list describes the formats of this parameter:

-   When the notified party is Cloud Monitor, the parameter format is acs:ess:\{region-id\}:\{account-id\}:cloudmonitor.
-   When the notified party is an MNS queue, the parameter format is acs:mns:\{region-id\}:\{account-id\}:queue/\{queuename\}.
-   When the notified party is an MNS topic, the parameter format is acs:mns:\{region-id\}:\{account-id\}:topic/\{topicname\}.

The variables in the preceding parameter formats have the following meanings:

-   region-id: the region ID of the scaling group
-   account-id: the ID of Alibaba Cloud account
-   queuename: the name of the MNS queue
-   topicname: the name of the MNS topic |
|ScalingGroupId|String|Yes|asg-bp18p2yfxow2dloq\*\*\*\*|The ID of the scaling group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DeleteNotificationConfiguration
&ScalingGroupId=asg-bp18p2yfxow2dloq****
&NotificationArn=acs:ess:cn-beijing:161456884340****:cloudmonitor
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteNotificationConfigurationResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DeleteNotificationConfigurationResponse>
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

|NotificationConfigurationNotExist

|The specified notificationConfiguration not exist for the scalingGroup.

|The error message returned because the specified notification for scaling activities and resource changes does not exist in the scaling group. |
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist. |

