# DescribeNotificationTypes {#concept_71117_zh .concept}

You can call this operation to query scaling events and notification types of resource changes \(`DescribeNotificationTypes`\).

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set the value to DescribeNotificationTypes.|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|RequestId|String|The request ID|
|NotificationTypes|Array of [NotificationTypeSet](#hxfour)|The list of scaling events and notification types of resource changes.|

## NotificationTypeSet {#hxfour .section}

|Name|Type|Description|
|:---|:---|:----------|
|NotificationType|String|Scaling events and notification types of resource changes. Valid values:-   AUTOSCALING:SCALE\_OUT\_SUCCESS: indicates that a scale-out activity is successful.
-   AUTOSCALING:SCALE\_IN\_SUCCESS: indicates that a scale-in activity is successful.
-   AUTOSCALING:SCALE\_OUT\_ERROR: indicates that a scale-out activity has failed.
-   AUTOSCALING:SCALE\_IN\_ERROR: indicates that a scale-in activity has failed.
-   AUTOSCALING:SCALE\_REJECT: indicates that a scaling activity is rejected.
-   AUTOSCALING:SCALE\_OUT\_START: indicates that a scale-out activity starts.
-   AUTOSCALING:SCALE\_IN\_START: indicates that a scale-in activity starts.
-   AUTOSCALING:SCHEDULE\_TASK\_EXPIRING: indicates that a scheduled task expires.

|

## Examples { .section}

Sample requests

```
http://ess.aliyuncs.com/?Action=DescribeNotificationTypes
& <Common request parameters>
```

Successful response examples

`XML` format

```
<DescribeNotificationTypesResponse>
    <RequestId>21F638C3-7054-4C1E-A143-A74C20F507A3</RequestId>
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

```
{
    "notificationTypes": [
        "AUTOSCALING:SCALE_OUT_SUCCESS",
        "AUTOSCALING:SCALE_IN_SUCCESS",
        "AUTOSCALING:SCALE_OUT_ERROR",
        "AUTOSCALING:SCALE_IN_ERROR",
        "AUTOSCALING:SCALE_REJECT"
    ],
    "requestId": "21F638C3-7054-4C1E-A143-A74C20F507A3"
}
```

