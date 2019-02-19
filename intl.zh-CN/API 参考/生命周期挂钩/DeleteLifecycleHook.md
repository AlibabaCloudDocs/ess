# DeleteLifecycleHook {#concept_73841_zh .concept}

删除一个生命周期挂钩（`DeleteLifecycleHook`）。

## 描述 {#section_unj_njl_lgb .section}

如果生命周期挂钩已触发伸缩活动等待状态，删除生命周期挂钩时，则对应的等待状态会被提前结束。您可以通过以下两种方式删除生命周期挂钩：

-   指定生命周期挂钩 ID（`LifecycleHookId`），此时将忽略 `ScalingGroupId` 和 `LifecycleHookName` 参数。
-   同时指定伸缩组 ID（`ScalingGroupId`）与生命周期挂钩名称（`LifecycleHookName`）。

## 请求参数 { .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DeleteLifecycleHook。|
|LifecycleHookId|String|否|生命周期挂钩 ID。|
|ScalingGroupId|String|否|伸缩组 ID。|
|LifecycleHookName|String|否|生命周期挂钩名称。|

## 返回参数 { .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|请求 ID。|

## 示例 { .section}

请求示例

```
http://ess.aliyuncs.com/?Action=DeleteLifecycleHook
&LifecycleHookId=ash-xxxxxxxxxxx
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteLifecycleHookResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</DeleteLifecycleHookResponse>
```

`JSON` 格式

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 { .section}

以下为本接口特有的错误码。以下为本接口特有的错误码。对于所有接口的通用性错误，请参考 [客户端错误](intl.zh-CN/API 参考/错误代码/客户端错误.md#) 或 [服务器端错误](intl.zh-CN/API 参考/错误代码/服务器端错误.md#)。

|HttpCode|错误码|错误信息|描述|
|--------|:--|:---|:-|
|400|InvalidParamter|The specified value of parameter is invalid.|参数值不合法。|
|400|InvalidLifecycleHookId.NotExist|The specified lifecycleHookId does not exist.|生命周期挂钩 ID 不存在。|
|400|InvalidLifecycleHookName.NotExist|The specified lifecycleHookName you provided does not exist.|生命周期挂钩名称不存在。|

