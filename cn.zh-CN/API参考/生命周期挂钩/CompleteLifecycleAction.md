# CompleteLifecycleAction {#doc_api_Ess_CompleteLifecycleAction .reference}

提前结束伸缩活动的等待状态（CompleteLifecycleAction）。

允许设置结束等待状态后的下一步动作是继续完成伸缩活动（`CONTINUE`）还是弃用此次伸缩活动（`ABANDON`）。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=CompleteLifecycleAction)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|LifecycleActionToken|String|是|aaaa-bbbbb-cccc-ddddd|伸缩活动的等待状态标识符，您可以从生命周期挂钩指定的消息服务队列或主题中获取。

 |
|LifecycleHookId|String|是|ash-\*\*\*\*|生命周期挂钩 ID。

 |
|Action|String|否|CompleteLifecycleAction|系统规定参数，取值：CompleteLifecycleAction。

 |
|LifecycleActionResult|String|否|CONTINUE|等待状态结束后的下一步动作。取值范围：

 -   CONTINUE：继续响应弹性扩张活动或者继续响应弹性收缩活动。
-   ABANDON：直接释放弹性扩张活动创建出来的 ECS 实例或者直接将弹性收缩活动中的 ECS 实例从伸缩组移除。

 默认值：CONTINUE

 当伸缩组发生弹性收缩活动（`SCALE_IN`）并触发多个生命周期挂钩时，`DefaultResult=ABANDON` 的生命周期挂钩触发的等待状态结束时，会提前将其它对应的等待状态提前结束。其他情况下，下一步动作均以最后一个结束等待状态的下一步动作为准。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM 用户的账号登录名称。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=CompleteLifecycleAction
&LifecycleHookId=ash-****
&LifecycleActionToken=aaaa-bbbbb-cccc-ddddd
&LifecycleActionResult=CONTINUE
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CompleteLifecycleActionResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</CompleteLifecycleActionResponse>

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

|指定的参数值不合法。

|
|400

|LifecycleHookIdAndLifecycleActionToken.Invalid

|The specified lifecycleActionToken and lifecycleHookId you provided does not match any in process lifecycle action.

|根据指定的 LifecycleActionToken 无法匹配 LifecycleHookId。

|

