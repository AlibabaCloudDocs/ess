# AttachLoadBalancers

调用AttachLoadBalancers添加一个或多个负载均衡实例。

## 接口说明

向伸缩组添加负载均衡实例时需要满足以下条件：

-   负载均衡实例与伸缩组必须属于同一账号。
-   负载均衡实例与伸缩组必须处于同一地域。
-   负载均衡实例必须处于运行中状态。
-   负载均衡实例至少配置有一个监听且必须开启健康检查。
-   如果负载均衡实例与伸缩组的网络类型均为VPC，必须处于同一VPC。
-   当伸缩组的网络类型为VPC，负载均衡实例的网络类型为经典网络时，如果负载均衡实例后端服务器中包含VPC实例，该实例必须与伸缩组处于同一VPC。
-   不超过伸缩组关联负载均衡实例的限额，具体限额请参见[使用限制](~~25863~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=AttachLoadBalancers&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AttachLoadBalancers|系统规定参数。取值：AttachLoadBalancers |
|LoadBalancer.N|RepeatList|是|lb-2zeur05gfs\*\*\*\*|负载均衡实例的ID，N的取值范围：1~5。 |
|ScalingGroupId|String|是|asg-bp1avr6ensitts3w\*\*\*\*|伸缩组的ID。 |
|ForceAttach|Boolean|否|false|是否把当前伸缩组内的实例全部添加为负载均衡实例的后端服务器，取值范围：

 -   true：添加
-   false：不添加

 默认值：false |
|ClientToken|String|否|123e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25965~~)。 |
|Async|Boolean|否|false|添加负载均衡实例时，是否采用异步调用的方式。异步调用能保证操作的事务性，即所有操作都执行成功或者某个操作失败时所有操作的执行结果都不生效，建议您采用异步调用。

 取值范围：

 -   true：异步调用。请求将返回伸缩活动的ID。
-   false：同步调用。

 默认值：false |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|ScalingActivityId|String|asa-bp140qd7mak8k63f\*\*\*\*|伸缩活动的ID。

 仅当Async=true时返回该值。您可使用API [DescribeScalingActivities](~~25961~~)遍历查询返回的伸缩活动ID，查看伸缩活动的执行状态。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=AttachLoadBalancers
&ScalingGroupId=asg-bp1avr6ensitts3w****
&LoadBalancer.1=lb-2zeur05gfs****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<AttachLoadBalancersResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</AttachLoadBalancersResponse>
```

`JSON`格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|您并未授予弹性伸缩完整的OpenAPI调用权限。 |
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|账号下不存在指定的伸缩组。 |
|400

|QuotaExceeded.LoadBalancer

|LoadBalancer quota exceeded in the scaling group "%s".

|伸缩组中负载均衡实例超出配额限制。 |
|404

|InvalidLoadBalancerId.NotFound

|The load balancer "%s" does not exist.

|不存在指定的负载均衡实例。 |
|400

|InvalidLoadBalancerId.RegionMismatch

|The load balancer "%s" and the specified scaling group are not in the same Region.

|负载均衡实例与伸缩组不在同一地域。 |
|400

|IncorrectLoadBalancerStatus

|The current status of the load balancer "%s" does not support this action.

|当前负载均衡实例状态不支持此操作。 |
|400

|IncorrectLoadBalancerHealthCheck

|The current health check type of the load balancer "%s" does not support this action.

|当前负载均衡实例未开启健康检查。 |
|400

|InvalidLoadBalancerId.VPCMismatch

|The specified virtual switch and the instance in the load balancer "%s" are not in the same VPC.

|负载均衡实例与伸缩组不在同一VPC下。 |
|400

|QuotaExceeded.BackendServer

|Backend server quota exceeded in the load balancer "%s".

|负载均衡实例后端服务器数量超出限额。 |
|404

|InvalidScalingConfigurationId.NotFound

|The specified scaling configuration does not exist.

|未找到当前伸缩组启用的伸缩配置。 |

