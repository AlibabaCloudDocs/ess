# DeleteLifecycleHook {#doc_api_Ess_DeleteLifecycleHook .reference}

调用DeleteLifecycleHook删除一个生命周期挂钩。

## 接口说明 {#description .section}

如果生命周期挂钩已触发伸缩活动等待状态，删除生命周期挂钩时，对应的等待状态会被提前结束。您可以通过以下两种方式删除生命周期挂钩：

-   指定生命周期挂钩ID（LifecycleHookId），此时将忽略ScalingGroupId和LifecycleHookName参数。
-   同时指定伸缩组ID（ScalingGroupId）与生命周期挂钩名称（LifecycleHookName）。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DeleteLifecycleHook&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|DeleteLifecycleHook|系统规定参数，取值：DeleteLifecycleHook。

 |
|LifecycleHookId|String|否|ash-\*\*\*\*|生命周期挂钩的ID。

 |
|LifecycleHookName|String|否|测试SCALE\_IN|生命周期挂钩的名称。

 |
|ScalingGroupId|String|否|dP8VqSd9ENXPc0ciVmbc\*\*\*\*|伸缩组的ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

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

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

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

|生命周期挂钩ID不存在。

|
|400

|InvalidLifecycleHookName.NotExist

|The specified lifecycleHookName you provided does not exist.

|生命周期挂钩名称不存在。

|

