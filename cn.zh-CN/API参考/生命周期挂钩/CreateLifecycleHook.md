# CreateLifecycleHook {#doc_api_Ess_CreateLifecycleHook .reference}

调用CreateLifecycleHook为伸缩组创建一个或多个生命周期挂钩。

## 接口说明 {#description .section}

一个伸缩组最多可以创建6个生命周期挂钩。创建了生命周期挂钩的伸缩组，在发生伸缩活动时，生命周期挂钩会暂停伸缩活动一段时间，即伸缩活动等待状态。您可以通过HeartbeatTimeout参数指定具体的等待时长。

伸缩活动处于等待状态时，伸缩组弹性扩张活动之前或者弹性收缩活动之前为您保留指定时长的操作时间。您可以在等待期间进行初始化ECS实例配置、获取ECS实例数据等操作。等待状态的进程在处于加入或移除RDS实例IP白名单和加入或移除SLB实例IP白名单之间。

推荐您利用消息服务MNS的主题或者队列创建消息通知，掌握伸缩组内正在启动或者即将释放的ECS实例的动态。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=CreateLifecycleHook&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|LifecycleTransition|String|是|SCALE\_OUT|生命周期挂钩适用的伸缩活动类型，取值范围：

 -   SCALE\_OUT：伸缩组弹性扩张活动
-   SCALE\_IN：伸缩组弹性收缩活动

 |
|ScalingGroupId|String|是|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组的ID。

 |
|Action|String|否|CreateLifecycleHook|系统规定参数。取值：CreateLifecycleHook。

 |
|DefaultResult|String|否|CONTINUE|等待状态结束后的下一步动作，取值范围：

 -   CONTINUE：继续响应弹性扩张活动或者继续响应弹性收缩活动。
-   ABANDON：直接释放弹性扩张活动创建出来的ECS实例或者直接将弹性收缩活动中的ECS实例从伸缩组移除。

 默认值：CONTINUE。

 当伸缩组发生弹性收缩活动（SCALE\_IN）并触发多个生命周期挂钩时，DefaultResult为ABANDON的生命周期挂钩触发的等待状态结束时，会提前将其它对应的等待状态提前结束。其他情况下，下一步动作均以最后一个结束等待状态的下一步动作为准。

 |
|HeartbeatTimeout|Integer|否|600|生命周期挂钩为伸缩组活动设置的等待时间，等待状态超时后会执行下一步动作。取值范围：30~21600，单位：秒。

 默认值：600。

 创建了生命周期挂钩后，您可以调用[RecordLifecycleActionHeartbeat](~~73846~~)延长ECS实例的等待时间，也可以调用[CompleteLifecycleAction](~~73847~~)提前结束伸缩活动的等待状态。

 |
|LifecycleHook.N.DefaultResult|String|否|CONTINUE|等待状态结束后的下一步动作，取值范围：

 -   CONTINUE：继续响应弹性扩张活动或者继续响应弹性收缩活动。
-   ABANDON：直接释放弹性扩张活动创建出来的ECS实例或者直接将弹性收缩活动中的ECS实例从伸缩组移除。

 默认值：CONTINUE。

 当伸缩组发生弹性收缩活动（SCALE\_IN）并触发多个生命周期挂钩时，DefaultResult为ABANDON的生命周期挂钩触发的等待状态结束时，会提前将其它对应的等待状态提前结束。其他情况下，下一步动作均以最后一个结束等待状态的下一步动作为准。

 |
|LifecycleHook.N.HeartbeatTimeout|Integer|否|600|生命周期挂钩为伸缩组活动设置的等待时间，等待状态超时后会执行下一步动作。取值范围：30~21600，单位：秒。

 默认值：600。

 创建了生命周期挂钩后，您可以调用[RecordLifecycleActionHeartbeat](~~73846~~)延长ECS实例的等待时间，也可以调用[CompleteLifecycleAction](~~73847~~)提前结束伸缩活动的等待状态。

 |
|LifecycleHook.N.LifecycleHookName|String|否|test\_SCALE\_OUT|生命周期挂钩的名称。不能与当前伸缩组其他生命周期挂钩重名，长度为2~40个英文或中文字符，以数字、大小字母或中文开头，可包含数字、下划线（\_）、连字符（-）和点号（.）。

 默认值为生命周期挂钩ID。

 |
