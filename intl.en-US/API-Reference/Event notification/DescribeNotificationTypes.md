# DescribeNotificationTypes {#doc_api_1163770 .reference}

You can call this operation to query the types of notifications for scaling events and resource changes.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=DescribeNotificationTypes) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|No|DescribeNotificationTypes|The operation that you want to perform. Set the value to DescribeNotificationTypes.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NotificationTypes| |AUTOSCALING:SCALE\_OUT\_SUCCESS|The list of different types of notifications for scaling events and resource changes.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DescribeNotificationTypes
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeNotificationTypesResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
  <NotificationTypes>
    <NotificationType>AUTOSCALING:SCALE_OUT_SUCCESS</NotificationType>
    <NotificationType>AUTOSCALING:SCALE_IN_SUCCESS</NotificationType>
    <NotificationType>AUTOSCALING:SCALE_OUT_ERROR</NotificationType>
    <NotificationType>AUTOSCALING:SCALE_IN_ERROR</NotificationType>
    <NotificationType>AUTOSCALING:SCALE_REJECT</NotificationType>
  </NotificationTypes>
</DescribeNotificationTypesResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"requestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"notificationTypes":[
		"AUTOSCALING:SCALE_OUT_SUCCESS",
		"AUTOSCALING:SCALE_IN_SUCCESS",
		"AUTOSCALING:SCALE_OUT_ERROR",
		"AUTOSCALING:SCALE_IN_ERROR",
		"AUTOSCALING:SCALE_REJECT"
	]
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Ess)

