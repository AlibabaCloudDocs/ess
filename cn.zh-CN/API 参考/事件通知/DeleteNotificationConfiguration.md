# DeleteNotificationConfiguration {#concept_71115_zh .concept}

删除弹性伸缩事件及资源变化通知（`DeleteNotificationConfiguration`）。

## 请求参数 { .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DeleteNotificationConfiguration。|
|ScalingGroupId|String|是|伸缩组 ID。|
|NotificationArn|String|是|通知对象标识符。格式为 `acs:ess:{region}:{account-id}:{resource-relative-id}`，其中：-   `region` 为伸缩组所在的地域 ID。更多详情，请参阅 [地域和可用区](../../../../../cn.zh-CN/通用参考/地域和可用区.md#)。
-   `account-id` 为您的账号 ID。
-   `resource-relative-id` 为通知方式，可选值包括云监控系统事件 `cloudmonitor`、消息服务 MNS 队列 `queue/{queuename}` 和 MNS 主题 `topic/{topicname}`。

|

## 返回参数 { .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|请求 ID。|

## 示例 { .section}

请求示例

```
http://ess.aliyuncs.com/?Action=DeleteNotificationConfiguration
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&NotificationArn=acs:ess:cn-hangzhou:123456:cloudmonitor
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteNotificationConfigurationResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</DeleteNotificationConfigurationResponse>
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
|400|NotificationConfigurationNotExist|The specified notificationConfiguration not exist for the scalingGroup.|当前伸缩组不存在指定的伸缩事件及资源变化通知。|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|指定的伸缩组不存在。|

