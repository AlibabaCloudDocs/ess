# AttachVServerGroups {#concept_ox3_qgz_zfb .concept}

除通过AttachLoadBalancers添加负载均衡实例外，您还可以通过AttachVServerGroups添加负载均衡实例下的一个或者多个虚拟服务器组。

## 限制条件 {#section_hdj_zgz_zfb .section}

由于负载均衡存在 [使用限制](../../../../cn.zh-CN/产品限制/使用限制.md#)，向伸缩组添加虚拟服务器组时需要满足以下条件：

-   负载均衡实例与伸缩组必须属于同一账号。
-   负载均衡实例与伸缩组必须处于同一地域。
-   负载均衡实例必须处于**运行中**状态。
-   负载均衡实例至少配置有一个监听且必须开启健康检查。
-   如果负载均衡实例与伸缩组的网络类型均为 VPC，必须处于同一 VPC。
-   当伸缩组的网络类型为 VPC，负载均衡实例的网络类型为经典网络时，如果虚拟服务器组包含 VPC 实例，该实例必须与伸缩组处于同一 VPC。
-   待添加虚拟服务器组必须属于对应的负载均衡实例。
-   目前，伸缩组内虚拟服务器组的限额为 5。

    **说明：** 确定伸缩组内虚拟服务器组的方式为：负载均衡实例ID（LoadBalancerId） + 虚拟服务器组ID（VServerGroupId） + 虚拟服务器组端口号（Port） 。如果通过不同的端口号将同一虚拟服务器组添加至伸缩组，视为伸缩组内添加了多个虚拟服务器组。如果请求参数中存在重复的虚拟服务器组ID + 端口号，默认使用最先配置的一组，忽略其余虚拟服务器组。


## 请求参数 {#section_xqd_fhz_zfb .section}

|名称|类型|是否必需|描述|
|--|--|----|--|
|Action|String|是|操作接口名，系统规定参数，取值： AttachVServerGroups。|
|RegionId|String|是|伸缩组所属的地域ID，如cn-hangzhou、cn-shanghai。更多详情，请参阅 [地域和可用区](../../../../cn.zh-CN/通用参考/地域和可用区.md#)。|
|ScalingGroupId|String|是|伸缩组ID。|
|VServerGroup.N.LoadBalancerId|String|是|虚拟服务器组所属负载均衡实例的ID。N 为负载均衡实例编号，取值范围：1-5。|
|VServerGroup.N.VServerGroupAttribute.M.VServerGroupId|String|是|虚拟服务器组ID。N 为负载均衡实例编号，取值范围：1-5。M 为负载均衡实例下虚拟服务器组的编号，取值范围：1-5。|
|VServerGroup.N.VServerGroupAttribute.M.Port|Integer|是|弹性伸缩将ECS实例添加到虚拟服务器组时使用的端口号，取值范围：1-65535。N 为负载均衡实例编号，取值范围：1-5。M 为负载均衡实例下虚拟服务器组的编号，取值范围：1-5。

|
|VServerGroup.N.VServerGroupAttribute.M.Weight|Integer|否| 弹性伸缩将ECS实例添加到虚拟服务器组时设置的权重，取值范围：0-100。默认值：50。

N 为负载均衡实例编号，取值范围：1-5。M 为负载均衡实例下虚拟服务器组的编号，取值范围：1-5。

|
|ForceAttach|Boolean|否|是否将当前伸缩组内的ECS实例添加到新增的虚拟服务器组。-   true：添加
-   false：不添加

默认值：false。

|

## 返回参数 {#section_j1y_f3z_zfb .section}

|名称|类型|描述|
|--|--|--|
|RequestId|String|请求ID。|

## 示例 {#section_lm4_j3z_zfb .section}

**请求示例**

```
http://ess.aliyuncs.com/?Action=AttachVServerGroups
&ScalingGroupId=asg-xxxxxxxxxxx
&RegionId=cn-hangzhou
&VServerGroup.1.LoadBalancerId=lb-xxxxxxx
&VServerGroup.1.VServerGroupAttribute.1.VServerGroupId=rsp-xxxxx
&VServerGroup.1.VServerGroupAttribute.1.Port=22
&VServerGroup.1.VServerGroupAttribute.1.Weight=100
&<公共请求参数>
```

**返回示例**

 XML 格式

```
<AttachVServerGroupsResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</AttachVServerGroupsResponse>
```

 JSON 格式

```
{
   "requestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 {#section_jh2_v3z_zfb .section}

|错误代码|错误信息|HTTP 状态码|说明|
|----|----|--------|--|
|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|403|您未授予弹性伸缩完整的Open API调用权限。|
|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|404|账号下不存在指定的伸缩组。|
|InvalidLoadBalancerId.NotFound|The load balancer "%s" does not exist.|404|账号下不存在指定的负载均衡实例。|
|InvalidLoadBalancerId.RegionMismatch|The load balancer "%s" and the specified scaling group are not in the same Region.|400|负载均衡实例与伸缩组不在同一地域。|
|IncorrectLoadBalancerStatus|The current status of the load balancer "%s" does not support this action.|400|当前负载均衡实例状态不支持此操作。|
|IncorrectLoadBalancerHealthCheck|The current health check type of the load balancer "%s" does not support this action.|400|当前负载均衡实例未开启健康检查。|
|InvalidLoadBalancerId.VPCMismatch|The specified virtual switch and the instance in the load balancer "%s" are not in the same VPC.|400|负载均衡实例与伸缩组不在同一VPC下。|
|InvalidVServerGroupId.ForLoadBalancer|Invalid VServerGroupId For LoadBalancer "%s".|400|VServerGroupId对应的虚拟服务器组不属于指定的负载均衡实例。|
|QuotaExceeded.VServerGroup|VServerGroup quota exceeded in the specified scaling group.|400|当前伸缩组内可配置的虚拟服务器组个数达到上限。|

