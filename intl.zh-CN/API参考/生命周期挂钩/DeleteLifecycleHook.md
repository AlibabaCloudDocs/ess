# DeleteLifecycleHook {#doc_api_Ess_DeleteLifecycleHook .reference}

删除一个生命周期挂钩（DeleteLifecycleHook）。

## 描述 {#description .section}

如果生命周期挂钩已触发伸缩活动等待状态，删除生命周期挂钩时，则对应的等待状态会被提前结束。您可以通过以下两种方式删除生命周期挂钩：

-   指定生命周期挂钩 ID（`LifecycleHookId`），此时将忽略 `ScalingGroupId` 和 `LifecycleHookName` 参数。
-   同时指定伸缩组 ID（`ScalingGroupId`）与生命周期挂钩名称（`LifecycleHookName`）。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=DeleteLifecycleHook)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|DeleteLifecycleHook|系统规定参数，取值：DeleteLifecycleHook。

 |
|LifecycleHookId|String|否|ash-\*\*\*\*|生命周期挂钩 ID。

 |
|LifecycleHookName|String|否|测试SCALE\_IN|生命周期挂钩名称。

 |
|ScalingGroupId|String|否|dP8VqSd9ENXPc0ciVmbc\*\*\*\*|伸缩组 ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DeleteLifecycleHook
&LifecycleHookId=ash-****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteLifecycleHookResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DeleteLifecycleHookResponse>

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

|The specified value of parameter is invalid.

|参数值不合法。

|
|400

|InvalidLifecycleHookId.NotExist

|The specified lifecycleHookId does not exist.

|生命周期挂钩 ID 不存在。

|
|400

|InvalidLifecycleHookName.NotExist

|The specified lifecycleHookName you provided does not exist.

|生命周期挂钩名称不存在。

|

