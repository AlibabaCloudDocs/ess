# RecordLifecycleActionHeartbeat {#concept_73846_zh .concept}

延长一个生命周期挂钩触发的被挂起的 ECS 实例的等待时间（`RecordLifecycleActionHeartbeat`）。

## 描述 {#section_xly_djl_lgb .section}

ECS 实例的等待时间最长不能超过 6 小时，每次等待状态最多能被延时 20 次。

## 请求参数 {#section_lll_nrl_sfb .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：RecordLifecycleActionHeartbeat|
|LifecycleHookId|String|是|生命周期挂钩 ID。|
|LifecycleActionToken|String|是|伸缩活动的等待状态标识符，您可以从生命周期挂钩指定的消息服务队列或主题中获取。|
|HeartbeatTimeout|Integer|否|生命周期挂钩为伸缩组活动设置的等待时间，等待状态超时后会执行下一步动作。取值范围：\[30, 21600\]，单位为秒，默认值：600。创建了生命周期挂钩后，您可以调用 RecordLifecycleActionHeartbeat 延长 ECS 实例的等待时间，也可以调用 [CompleteLifecycleAction](cn.zh-CN/API 参考/生命周期挂钩/CompleteLifecycleAction.md#) 提前结束伸缩活动的等待状态。

|

## 返回参数 { .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|请求 ID。|

## 示例 { .section}

请求示例

```
http://ess.aliyuncs.com/?Action=RecordLifecycleActionHeartbeat
&LifecycleHookId=ash-xxxxxxxxxxx
&LifecycleActionToken=aaaa-bbbbb-cccc-ddddd
&LifecycleActionResult=CONTINUE
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<RecordLifecycleActionHeartbeatResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</RecordLifecycleActionHeartbeatResponse>
```

`JSON` 格式

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 { .section}

以下为本接口特有的错误码。以下为本接口特有的错误码。对于所有接口的通用性错误，请参考 [客户端错误](cn.zh-CN/API 参考/错误代码/客户端错误.md#) 或 [服务器端错误](cn.zh-CN/API 参考/错误代码/服务器端错误.md#)。

|HttpCode|错误码|错误信息|描述|
|--------|:--|:---|:-|
|400|InvalidParamter|The specified value of parameter is not valid.|指定的参数值不合法。|
|400|LifecycleHookIdAndLifecycleActionToken.Invalid|The specified lifecycleActionToken and lifecycleHookId you provided does not match any in process lifecycle action.|根据指定的 `LifecycleActionToken` 无法匹配 `LifecycleHookId`。|
|400|LifecycleAction.TimeExceeded|The specified parameter heartbeatTime exceed lifecycleAction max suspend time.|等待时间最长不能超过 6 小时。|
|400|LifecycleAction.RecordTimesExceeded|The specified lifecycleAction exceed lifecycleAction max record times.|每次等待状态最多能被延时 20 次。|

