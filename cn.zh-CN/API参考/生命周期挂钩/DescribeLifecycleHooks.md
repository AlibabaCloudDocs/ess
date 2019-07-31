# DescribeLifecycleHooks {#doc_api_Ess_DescribeLifecycleHooks .reference}

调用DescribeLifecycleHooks查询生命周期挂钩。

## 接口说明 {#description .section}

您可以通过以下三种方式查询生命周期挂钩：

-   指定一个生命周期挂钩ID列表（LifecycleHookId.N），此时将忽略ScalingGroupId和LifecycleHookName参数。
-   指定伸缩组ID（ScalingGroupId）。
-   同时指定伸缩组ID（ScalingGroupId）和生命周期挂钩名称（LifecycleHookName）。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DescribeLifecycleHooks&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|DescribeLifecycleHooks|系统规定参数，取值：DescribeLifecycleHooks。

 |
|LifecycleHookId.N|RepeatList|否|ash-\*\*\*\*|生命周期挂钩的ID。

 |
|LifecycleHookName|String|否|Test|生命周期挂钩的名称。

 |
|PageNumber|Integer|否|1|实例状态列表的页码。起始值：1。

 默认值：1。

 |
|PageSize|Integer|否|50|分页查询时设置的每页行数。最大值：50。

 默认值：50。

 |
|ScalingGroupId|String|否|asg-\*\*\*\*|伸缩组的ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|LifecycleHooks| | |生命周期挂钩信息列表。

 |
|DefaultResult|String|CONTINUE|等待状态结束后的下一步动作。

 |
|HeartbeatTimeout|Integer|60|生命周期挂钩为伸缩组活动设置的等待时间，等待状态超时后会执行下一步动作。

 |
|LifecycleHookId|String|ash-\*\*\*\*|生命周期挂钩ID。

 |
|LifecycleHookName|String|Test|生命周期挂钩名称。

 |
|LifecycleTransition|String|SCALE\_OUT|生命周期挂钩对应伸缩活动类型。

 |
|NotificationArn|String|acs:ess:cn-hangzhou:1111111111:queue/queue1|生命周期挂钩通知对象标识符。

 |
|NotificationMetadata|String|Test|伸缩活动的等待状态的固定字符串信息。

 |
|ScalingGroupId|String|asg-\*\*\*\*|伸缩组ID。

 |
|PageNumber|Integer|1|查询起始页数。

 |
|PageSize|Integer|50|查询每页返回行数。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

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
            <ScalingGroupId>asg-****</ScalingGroupId>
            <LifecycleHookId>ash-****</LifecycleHookId>
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
	"PageNumber":"1",
	"TotalCount":"1",
	"PageSize":"50",
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"LifecycleHooks":{
		"LifecycleHook":{
			"NotificationArn":"acs:ess:cn-hangzhou:1111111111:queue/queue1",
			"LifecycleTransition":"SCALE_OUT",
			"LifecycleHookId":"ash-****",
			"ScalingGroupId":"asg-****",
			"DefaultResult":"CONTINUE",
			"HeartbeatTimeout":"60",
			"NotificationMetadata":"Test",
			"LifecycleHookName":"Test"
		}
	}
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

|指定的参数值不合法。

|

