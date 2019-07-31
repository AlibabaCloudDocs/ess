# AttachVServerGroups {#doc_api_Ess_AttachVServerGroups .reference}

调用AttachVServerGroups添加负载均衡实例下的一个或者多个虚拟服务器组。

## 接口说明 {#description .section}

由于负载均衡存在[使用限制](~~32459~~)，向伸缩组添加虚拟服务器组时需要满足以下条件：

-   负载均衡实例与伸缩组必须属于同一账号。
-   负载均衡实例与伸缩组必须处于同一地域。
-   负载均衡实例必须处于运行中状态。
-   负载均衡实例至少配置有一个监听且必须开启健康检查。
-   如果负载均衡实例与伸缩组的网络类型均为VPC，必须处于同一VPC。
-   当伸缩组的网络类型为VPC，负载均衡实例的网络类型为经典网络时，如果虚拟服务器组包含VPC实例，该实例必须与伸缩组处于同一VPC。
-   待添加虚拟服务器组必须属于对应的负载均衡实例。
-   目前，伸缩组内虚拟服务器组的限额为5。

    **说明：** 

    注意：确定伸缩组内虚拟服务器组的方式为：负载均衡实例ID（LoadBalancerId）

    -   虚拟服务器组ID（VServerGroupId）
    -   虚拟服务器组端口号（Port） 。如果通过不同的端口号将同一虚拟服务器组添加至伸缩组，视为伸缩组内添加了多个虚拟服务器组。如果请求参数中存在重复的虚拟服务器组ID
    -   端口号，默认使用最先配置的一组，忽略其余虚拟服务器组。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=AttachVServerGroups&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|伸缩组所属地域的ID，如cn-hangzhou、cn-shanghai。更多详情，请参见[地域和可用区](~~40654~~)。

 |
|ScalingGroupId|String|是|asg-\*\*\*\*|伸缩组的ID。

 |
|Action|String|否|AttachVServerGroups|系统规定参数，取值： AttachVServerGroups。

 |
|ForceAttach|Boolean|否|false|是否将当前伸缩组内的ECS实例添加到新增的虚拟服务器组。

 -   true：添加
-   false：不添加

 默认值：false。

 |
|VServerGroup.N.LoadBalancerId|String|否|lb-\*\*\*\*|虚拟服务器组所属负载均衡实例的ID。N为负载均衡实例编号，取值范围：1~5。

 |
|VServerGroup.N.VServerGroupAttribute.N.Port|Integer|否|22|弹性伸缩将ECS实例添加到虚拟服务器组时使用的端口号，取值范围：1~65535。

 N为负载均衡实例编号，取值范围：1~5。

 M为负载均衡实例下虚拟服务器组的编号，取值范围：1~5。

 |
|VServerGroup.N.VServerGroupAttribute.N.VServerGroupId|String|否|rsp-\*\*\*\*|虚拟服务器组的ID。N为负载均衡实例编号，取值范围：1~5。

 M为负载均衡实例下虚拟服务器组的编号，取值范围：1~5。

 |
|VServerGroup.N.VServerGroupAttribute.N.Weight|Integer|否|100|弹性伸缩将ECS实例添加到虚拟服务器组时设置的权重，取值范围：0~100。

 默认值：50。

 N为负载均衡实例编号，取值范围：1~5。

 M为负载均衡实例下虚拟服务器组的编号，取值范围：1~5。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=AttachVServerGroups
&ScalingGroupId=asg-****
&RegionId=cn-hangzhou
&VServerGroup.1.LoadBalancerId=lb-****
&VServerGroup.1.VServerGroupAttribute.1.VServerGroupId=rsp-****
&VServerGroup.1.VServerGroupAttribute.1.Port=22
&VServerGroup.1.VServerGroupAttribute.1.Weight=100
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AttachVServerGroupsResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</AttachVServerGroupsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
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
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|您未授予弹性伸缩完整的Open API调用权限。

|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|账号下不存在指定的伸缩组。

|
|404

|InvalidLoadBalancerId.NotFound

|The load balancer "%s" does not exist.

|账号下不存在指定的负载均衡实例。

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

|负载均衡实例与伸缩组不在同一VPC下。

|
|400

|InvalidVServerGroupId.ForLoadBalancer

|Invalid VServerGroupId For LoadBalancer "%s".

|VServerGroupId对应的虚拟服务器组不属于指定的负载均衡实例。

|
|400

|QuotaExceeded.VServerGroup

|VServerGroup quota exceeded in the specified scaling group.

|当前伸缩组内可配置的虚拟服务器组个数达到上限。

|

