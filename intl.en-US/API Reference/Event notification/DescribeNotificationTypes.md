# DescribeNotificationTypes

You can call this operation to query the types of notifications for scaling activities and resource changes.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeNotificationTypes&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeNotificationTypes|The operation that you want to perform. Set the value to DescribeNotificationTypes. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NotificationTypes|List|AUTOSCALING:SCALE\_OUT\_SUCCESS|The types of notifications for scaling activities and resource changes.

 -   AUTOSCALING:SCALE\_OUT\_SUCCESS: The scale-out event is successful.
-   AUTOSCALING:SCALE\_IN\_SUCCESS: The scale-in event is successful.
-   AUTOSCALING:SCALE\_OUT\_ERROR: The scale-out event fails.
-   AUTOSCALING:SCALE\_IN\_ERROR: The scale-in event fails.
-   AUTOSCALING:SCALE\_REJECT: The scaling activity is rejected.
-   AUTOSCALING:SCALE\_OUT\_START: The scale-out event is started.
-   AUTOSCALING:SCALE\_IN\_START: The scale-in event is started.
-   AUTOSCALING:SCHEDULE\_TASK\_EXPIRING: Auto Scaling sends a notification when a scheduled task is about to expire. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DescribeNotificationTypes
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeNotificationTypesResponse>
    <RequestId>66046F31-AF8C-44B4-9992-453F33CF179E</RequestId>
    <NotificationTypes>
        <NotificationType>AUTOSCALING:SCALE_OUT_SUCCESS</NotificationType>
        <NotificationType>AUTOSCALING:SCALE_IN_SUCCESS</NotificationType>
        <NotificationType>AUTOSCALING:SCALE_OUT_ERROR</NotificationType>
        <NotificationType>AUTOSCALING:SCALE_IN_ERROR</NotificationType>
        <NotificationType>AUTOSCALING:SCALE_REJECT</NotificationType>
        <NotificationType>AUTOSCALING:SCALE_OUT_START</NotificationType>
        <NotificationType>AUTOSCALING:SCALE_IN_START</NotificationType>
        <NotificationType>AUTOSCALING:SCHEDULE_TASK_EXPIRING</NotificationType>
    </NotificationTypes>
</DescribeNotificationTypesResponse>
```

`JSON` format

```
{
	"RequestId": "66046F31-AF8C-44B4-9992-453F33CF179E",
	"NotificationTypes": {
		"NotificationType": [
			"AUTOSCALING:SCALE_OUT_SUCCESS",
			"AUTOSCALING:SCALE_IN_SUCCESS",
			"AUTOSCALING:SCALE_OUT_ERROR",
			"AUTOSCALING:SCALE_IN_ERROR",
			"AUTOSCALING:SCALE_REJECT",
			"AUTOSCALING:SCALE_OUT_START",
			"AUTOSCALING:SCALE_IN_START",
			"AUTOSCALING:SCHEDULE_TASK_EXPIRING"
		]
	}
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

