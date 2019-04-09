# RecordLifecycleActionHeartbeat {#doc_api_1163759 .reference}

延长一个生命周期挂钩触发的被挂起的 ECS 实例的等待时间（\`RecordLifecycleActionHeartbeat\`）。

## 描述 {#description .section}

ECS 实例的等待时间最长不能超过 6 小时，每次等待状态最多能被延时 20 次。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=RecordLifecycleActionHeartbeat)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|lifecycleActionToken|String|是|aaaa-bbbbb-cccc-ddddd|伸缩活动的等待状态标识符，您可以从生命周期挂钩指定的消息服务队列或主题中获取。

 |
|lifecycleHookId|String|是|ash-\*\*\*\*|生命周期挂钩 ID。

 |
|Action|String|否|RecordLifecycleActionHeartbeat|系统规定参数，取值：RecordLifecycleActionHeartbeat。

 |
|heartbeatTimeout|Integer|否|600|命周期挂钩为伸缩组活动设置的等待时间，等待状态超时后会执行下一步动作。取值范围：30~21600，单位为秒，默认值：600。

 创建了生命周期挂钩后，您可以调用 RecordLifecycleActionHeartbeat 延长 ECS 实例的等待时间，也可以调用 [CompleteLifecycleAction](~~73847~~) 提前结束伸缩活动的等待状态。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=RecordLifecycleActionHeartbeat
&LifecycleHookId=ash-****
&LifecycleActionToken=aaaa-bbbbb-cccc-ddddd
&LifecycleActionResult=CONTINUE
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RecordLifecycleActionHeartbeatResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</RecordLifecycleActionHeartbeatResponse>

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

|指定的参数值不合法。

|
|400

|LifecycleHookIdAndLifecycleActionToken.Invalid

|The specified lifecycleActionToken and lifecycleHookId you provided does not match any in process lifecycle action.

|根据指定的

`LifecycleActionToken`无法匹配

`LifecycleHookId`。

|
|400

|LifecycleAction.TimeExceeded

|The specified parameter heartbeatTime exceed lifecycleAction max suspend time.

|等待时间最长不能超过 6 小时。

|
|400

|LifecycleAction.RecordTimesExceeded

|The specified lifecycleAction exceed lifecycleAction max record times.

|每次等待状态最多能被延时 20 次。

|

