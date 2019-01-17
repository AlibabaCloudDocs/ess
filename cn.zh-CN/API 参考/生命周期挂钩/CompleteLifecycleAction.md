# CompleteLifecycleAction {#concept_73847_zh .concept}

提前结束伸缩活动的等待状态（`CompleteLifecycleAction`）。

## 描述 {#section_ems_3jl_lgb .section}

允许设置结束等待状态后的下一步动作是继续完成伸缩活动（`CONTINUE`）还是弃用此次伸缩活动（`ABANDON`）。

## 请求参数 {#section_jqw_qsl_sfb .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：CompleteLifecycleAction。|
|LifecycleHookId|String|是|生命周期挂钩 ID。|
|LifecycleActionToken|String|是|伸缩活动的等待状态标识符，您可以从生命周期挂钩指定的消息服务队列或主题中获取。|
|LifecycleActionResult|String|否|等待状态结束后的下一步动作。取值范围：-   CONTINUE：继续响应弹性扩张活动或者继续响应弹性收缩活动。
-   ABANDON：直接释放弹性扩张活动创建出来的 ECS 实例或者直接将弹性收缩活动中的 ECS 实例从伸缩组移除。

默认值：CONTINUE

当伸缩组发生弹性收缩活动（`SCALE_IN`）并触发多个生命周期挂钩时，`DefaultResult=ABANDON` 的生命周期挂钩触发的等待状态结束时，会提前将其它对应的等待状态提前结束。其他情况下，下一步动作均以最后一个结束等待状态的下一步动作为准。

|

## 返回参数 { .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|请求 ID。|

## 示例 { .section}

请求示例

```
http://ess.aliyuncs.com/?Action=CompleteLifecycleAction
&LifecycleHookId=ash-xxxxxxxxxxx
&LifecycleActionToken=aaaa-bbbbb-cccc-ddddd
&LifecycleActionResult=CONTINUE
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CompleteLifecycleActionResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</CompleteLifecycleActionResponse>
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
|400|InvalidParamter|The specified value of parameter is invalid.|指定的参数值不合法。|
|400|LifecycleHookIdAndLifecycleActionToken.Invalid|The specified lifecycleActionToken and lifecycleHookId you provided does not match any in process lifecycle action.|根据指定的 `LifecycleActionToken` 无法匹配 `LifecycleHookId`。|

