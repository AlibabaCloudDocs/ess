# DescribeLifecycleHooks {#doc_api_1163758 .reference}

查询一个或多个满足指定条件的生命周期挂钩列表（\`DescribeLifecycleHooks\`）。

## 描述 {#description .section}

您可以通过以下三种方式查询生命周期挂钩：

-   指定一个生命周期挂钩 ID 列表（`LifecycleHookId.N`），此时将忽略 `ScalingGroupId` 和 `LifecycleHookName` 参数。
-   指定伸缩组 ID（`ScalingGroupId`）。
-   同时指定伸缩组 ID（`ScalingGroupId`）和生命周期挂钩名称（`LifecycleHookName`）。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=DescribeLifecycleHooks)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|DescribeLifecycleHooks|系统规定参数，取值：DescribeLifecycleHooks

 |
|LifecycleHookId.N|RepeatList|否|ash-\*\*\*\*|生命周期挂钩 ID。

 |
|LifecycleHookName|String|否|Test|生命周期挂钩名称。

 |
|PageNumber|Integer|否|1|实例状态列表的页码。起始值：1，默认值：1。

 |
|PageSize|Integer|否|50|分页查询时设置的每页行数。最大值：50，默认值：50。

 |
|ScalingGroupId|String|否|asg-\*\*\*\*|伸缩组 ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|LifecycleHooks| | |生命周期挂钩信息列表。

 |
|└DefaultResult|String|CONTINUE|等待状态结束后的下一步动作。

 |
|└HeartbeatTimeout|Integer|60|生命周期挂钩为伸缩组活动设置的等待时间，等待状态超时后会执行下一步动作。

 |
|└LifecycleHookId|String|ash-\*\*\*\*|生命周期挂钩 ID。

 |
|└LifecycleHookName|String|Test|生命周期挂钩名称。

 |
|└LifecycleTransition|String|SCALE\_OUT|生命周期挂钩对应伸缩活动类型。

 |
|└NotificationArn|String|acs:ess:cn-hangzhou:1111111111:queue/queue1|生命周期挂钩通知对象标识符。

 |
|└NotificationMetadata|String|Test|伸缩活动的等待状态的固定字符串信息。

 |
|└ScalingGroupId|String|asg-\*\*\*\*|伸缩组 ID。

 |
|PageNumber|Integer|1|查询起始页数。

 |
|PageSize|Integer|50|查询每页返回行数。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |
|TotalCount|Integer|1|生命周期挂钩总个数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DescribeLifecycleHooks
&ScalingGroupId=asg-****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeLifecycleHooksResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
  <PageNumber>1</PageNumber>
  <PageSize>50</PageSize>
  <TotalCount>1</TotalCount>
  <LifecycleHooks>
    <LifecycleHook>
      <ScalingGroupId>asg-xxx</ScalingGroupId>
      <LifecycleHookId>ash-xxx</LifecycleHookId>
      <LifecycleHookName>Test</LifecycleHookName>
      <DefaultResult>CONTINUE</DefaultResult>
      <HeartbeatTimeout>60</HeartbeatTimeout>
      <LifecycleTransition>SCALE_OUT</LifecycleTransition>
      <NotificationMetadata>Test</NotificationMetadata>
      <NotificationArn>acs:ess:cn-hangzhou:1111111111:queue/queue1</NotificationArn>
    </LifecycleHook>
  </LifecycleHooks>
</DescribeLifecycleHooksResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"lifecycleHooks":[
		{
			"notificationArn":"acs:ess:cn-hangzhou:1111111111:queue/queue1",
			"lifecycleHookId":"ash-****",
			"notificationMetadata":"Test",
			"lifecycleTransition":"SCALE_OUT",
			"defaultResult":"CONTINUE",
			"lifecycleHookName":"Test",
			"scalingGroupId":"asg-****",
			"heartbeatTimeout":600
		}
	],
	"totalCount":1,
	"requestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"pageSize":50,
	"pageNumber":1
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

