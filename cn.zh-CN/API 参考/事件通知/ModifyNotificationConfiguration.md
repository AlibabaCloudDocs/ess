# ModifyNotificationConfiguration {#concept_71118_zh .concept}

修改您创建的弹性伸缩事件及资源变化通知（`ModifyNotificationConfiguration`）。

## 请求参数 { .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifyNotificationConfiguration。|
|ScalingGroupId|String|是|伸缩组 ID。|
|NotificationArn|String|是|通知对象标识符。格式为 `acs:ess:{region}:{account-id}:{resource-relative-id}`，其中：-   `region` 为伸缩组所在的地域 ID。更多详情，请参阅 [地域和可用区](../../../../../cn.zh-CN/通用参考/地域和可用区.md#)。
-   `account-id` 为您的账号 ID。
-   `resource-relative-id` 为通知方式，可选值包括云监控系统事件 `cloudmonitor`、消息服务 MNS 队列 `queue/{queuename}` 和 MNS 主题 `topic/{topicname}`。

|
|NotificationType.N|String|是|一类或者多类弹性伸缩事件通知。`N` 的取值范围：\[1, 5\]，多个取值使用重复列表的形式。您可以通过接口 [DescribeNotificationTypes](cn.zh-CN/API 参考/事件通知/DescribeNotificationTypes.md#) 查询参数取值。|

## 返回参数 { .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|请求 ID。|

## 示例 { .section}

请求示例

```
http://ess.aliyuncs.com/?Action=ModifyNotificationConfiguration
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
<ModifyNotificationConfigurationResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyNotificationConfigurationResponse>
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
|400|InvalidNotificationTypes|The specified notificationType is invalid.|指定的 `NotificationType.N` 不合法。|
|400|NotificationConfigurationNotExist|The specified notificationConfiguration not exist for the scalingGroup.|当前伸缩组不存在指定的弹性伸缩事件及资源变化通知类型。|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|指定的伸缩组不存在。|

