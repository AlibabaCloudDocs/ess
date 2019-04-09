# ModifyNotificationConfiguration {#doc_api_Ess_ModifyNotificationConfiguration .reference}

修改您创建的弹性伸缩事件及资源变化通知（ModifyNotificationConfiguration）。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=ModifyNotificationConfiguration)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|NotificationArn|String|是|acs:ess:cn-hangzhou:123456:cloudmonitor|通知对象标识符。格式为 `acs:ess:{region}:{account-id}:{resource-relative-id}`，其中：

 -   `region` 为伸缩组所在的地域 ID。更多详情，请参阅 [地域和可用区](~~40654~~)。
-   `account-id` 为您的账号 ID。
-   `resource-relative-id` 为通知方式，可选值包括云监控系统事件 `cloudmonitor`、消息服务 MNS 队列 `queue/{queuename}` 和 MNS 主题 `topic/{topicname}`。

 |
|NotificationType.N|RepeatList|是|AUTOSCALING:SCALE\_OUT\_SUCCESS|一类或者多类弹性伸缩事件通知。N 的取值范围：1~5，多个取值使用重复列表的形式。您可以通过接口 [DescribeNotificationTypes](~~71117~~) 查询参数取值。

 |
|ScalingGroupId|String|是|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组 ID。

 |
|Action|String|否|ModifyNotificationConfiguration|系统规定参数。取值：ModifyNotificationConfiguration。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=ModifyNotificationConfiguration
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
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

``` {#xml_return_success_demo}
<ModifyNotificationConfigurationResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyNotificationConfigurationResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ess)

|HttpCode

|错误码

|错误信息

|描述

|
|----------|-----|------|----|
|400

|InvalidNotificationTypes

|The specified notificationType is invalid.

|指定的

`NotificationType.N`不合法。

|
|400

|NotificationConfigurationNotExist

|The specified notificationConfiguration not exist for the scalingGroup.

|当前伸缩组不存在指定的弹性伸缩事件及资源变化通知类型。

|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|指定的伸缩组不存在。

|

