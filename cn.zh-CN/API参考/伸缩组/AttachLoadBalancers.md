# AttachLoadBalancers {#doc_api_1163783 .reference}

添加一个或多个负载均衡实例。

## 描述 {#description .section}

由于存在 [使用限制](~~32459~~)，向伸缩组添加负载均衡实例时需要满足以下条件：

-   负载均衡实例与伸缩组必须属于同一账号。
-   负载均衡实例与伸缩组必须处于同一地域。
-   负载均衡实例必须处于运行中状态。
-   负载均衡实例至少配置有一个监听且必须开启健康检查。
-   如果负载均衡实例与伸缩组的网络类型均为 VPC，必须处于同一 VPC。
-   当伸缩组的网络类型为 VPC，负载均衡实例的网络类型为经典网络时，如果负载均衡实例后端服务器中包含 VPC 实例，该实例必须与伸缩组处于同一 VPC。
-   添加的负载均衡实例个数必须少于伸缩组的实例配额。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=AttachLoadBalancers)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|LoadBalancer.N|RepeatList|是|lb-2zeur05gfs\*\*\*\*|负载均衡实例 ID，单次最多支持添加 5 个负载均衡实例。

 |
|ScalingGroupId|String|是|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组 ID。

 |
|Action|String|否|AttachLoadBalancers|操作接口名，系统规定参数，取值：AttachLoadBalancers。

 |
|ForceAttach|Boolean|否|false|是否把当前伸缩组内的实例全部添加到负载均衡后端服务器：

 -   true：添加
-   false：不添加

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

http://ess.aliyuncs.com/?Action=AttachLoadBalancers
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&LoadBalancer.1=lb-2zeur05gfs****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AttachLoadBalancersResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</AttachLoadBalancersResponse>

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
|400

|QuotaExceeded.LoadBalancer

|LoadBalancer quota exceeded in the scaling group "%s".

|伸缩组中负载均衡实例超出配额限制。

|
|404

|InvalidLoadBalancerId.NotFound

|The load balancer "%s" does not exist.

|不存在指定的负载均衡实例。

|
|400

|InvalidLoadBalancerId.RegionMismatch

|The load balancer "%s" and the specified scaling group are not in the same Region.

|负载均衡实例与伸缩组不在同一地域。

|
|400

|IncorrectLoadBalancerStatus

|The current status of the load balancer "%s" does not support this action.

|当前负载均衡实例状态不支持此操作。

|
|400

|IncorrectLoadBalancerHealthCheck

|The current health check type of the load balancer "%s" does not support this action.

|当前负载均衡实例未开启健康检查。

|
|400

|InvalidLoadBalancerId.VPCMismatch

|The specified virtual switch and the instance in the load balancer "%s" are not in the same VPC.

|负载均衡实例与伸缩组不在同一 VPC 下。

|
|400

|QuotaExceeded.BackendServer

|Backend server quota exceeded in the load balancer "%s".

|负载均衡实例后端服务器数量超出限额。

|
|404

|InvalidScalingConfigurationId.NotFound

|The specified scaling configuration does not exist.

|未找到当前伸缩组启用的伸缩配置。

|

