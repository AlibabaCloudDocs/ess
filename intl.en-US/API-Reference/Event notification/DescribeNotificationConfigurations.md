# DescribeNotificationConfigurations {#doc_api_1163768 .reference}

You can call this operation to query notification configurations for scaling events and resource changes.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=DescribeNotificationConfigurations) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|ScalingGroupId|String|Yes|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|The ID of the scaling group.

 |
|Action|String|No|DescribeNotificationConfigurations|The operation that you want to perform. Set the value to DescribeNotificationConfigurations.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NotificationConfigurationModels| | |The list of notifications for scaling events and resource changes.

 |
|└NotificationArn|String|acs:ess:cn-hangzhou:1111111111:queue/queue1|The list of notifications for scaling events and resource changes.

 |
|└NotificationTypes| |AUTOSCALING:SCALE\_IN\_SUCCESS|The list of different types of notifications for scaling events and resource changes.

 |
|└ScalingGroupId|String|asg-\*\*\*\*|The ID of the scaling group.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DescribeNotificationConfigurations
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeNotificationConfigurationsResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
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
      <ScalingGroupId>xxxxxxxxxx</ScalingGroupId>
      <NotificationTypes>
        <NotificationType>AUTOSCALING:SCALE_IN_SUCCESS</NotificationType>
        <NotificationType>AUTOSCALING:SCALE_IN_ERROR</NotificationType>
      </NotificationTypes>
    </NotificationConfigurationModel>
  </NotificationConfigurationModels>
</DescribeNotificationConfigurationsResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"requestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"notificationConfigurationModels":[
		{
			"notificationArn":"xxxxxxxxxx",
			"notificationTypes":[
				"AUTOSCALING:SCALE_OUT_SUCCESS",
				"AUTOSCALING:SCALE_OUT_ERROR",
				"AUTOSCALING:SCALE_IN_SUCCESS",
				"AUTOSCALING:SCALE_IN_ERROR",
				"AUTOSCALING:SCALE_REJECT"
			],
			"scalingGroupId":"xxxxxxxxxx"
		},
		{
			"notificationArn":"xxxxxxxxxx",
			"notificationTypes":[
				"AUTOSCALING:SCALE_OUT_SUCCESS",
				"AUTOSCALING:SCALE_OUT_ERROR",
				"AUTOSCALING:SCALE_IN_SUCCESS",
				"AUTOSCALING:SCALE_IN_ERROR",
				"AUTOSCALING:SCALE_REJECT"
			],
			"scalingGroupId":"xxxxxxxxxx"
		}
	]
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
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned when the specified scaling group does not exist.

|

