# DetachLoadBalancers

调用DetachLoadBalancers移除一个或多个负载均衡实例。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DetachLoadBalancers&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DetachLoadBalancers|系统规定参数。取值：DetachLoadBalancers |
|LoadBalancer.N|RepeatList|是|lb-2zeur05gfs\*\*\*\*|负载均衡实例的ID，单次最多支持移除5台负载均衡实例。 |
|ScalingGroupId|String|是|asg-bp1ffogfdauy0jw0\*\*\*\*|伸缩组的ID。 |
|ForceDetach|Boolean|否|false|是否移除负载均衡实例后端服务器中属于当前伸缩组的ECS实例，取值范围：

 -   true：移除ECS实例。
-   false：不移除ECS实例。

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
https://ess.aliyuncs.com/?Action=DetachLoadBalancers
&ScalingGroupId=asg-bp1ffogfdauy0jw0****
&LoadBalancer.1=lb-2zeur05gfs****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DetachLoadBalancersResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DetachLoadBalancersResponse>
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
|404

|InvalidLoadBalancerId.NotFound

|The Load Balancer "%s" does not exist.

|伸缩组中不存在指定的负载均衡实例。 |

