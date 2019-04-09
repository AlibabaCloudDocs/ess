# ModifyLifecycleHook {#doc_api_1163748 .reference}

修改一个生命周期挂钩的属性（\`ModifyLifecycleHook\`）。

## 描述 {#description .section}

您可以通过以下两种方式修改生命周期挂钩：

-   指定生命周期挂钩 ID（`LifecycleHookId`），此时将忽略 `ScalingGroupId` 和 `LifecycleHookName` 参数。
-   同时指定伸缩组 ID（`ScalingGroupId`）与生命周期挂钩名称（`LifecycleHookName`）。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=ModifyLifecycleHook)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|ModifyLifecycleHook|系统规定参数，取值：ModifyLifecycleHook。

 |
|DefaultResult|String|否|CONTINUE|等待状态结束后的下一步动作。取值范围：

 -   CONTINUE：继续响应弹性扩张活动或者继续响应弹性收缩活动。
-   ABANDON：直接释放弹性扩张活动创建出来的 ECS 实例或者直接将弹性收缩活动中的 ECS 实例从伸缩组移除。

 默认值：CONTINUE

 当伸缩组发生弹性收缩活动（`SCALE_IN`）并触发多个生命周期挂钩时，`DefaultResult=ABANDON` 的生命周期挂钩触发的等待状态结束时，会提前将其它对应的等待状态提前结束。其他情况下，下一步动作均以最后一个结束等待状态的下一步动作为准。

 |
|HeartbeatTimeout|Integer|否|600|生命周期挂钩为伸缩组活动设置的等待时间，等待状态超时后会执行下一步动作。取值范围：30~21600，单位为秒，默认值：600。

 创建了生命周期挂钩后，您可以调用 [RecordLifecycleActionHeartbeat](~~73846~~) 延长 ECS 实例的等待时间，也可以调用 [CompleteLifecycleAction](~~73847~~) 提前结束伸缩活动的等待状态。

 |
|LifecycleHookId|String|否|ash-\*\*\*|生命周期挂钩 ID，用于指定生命周期挂钩，不支持修改。

 |
|LifecycleHookName|String|否|测试SCALE\_IN|生命周期挂钩名称，用于指定生命周期挂钩，不支持修改。

 |
|LifecycleTransition|String|否|SCALE\_IN|生命周期挂钩适用的伸缩活动类型。取值范围：

 -   SCALE\_OUT：伸缩组弹性扩张活动
-   SCALE\_IN：伸缩组弹性收缩活动

 |
|NotificationArn|String|否|acs:ess:cn-hangzhou:1111111111:queue/queue2|生命周期挂钩通知对象标识符。目前我们支持消息服务 MNS 队列或主题，参数取值格式：acs:ess:\{region\}:\{account-id\}:\{resource-relative-id\}。

 -   `region`：伸缩组所在的地域
-   `account-id`：阿里云账号 ID

 例如：

 -   MNS 队列：acs:ess:\{region\}:\{account-id\}:queue/\{queuename\}
-   MNS 主题：acs:ess:\{region\}:\{account-id\}:topic/\{topicname\}

 |
|NotificationMetadata|String|否|Test|伸缩活动的等待状态的固定字符串信息。参数长度不能超过 128 个字符。弹性伸缩每次推送消息到通知对象时，会同时发送您预先指定的 `NotificationMetadata` 参数值，便于管理和标记不同类别的通知信息。当您同时指定了 `NotificationArn` 参数时，`NotificationMetadata` 参数方可生效。

 |
|ScalingGroupId|String|否|AG6CQdPU8OKdwLjgZcJ2\*\*\*|伸缩组 ID，用于指定生命周期挂钩，不支持修改。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=ModifyLifecycleHook
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&LifecycleHookName=测试SCALE_IN
&LifecycleTransition=SCALE_IN
&DefaultResult=ABANDON
&NotificationArn=acs:ess:cn-hangzhou:1111111111:queue/queue2
&NotificationMetadata=Test
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyLifecycleHookResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyLifecycleHookResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
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

|InvalidParamter

|The specified value of parameter is not valid.

|参数值不合法。

|
|400

|InvalidLifecycleHookId.NotExist

|The specified lifecycleHookId not exist.

|指定的

`LifecycleHookId`不存在。

|
|400

|InvalidLifecycleHookName.NotExist

|The specified lifecycleHookName you provided not exist.

|指定的

`LifecycleHookName`不存在。

|
|400

|InvalidNotificationArn

|The specified parameter \*\*notificationArn\*\* is invalid.

|指定的

`NotificationArn`不存在。

|
|400

|UnsupportedNotificationType.CurrentRegion

|The \*\*notificationType\*\* is not supported in the special region which scalingGroup belongs to.

|当前地域不支持该通知方式。

|
|400

|LifecycleHook

|The specified queue does not exist.

|指定的 MNS 队列不存在。

|
|400

|TopicNotExist

|The specified topic does not exist.

|指定的 MNS 主题不存在。

|

