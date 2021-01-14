# DescribeNotificationTypes

调用DescribeNotificationTypes查询弹性伸缩事件及资源变化通知的类型。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DescribeNotificationTypes&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeNotificationTypes|系统规定参数。取值：DescribeNotificationTypes |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|NotificationTypes|List|AUTOSCALING:SCALE\_OUT\_SUCCESS|弹性伸缩事件及资源变化通知类型的列表。

 -   AUTOSCALING:SCALE\_OUT\_SUCCESS：扩容伸缩活动成功。
-   AUTOSCALING:SCALE\_IN\_SUCCESS：缩容伸缩活动成功。
-   AUTOSCALING:SCALE\_OUT\_ERROR：扩容伸缩活动失败。
-   AUTOSCALING:SCALE\_IN\_ERROR：缩容伸缩活动失败。
-   AUTOSCALING:SCALE\_REJECT：伸缩活动拒绝执行。
-   AUTOSCALING:SCALE\_OUT\_START：扩容伸缩活动开始。
-   AUTOSCALING:SCALE\_IN\_START：缩容伸缩活动开始。
-   AUTOSCALING:SCHEDULE\_TASK\_EXPIRING：任务到期提醒。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=DescribeNotificationTypes
&<公共请求参数>
```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ess)查看更多错误码。

