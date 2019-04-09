# DetachVServerGroups {#doc_api_Ess_DetachVServerGroups .reference}

您可以通过 DetachVServerGroups 移除一个或者多个虚拟服务器组。

## 描述 {#description .section}

确定待移除虚拟服务器组的方式为：负载均衡实例ID（**LoadBalancerId**）

-   虚拟服务器组ID（**VServerGroupId**）
-   虚拟服务器组端口号（**Port**） 。如果请求参数中的虚拟服务器组与伸缩组中的虚拟服务器组相匹配，则移除该虚拟服务器组；如果未能匹配，则忽略移除请求，接口不报错。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=DetachVServerGroups)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|伸缩组所属的地域 ID，如 cn-hangzhou、cn-shanghai。更多详情，请参阅 [地域和可用区](~~40654~~)。

 |
|ScalingGroupId|String|是|asg-\*\*\*\*|伸缩组 ID。

 |
|Action|String|否|DetachVServerGroups|操作接口名，系统规定参数，取值： DetachVServerGroups。

 |
|ForceDetach|Boolean|否|false|是否从待移除虚拟服务器组中移除当前伸缩组内的ECS实例。

 -   true：移除
-   false：不移除

 默认值：false

 |
|VServerGroup.N.LoadBalancerId|String|否|lb-\*\*\*\*|虚拟服务器组所属负载均衡实例的 ID。N 为负载均衡实例编号，取值范围：1~5。

 |
|VServerGroup.N.VServerGroupAttribute.N.Port|Integer|否|22|弹性伸缩将 ECS 实例添加到虚拟服务器组时使用的端口号，取值范围：1~65535。

 N 为负载均衡实例编号，取值范围：1~5。M 为负载均衡实例下虚拟服务器组的编号，取值范围：1~5。

 |
|VServerGroup.N.VServerGroupAttribute.N.VServerGroupId|String|否|rsp-\*\*\*\*|虚拟服务器组ID。N 为负载均衡实例编号，取值范围：1~5。

 M 为负载均衡实例下虚拟服务器组的编号，取值范围：1~5。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DetachVServerGroups
&ScalingGroupId=asg-****
&RegionId=cn-hangzhou
&VServerGroup.1.LoadBalancerId=lb-****
&VServerGroup.1.VServerGroupAttribute.1.VServerGroupId=rsp-****
&VServerGroup.1.VServerGroupAttribute.1.Port=22
&VServerGroup.1.VServerGroupAttribute.2.VServerGroupId=rsp-****
&VServerGroup.1.VServerGroupAttribute.2.Port=80
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DetachVServerGroupsResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DetachVServerGroupsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
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

|您未授予弹性伸缩完整的Open API调用权限。

|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|账号下不存在指定的伸缩组。

|
|400

|InvalidParameter

|The specified value of parameter "%s" is not valid.

|参数值不合法。

|
|400

|MissingParameter

|The input parameter "%s" that is mandatory for processing this request is not supplied.

|缺少必要的参数。

|

