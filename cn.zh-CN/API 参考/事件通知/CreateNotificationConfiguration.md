# CreateNotificationConfiguration {#concept_71114_zh .concept}

创建弹性伸缩事件及资源变化通知（`CreateNotificationConfiguration`）。

## 描述 {#section_kyv_sjl_lgb .section}

您可以设置由云监控系统事件、消息服务 MNS 队列或 MNS 主题接收消息通知。当伸缩组发生指定类型的伸缩事件或者资源变化时，弹性伸缩会发送消息通知云监控或 MNS。

目前，有部分阿里云地域暂未部署 MNS 队列 和 MNS 主题服务，具体详情，请访问 [MNS 管理控制台](https://mns.console.aliyun.com) 或者参阅 [MNS 常见问题]()。

## 请求参数 { .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：CreateNotificationConfiguration。|
|ScalingGroupId|String|是|伸缩组 ID。|
|NotificationArn|String|是|通知对象标识符。格式为 `acs:ess:{region}:{account-id}:{resource-relative-id}`，其中：-   `region`：伸缩组所在地域 ID。更多详情，请参阅 [地域和可用区](../../../../../cn.zh-CN/通用参考/地域和可用区.md#)。
-   `account-id`：您的账号 ID。
-   `resource-relative-id` ：通知方式，可选值包括云监控 `cloudmonitor`，MNS 队列 `queue/{queuename}` 和 MNS 主题 `topic/{topicname}`。

|
|NotificationType.N|String|是|一类或者多类弹性伸缩事件及资源变化通知。`N` 的取值范围：\[1, 8\]，多个取值使用重复列表的形式。您可以通过接口 [DescribeNotificationTypes](cn.zh-CN/API 参考/事件通知/DescribeNotificationTypes.md#) 查询参数取值。

|

## 返回参数 { .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|请求 ID。|

## 示例 { .section}

请求示例

```
http://ess.aliyuncs.com/?Action=CreateNotificationConfiguration
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&NotificationArn=acs:ess:cn-hangzhou:123456:cloudmonitor
&NotificationType.1=AUTOSCALING:SCALE_OUT_SUCCESS
&NotificationType.2=AUTOSCALING:SCALE_IN_SUCCESS
&NotificationType.3=AUTOSCALING:SCALE_OUT_ERROR
&NotificationType.4=AUTOSCALING:SCALE_IN_ERROR
&NotificationType.5=AUTOSCALING:SCALE_REJECT
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateNotificationConfigurationResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</CreateNotificationConfigurationResponse>
```

`JSON` 格式

```
{
    "requestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|:--|:---|:-|
|400|InvalidNotificationArn|The specified parameter notificationArn is invalid.|指定的 `NotificationArn` 不合法。|
|400|InvalidNotificationTypes|The specified notificationType is invalid.|指定的 `NotificationType.N`不合法。|
|400|NotificationConfigurationExist|The specified notificationConfiguration already exist for the scalingGroup.|指定的事件通知已经存在于当前伸缩组中。|
|400|NotificationConfigurationQuotaExceed.ForScalingGroup|NotificationConfiguration num exceed for the specified scalingGroup.|当前伸缩组配置的通知功能超出允许的上限值。|
|400|QueueNotExist|The specified queue queuename does not exist.|指定的 MNS 队列不存在。|
|400|TopicNotExist|The specified topic topicname does not exist.|指定的 MNS 主题不存在。|
|400|UnsupportedNotificationType.CurrentRegion|The notificationType is not supported in the special region which scalingGroup belongs to.|当前地域不支持该通知方式。|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|指定的伸缩组不存在。|

