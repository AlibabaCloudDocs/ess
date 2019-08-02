# AttachInstances {#doc_api_Ess_AttachInstances .reference}

调用AttachInstances为伸缩组添加ECS实例。

## 接口说明 {#description .section}

加入的ECS实例的限定条件包括：

-   加入的ECS实例必须与伸缩组在同一个地域。
-   加入的ECS实例必须处于Running状态。
-   加入的ECS实例不能已加入到其它伸缩组中。
-   加入的ECS实例支持包年包月和按量付费两种类型。
-   如果伸缩组指定VswitchID，则不支持Classic类型的ECS实例加入伸缩组，也不支持其他VPC的ECS实例加入伸缩组。
-   如果伸缩组没有指定VswitchID，则不支持VPC类型的ECS实例加入伸缩组。

    当伸缩组处于Active状态时，才可以调用该接口。


当伸缩组没有伸缩活动正在执行时，才可以调用该接口。

当伸缩组没有伸缩活动正在执行时，该接口可以绕过冷却时间（Cooldown）直接执行。

调用该接口返回成功，只是表示弹性伸缩服务接受了该接口调用的请求，伸缩活动可以执行，但不代表伸缩活动能够执行成功。您需要通过返回的ScalingActivityId查看该伸缩活动的执行状态。

如果该接口指定的实例数加上当前伸缩组的实例数（Total Capacity）大于MaxSize，则调用失败。

手工添加的ECS实例不与伸缩组生效的伸缩配置进行关联。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=AttachInstances&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ScalingGroupId|String|是|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组的ID。

 |
|InstanceId.1|String|是|i-28wt4\*\*\*\*|InstanceId.N为待添加ECS实例的ID，N的取值范围：1～20。

 |
|Action|String|否|AttachInstances|系统规定参数，取值：AttachInstances。

 |
|LoadBalancerWeight.1|Integer|否|50|LoadBalancerWeight.N为对应ECS实例后端服务器的权重，N的取值范围：1～20，该参数取值范围：0~100。

 默认值：50。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |
|ScalingActivityId|String|bybj9OcaOT4ucPMbFhcq\*\*\*\*|伸缩活动的ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=AttachInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&InstanceId.1=i-28wt4****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AttachInstancesResponse>
      <ScalingActivityId>bybj9OcaOT4ucPMbFhcqHfA3</ScalingActivityId>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</AttachInstancesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"ScalingActivityId":"bybj9OcaOT4ucPMbFhcq****"
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
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|指定的伸缩组在该账号下不存在。

|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|您并未向弹性伸缩完整授权Open API接口。

|
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|指定的伸缩组未处于active状态。

|
|404

|InvalidInstanceId.NotFound

|Instance “XXX” does not exist.

|指定的ECS实例在该账号下不存在。

|
|400

|InvalidInstanceId. RegionMismatch

|Instance “XXX” and the specified scaling group are not in the same Region.

|指定的ECS实例与伸缩组所属的地域不匹配。

|
|400

|InvalidInstanceId.InstanceTypeMismatch

|Instance “XXX” and existing active scaling configurations have different instance types.

|指定的ECS实例与伸缩配置的实例规格不匹配。

|
|400

|IncorrectInstanceStatus

|The current status of instance “XXX” does not support this action.

|指定的ECS实例未处于running状态。

|
|400

|InvalidInstanceId. NetworkTypeMismatch

|The network type of instance “XXX” does not support this action.

|ECS实例的网络类型与伸缩组的网络类型不匹配。

|
|400

|InvalidInstanceId.VPCMismatch

|Instance “XXX” and the specified scaling group are not in the same VPC.

|指定的伸缩组与添加的ECS实例不在同一个VPC当中。

|
|400

|InvalidInstanceId.InUse

|Instance “XXX” is already attached to another scaling group.

|指定的ECS实例已加入其它伸缩组。

|
|400

|ScalingActivityInProgress

|You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress for the specified scaling group.

|指定的伸缩组有伸缩活动正在进行。

|
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|指定的伸缩组的负载均衡实例未处于active状态。

|
|400

|IncorrectLoadBalancerHealthCheck

|The current health check type of specified load balancer does not support this action.

|指定的伸缩组的负载均衡实例未开启健康检查。

|
|400

|InvalidLoadBalancerId.IncorrectInstanceNetworkType

|The network type of the instance in specified load balancer does not support this action.

|指定的负载均衡实例含有的ECS实例的网络类型与伸缩组的网络类型不匹配。

|
|400

|InvalidLoadBalancerId.VPCMismatch

|he specified virtual switch and the instance in specified load balancer are not in the same VPC.

|指定的伸缩组的负载均衡实例含有的ECS实例与VSwitchId不在同一个VPC当中。

|
|400

|IncorrectDBInstanceStatus

|The current status of DB instance “XXX” does not support this action.

|指定的伸缩组的RDS实例未处于running状态。

|
|400

|QuotaExceeded.DBInstanceSecurityIP

|Security IP quota exceeded in DB instance “XXX”.

|指定的伸缩组的RDS实例访问白名单的IP个数达到上限。

|
|400

|QuotaExceeded.SecurityGroupInstance

|Instance quota exceeded in the specified security group.

|指定的安全组已添加的ECS实例个数达到上限。

|
|400

|IncorrectCapacity.MaxSize

|To attach the instances, the total capacity will be greater than the MaxSize.

|加入的ECS实例数使得Total Capacity超过MaxSize。

|

