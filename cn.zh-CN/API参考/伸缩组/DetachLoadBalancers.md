# DetachLoadBalancers {#doc_api_1163784 .reference}

移除一个或多个负载均衡实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=DetachLoadBalancers)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|LoadBalancer.N|RepeatList|是|lb-2zeur05gfs\*\*\*\*|负载均衡实例 ID，单次最多支持移除 5 个负载均衡实例。

 |
|ScalingGroupId|String|是|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组 ID。

 |
|Action|String|否|DetachLoadBalancers|操作接口名，系统规定参数，取值：DetachLoadBalancers。

 |
|ForceDetach|Boolean|否|false|是否移除负载均衡实例后端服务器中属于伸缩组的实例：

 -   true：移除
-   false：不移除

 默认值：false

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DetachLoadBalancers
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&LoadBalancer.1=lb-2zeur05gfs****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DetachLoadBalancersResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E
</RequestId>
</DetachLoadBalancersResponse>

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

|您并未授予弹性伸缩完整的 Open API 调用权限。

|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|账号下不存在指定的伸缩组。

|
|404

|InvalidLoadBalancerId.NotFound

|The Load Balancer "%s" does not exist.

|伸缩组中不存在指定的负载均衡实例。

|