|LifecycleHook.N.LifecycleTransition|String|否|SCALE\_OUT|生命周期挂钩适用的伸缩活动类型，取值范围：

 -   SCALE\_OUT：伸缩组弹性扩张活动
-   SCALE\_IN：伸缩组弹性收缩活动

 |
|LifecycleHook.N.NotificationArn|String|否|acs:ess:cn-hangzhou:1111111111:queue/queue1|生命周期挂钩通知对象标识符。支持消息服务MNS队列和主题，参数取值格式：acs:ess:\{region\}:\{account-id\}:\{resource-relative-id\}。

 -   region：伸缩组所在的地域
-   account-id：阿里云账号ID

 例如：

 -   MNS队列：acs:ess:\{region\}:\{account-id\}:queue/\{queuename\}
-   MNS主题：acs:ess:\{region\}:\{account-id\}:topic/\{topicname\}

 |
|LifecycleHook.N.NotificationMetadata|String|否|Test|伸缩活动的等待状态的固定字符串信息。参数长度不能超过128个字符。

 弹性伸缩每次推送消息到通知对象时，会同时发送您预先指定的NotificationMetadata参数值，便于管理和标记不同类别的通知信息。当您同时指定了NotificationArn参数时，NotificationMetadata参数方可生效。

 |
|LifecycleHookName|String|否|test\_SCALE\_OUT|生命周期挂钩的名称。不能与当前伸缩组其他生命周期挂钩重名，长度为2~40个英文或中文字符，以数字、大小字母或中文开头，可包含数字、下划线（\_）、连字符（-）和点号（.）。

 默认值为生命周期挂钩ID。

 |
|NotificationArn|String|否|acs:ess:cn-hangzhou:1111111111:queue/queue1|生命周期挂钩通知对象标识符。支持消息服务MNS队列和主题，参数取值格式：acs:ess:\{region\}:\{account-id\}:\{resource-relative-id\}。

 -   region：伸缩组所在的地域
-   account-id：阿里云账号ID

 例如：

 -   MNS队列：acs:ess:\{region\}:\{account-id\}:queue/\{queuename\}
-   MNS主题：acs:ess:\{region\}:\{account-id\}:topic/\{topicname\}

 |
|NotificationMetadata|String|否|Test|伸缩活动的等待状态的固定字符串信息。参数长度不能超过128个字符。

 弹性伸缩每次推送消息到通知对象时，会同时发送您预先指定的NotificationMetadata参数值，便于管理和标记不同类别的通知信息。当您同时指定了NotificationArn参数时，NotificationMetadata参数方可生效。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|LifecycleHookId|String|ash-\*\*\*\*|生命周期挂钩的D。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=CreateLifecycleHook
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&LifecycleHookName=test_SCALE_OUT
&LifecycleTransition=SCALE_OUT
&NotificationArn=acs:ess:cn-hangzhou:1111111111:queue/queue1
&NotificationMetadata=Test
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateLifecycleHookResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <LifecycleHookId>ash-****</LifecycleHookId>
</CreateLifecycleHookResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"LifecycleHookId":"ash-****",
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
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

|InvalidParamter

|The specified value of parameter is not valid.

|参数值不合法。

|
|400

|InvalidNotificationArn

|The specified parameter notificationArn is invalid.

|指定的NotificationArn不合法。

|
|400

|UnsupportedNotificationType.CurrentRegion

|The notificationType is not supported in the special region which scalingGroup belongs to.

|当前地域不支持该通知方式。

|
|400

|QueueNotExist

|The specified queue does not exist.

|指定的MNS队列不存在。

|
|400

|TopicNotExist

|The specified topic does not exist.

|指定的MNS主题不存在。

|
|400

|InvalidLifecycleHookName.Duplicate

|The specified value of parameter lifecycleHookName is duplicated.

|生命周期挂钩已存在。

|
|400

|QuotaExceeded.LifecycleHook

|Lifecycle hook quota exceeded in the specified scaling group.

|一个伸缩组最多可以创建6个生命周期挂钩。

|

