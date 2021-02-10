# AttachInstances

调用AttachInstances为伸缩组手动添加ECS实例。

## 接口说明

调用该接口前，请确保满足以下条件：

-   伸缩组处于Active状态。
-   伸缩组内没有执行中的伸缩活动。

加入伸缩组的ECS实例的限制条件包括：

-   必须与伸缩组在同一个地域。
-   必须处于Running状态。
-   不能已加入到其它伸缩组中。
-   付费方式为包年包月、按量付费或抢占式实例。
-   如果伸缩组指定VswitchID，则不支持Classic类型的ECS实例加入伸缩组，也不支持其他VPC的ECS实例加入伸缩组。
-   如果伸缩组没有指定VswitchID，则不支持VPC类型的ECS实例加入伸缩组。

当伸缩组没有伸缩活动正在执行时，该接口可以绕过冷却时间（Cooldown）直接执行。

调用该接口返回成功，只是表示弹性伸缩服务接受了该接口调用的请求，伸缩活动可以执行，但不代表伸缩活动能够执行成功。您需要通过返回的ScalingActivityId查看该伸缩活动的执行状态。

如果该接口指定的实例数加上当前伸缩组的实例数（Total Capacity）大于MaxSize，则调用失败。

通过该接口手动添加的ECS实例不与伸缩组生效的伸缩配置进行关联。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=AttachInstances&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AttachInstances|系统规定参数。取值：AttachInstances |
|ScalingGroupId|String|是|asg-bp18p2yfxow2dloq\*\*\*\*|伸缩组的ID。 |
|InstanceId.N|RepeatList|否|i-28wt4\*\*\*\*|InstanceId.N为待添加ECS实例的ID，N的取值范围：1～20。 |
|LoadBalancerWeight.N|RepeatList|否|50|LoadBalancerWeight.N为ECS实例作为负载均衡实例后端服务器时的权重，N的取值范围：1～20，该参数取值范围：1~100。

 默认值：50 |
|Entrusted|Boolean|否|false|将已经存在的实例手动添加到伸缩组时，是否将该实例的生命周期托管给伸缩组。取值范围：

 -   true：托管。该实例的生命周期由弹性伸缩管理，与伸缩组自动创建的实例一致。实例被移出伸缩组（不包括通过调用DetachInstances移出）时会自动释放。
-   false：不托管。该实例在被移出伸缩组时不会被释放。

 **说明：** 不支持托管包年包月实例。

 默认值：false |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|ScalingActivityId|String|asa-bp1crxor24s28xf1\*\*\*\*|伸缩活动的ID。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=AttachInstances
&ScalingGroupId=asg-bp18p2yfxow2dloq****
&InstanceId.1=i-28wt4****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<AttachInstancesResponse>
      <ScalingActivityId>asa-bp1crxor24s28xf1****</ScalingActivityId>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</AttachInstancesResponse>
```

`JSON`格式

```
{"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E","ScalingActivityId":"asa-bp1crxor24s28xf1****"}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|指定的伸缩组在该账号下不存在。 |
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|您并未向弹性伸缩完整授权OpenAPI接口。 |
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|指定的伸缩组未处于Active状态。 |
|404

|InvalidInstanceId.NotFound

|Instance “XXX” does not exist.

|指定的ECS实例在该账号下不存在。 |
|400

|InvalidInstanceId. RegionMismatch

|Instance “XXX” and the specified scaling group are not in the same Region.

|指定的ECS实例与伸缩组所属的地域不匹配。 |
|400

|InvalidInstanceId.InstanceTypeMismatch

|Instance “XXX” and existing Active scaling configurations have different instance types.

|指定的ECS实例与伸缩配置的实例规格不匹配。 |
|400

|IncorrectInstanceStatus

|The current status of instance “XXX” does not support this action.

|指定的ECS实例未处于Running状态。 |
|400

|InvalidInstanceId. NetworkTypeMismatch

|The network type of instance “XXX” does not support this action.

|ECS实例的网络类型与伸缩组的网络类型不匹配。 |
|400

|InvalidInstanceId.VPCMismatch

|Instance “XXX” and the specified scaling group are not in the same VPC.

|指定的伸缩组与添加的ECS实例不在同一个VPC当中。 |
|400

|InvalidInstanceId.InUse

|Instance “XXX” is already attached to another scaling group.

|指定的ECS实例已加入其它伸缩组。 |
|400

|ScalingActivityInProgress

|You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress for the specified scaling group.

|指定的伸缩组有伸缩活动正在进行。 |
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|指定的伸缩组的负载均衡实例未处于Active状态。 |
|400

|IncorrectLoadBalancerHealthCheck

|The current health check type of specified load balancer does not support this action.

|指定的伸缩组关联的负载均衡实例未开启健康检查。 |
|400

|InvalidLoadBalancerId.IncorrectInstanceNetworkType

|The network type of the instance in specified load balancer does not support this action.

|指定的负载均衡实例含有的ECS实例的网络类型与伸缩组的网络类型不匹配。 |
|400

|InvalidLoadBalancerId.VPCMismatch

|he specified virtual switch and the instance in specified load balancer are not in the same VPC.

|指定的伸缩组的负载均衡实例含有的ECS实例与VSwitchId不在同一个VPC当中。 |
|400

|IncorrectDBInstanceStatus

|The current status of DB instance “XXX” does not support this action.

|指定的伸缩组的RDS实例未处于Running状态。 |
|400

|QuotaExceeded.DBInstanceSecurityIP

|Security IP quota exceeded in DB instance “XXX”.

|指定的伸缩组的RDS实例访问白名单的IP个数达到上限。 |
|400

|QuotaExceeded.SecurityGroupInstance

|Instance quota exceeded in the specified security group.

|指定的安全组已添加的ECS实例个数达到上限。 |
|400

|IncorrectCapacity.MaxSize

|To attach the instances, the total capacity will be greater than the MaxSize.

|加入的ECS实例数使得Total Capacity超过MaxSize。 |

