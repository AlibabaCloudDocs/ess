# CreateNotificationConfiguration {#doc_api_Ess_CreateNotificationConfiguration .reference}

调用CreateNotificationConfiguration创建弹性伸缩事件及资源变化通知。

## 接口说明 {#description .section}

您可以设置由云监控系统事件、消息服务MNS队列或MNS主题接收消息通知。当伸缩组发生指定类型的伸缩事件或者资源变化时，弹性伸缩会发送消息通知云监控或消息。目前部分阿里云地域暂未部署MNS队列和MNS主题服务，详情请参见[MNS常见问题](~~27436~~)。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=CreateNotificationConfiguration&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|NotificationArn|String|是|acs:ess:cn-hangzhou:123456:cloudmonitor|通知对象标识符。格式为`acs:ess:{region}:{account-id}:{resource-relative-id}`，其中：

 -   region为伸缩组所在地域的ID。更多详情，请参见[地域和可用区](~~40654~~)。
-   account-id为您账号的ID。
-   resource-relative-id为通知方式，取值范围：
    -   cloudmonitor：云监控
    -   MNS队列：queue/\{queuename\}，其中topicname需要替换为具体的MNS队列名称。
    -   MNS主题：topic/\{topicname\}，其中topicname需要替换为具体的MNS主题名称。

 |
|NotificationType.N|RepeatList|是|AUTOSCALING:SCALE\_OUT\_SUCCESS|一类或者多类弹性伸缩事件及资源变化通知。N的取值范围：1~8，多个取值使用重复列表的形式。

 您可以调用接口[DescribeNotificationTypes](~~71117~~)查询参数取值。

 |
|ScalingGroupId|String|是|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组的ID。

 |
|Action|String|否|CreateNotificationConfiguration|系统规定参数。取值：CreateNotificationConfiguration。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=CreateNotificationConfiguration
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
<CreateNotificationConfigurationResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</CreateNotificationConfigurationResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述

|
|----------|-----|------|----|
|400

|InvalidNotificationArn

|The specified parameter notificationArn is invalid.

|指定的NotificationArn不合法。

|
|400

|InvalidNotificationTypes

|The specified notificationType is invalid.

|指定的NotificationType.N不合法。

|
|400

|NotificationConfigurationExist

|The specified notificationConfiguration already exist for the scalingGroup.

|指定的事件通知已经存在于当前伸缩组中。

|
|400

|NotificationConfigurationQuotaExceed.ForScalingGroup

|NotificationConfiguration num exceed for the specified scalingGroup.

|当前伸缩组配置的通知功能超出允许的上限值。

|
|400

|QueueNotExist

|The specified queue queuename does not exist.

|指定的MNS队列不存在。

|
|400

|TopicNotExist

|The specified topic topicname does not exist.

|指定的MNS主题不存在。

|
|400

|UnsupportedNotificationType.CurrentRegion

|The notificationType is not supported in the special region which scalingGroup belongs to.

|当前地域不支持该通知方式。

|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|指定的伸缩组不存在。

|

