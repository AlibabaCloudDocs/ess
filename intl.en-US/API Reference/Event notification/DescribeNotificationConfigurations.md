# DescribeNotificationConfigurations

You can call this operation to query notifications for scaling activities and resource changes.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeNotificationConfigurations&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeNotificationConfigurations|The operation that you want to perform. Set the value to DescribeNotificationConfigurations. |
|ScalingGroupId|String|Yes|asg-bp1igpak5ft1flyp\*\*\*\*|The ID of the scaling group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NotificationConfigurationModels|Array of NotificationConfigurationModel| |Details about the notifications for scaling activities and resource changes. |
|NotificationConfigurationModel| | | |
|NotificationArn|String|acs:mns:cn-beijing:161456884340\*\*\*\*:topic/modifyLifecycleHo\*\*\*\*|The Alibaba Cloud Resource Name \(ARN\) of the notified party. The following list describes the formats of this parameter:

-   When the notified party is Cloud Monitor, the parameter format is acs:ess:\{region-id\}:\{account-id\}:cloudmonitor.
-   When the notified party is an MNS queue, the parameter format is acs:mns:\{region-id\}:\{account-id\}:queue/\{queuename\}.
-   When the notified party is an MNS topic, the parameter format is acs:mns:\{region-id\}:\{account-id\}:topic/\{topicname\}.

The variables in the preceding parameter formats have the following meanings:

-   region-id: the region ID of the scaling group
-   account-id: the ID of Alibaba Cloud account
-   queuename: the name of the MNS queue
-   topicname: the name of the MNS topic |
|NotificationTypes|List|AUTOSCALING:SCALE\_IN\_SUCCESS|The types of notifications for scaling activities and resource changes. |
|ScalingGroupId|String|asg-bp1igpak5ft1flyp\*\*\*\*|The ID of the scaling group. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
http://ess.aliyuncs.com/?Action=DescribeNotificationConfigurations
&ScalingGroupId=asg-bp1igpak5ft1flyp****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeNotificationConfigurationsResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <NotificationConfigurationModels>
            <NotificationConfigurationModel>
                  <NotificationArn>acs:mns:cn-beijing:161456884340****:queue/modifyLifecycleHo****</NotificationArn>
                  <ScalingGroupId>asg-bp1igpak5ft1flyp****</ScalingGroupId>
                  <NotificationTypes>
                        <NotificationType>AUTOSCALING:SCALE_IN_SUCCESS</NotificationType>
                        <NotificationType>AUTOSCALING:SCALE_IN_ERROR</NotificationType>
                  </NotificationTypes>
            </NotificationConfigurationModel>
            <NotificationConfigurationModel>
                  <NotificationArn>acs:mns:cn-beijing:161456884340****:topic/modifyLifecycleHo****</NotificationArn>
                  <ScalingGroupId>asg-bp18p2yfxow2dloq****</ScalingGroupId>
                  <NotificationTypes>
                        <NotificationType>AUTOSCALING:SCALE_IN_SUCCESS</NotificationType>
                        <NotificationType>AUTOSCALING:SCALE_IN_ERROR</NotificationType>
                  </NotificationTypes>
            </NotificationConfigurationModel>
      </NotificationConfigurationModels>
</DescribeNotificationConfigurationsResponse>
```

`JSON` format

```
{
    "RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "NotificationConfigurationModels":{
        "NotificationConfigurationModel":[
            {
                "NotificationArn":"acs:mns:cn-beijing:161456884340****:queue/modifyLifecycleHo****",
                "ScalingGroupId":"asg-bp1igpak5ft1flyp****",
                "NotificationTypes":{
                    "NotificationType":[
                        "AUTOSCALING:SCALE_IN_SUCCESS",
                        "AUTOSCALING:SCALE_IN_ERROR"
                    ]
                }
            },
            {
                "NotificationArn":"acs:mns:cn-beijing:161456884340****:topic/modifyLifecycleHo****",
                "ScalingGroupId":"asg-bp18p2yfxow2dloq****",
                "NotificationTypes":{
                    "NotificationType":[
                        "AUTOSCALING:SCALE_IN_SUCCESS",
                        "AUTOSCALING:SCALE_IN_ERROR"
                    ]
                }
            }
        ]
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist. |

