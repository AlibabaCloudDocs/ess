# DescribeNotificationConfigurations {#concept_71116_zh .concept}

You can call this operation to query newly created scaling events and resource change notifications \(`DescribeNotificationConfigurations`\).

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set the value to DescribeNotificationConfigurations.|
|ScalingGroupId|String|Yes|The ID of the scaling group.|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|RequestId|String|The request ID|
|NotificationConfigurationModels|Array of [NotificationConfigurationModelSet](#hxtwo)|The list of scaling events and resource change notifications.|

## NotificationConfigurationModelSet {#hxtwo .section}

|Name|Type|Description|
|:---|:---|:----------|
|ScalingGroupId|String|The request ID|
|NotificationArn|String|The list of scaling events and resource change notifications.|
|NotificationTypes|Array of [NotificationTypeSet](#hxthree)|The list of scaling events and notification types of resource changes.|

## NotificationTypeSet {#hxthree .section}

|Name|Type|Description|
|:---|:---|:----------|
|NotificationType|String|Scaling events and notification types of resource changes. You can call the [DescribeNotificationTypes](reseller.en-US/API-Reference/Event notification/DescribeNotificationTypes.md#) operation to query parameter values.|

## Examples { .section}

Sample requests

```
http://ess.aliyuncs.com/?Action=DescribeNotificationConfigurations
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ 
&<Common request parameters>
```

Successful response examples

`XML` format

```
<DescribeNotificationConfigurationsResponse> 
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId> 
    <NotificationConfigurationModels>
        <NotificationConfigurationModel>
            <NotificationArn>xxxxxxxxx</NotificationArn> 
            <ScalingGroupId>xxxxxxxxxxx</ScalingGroupId> 
            <NotificationTypes>
                <NotificationType>AUTOSCALING:SCALE_IN_SUCCESS</NotificationType>
                <NotificationType>AUTOSCALING:SCALE_IN_ERROR</NotificationType> 
            </NotificationTypes> 
        </NotificationConfigurationModel>
        <NotificationConfigurationModel>
            <NotificationArn>xxxxxxxxx</NotificationArn>
            <ScalingGroupId>xxxxxxxxxxx</ScalingGroupId>
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
    "notificationConfigurationModels": [
    {
      "notificationArn": "xxxxxxxxxx",
      "notificationTypes": [
        "AUTOSCALING:SCALE_OUT_SUCCESS",
        "AUTOSCALING:SCALE_OUT_ERROR",
        "AUTOSCALING:SCALE_IN_SUCCESS",
        "AUTOSCALING:SCALE_IN_ERROR",
        "AUTOSCALING:SCALE_REJECT"
      ],
      "scalingGroupId": "xxxxxxxxxx"
    },
    {
      "notificationArn": "xxxxxxxxxx",
      "notificationTypes": [
        "AUTOSCALING:SCALE_OUT_SUCCESS",
        "AUTOSCALING:SCALE_OUT_ERROR",
        "AUTOSCALING:SCALE_IN_SUCCESS",
        "AUTOSCALING:SCALE_IN_ERROR",
        "AUTOSCALING:SCALE_REJECT"
      ],
      "scalingGroupId": "xxxxxxxxxx"
    }
  ],
  "requestId": "EEAB83FF-318A-41CA-8EB6-BB9614256BA9"
}
```

## Error codes { .section}

|HttpCode|Error code|Error message|Description|
|--------|:---------|:------------|:----------|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|The error message returned when the specified scaling group does not exist.|

