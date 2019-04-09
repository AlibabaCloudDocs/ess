# ExitStandby {#doc_api_1163345 .reference}

运行伸缩组内的处于备用状态的 ECS 实例（\`ExitStandby\`）。

## 描述 {#description .section}

如果伸缩组设置了负载均衡服务，则会将权重设置伸缩配置定义的权重值。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=ExitStandby)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId.N|RepeatList|是|i-28wt4\*\*\*\*|ECS 实例 ID。取值可以由多个实例 ID 组成一个 JSON 数组，最多支持 20 个 ID，ID 之间用半角逗号（,）隔开。

 |
|ScalingGroupId|String|是|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组 ID。

 |
|Action|String|否|ExitStandby|系统规定参数。取值：ExitStandby。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=ExitStandby
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&InstanceId.1=i-28wt4****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ExitStandbyResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ExitStandbyResponse>

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
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|RAM用户无权限调用该接口。请联系主账号授权后重试。

|
|404

|InvalidInstanceId.NotFound

|A required authorization for the specified action is not supplied.

|指定的ECS实例不存在。

|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|指定的伸缩组在该用户账号下不存在。

|

