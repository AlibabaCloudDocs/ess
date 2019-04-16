# AttachInstances {#concept_25954_zh .concept}

往指定的伸缩组添加ECS实例。

## 描述 {#section_odd_l1l_sfb .section}

-   加入的ECS实例的限定条件包括：
    -   加入的ECS实例必须与伸缩组在同一个地域。
    -   加入的ECS实例必须是running状态。
    -   加入的ECS实例不能已加入到其它伸缩组中。
    -   加入的ECS实例支持包年包月和按量付费两种类型。
    -   如果伸缩组指定VswitchID，则不支持Classic类型的ECS实例加入伸缩组，也不支持其他VPC的ECS实例加入伸缩组。
    -   如果伸缩组没有指定VswitchID，则不支持VPC类型的ECS实例加入伸缩组。
-   当伸缩组为active状态，才可以调用该接口。
-   当伸缩组没有伸缩活动正在执行，才可以调用该接口。
-   当伸缩组没有伸缩活动正在执行时，该接口可以绕过冷却时间（Cooldown）直接执行。
-   调用该接口返回成功，只是表示弹性伸缩服务接受了该接口调用的请求，伸缩活动可以执行，但不代表伸缩活动能够执行成功。用户需要通过返回的ScalingActivityId查看该伸缩活动的执行状态。
-   如果该接口指定的实例数加上当前伸缩组的实例数（Total Capacity）大于MaxSize时，则调用失败。
-   手工添加的ECS实例不与伸缩组生效的伸缩配置进行关联。

## 请求参数 {#section_wjq_m1l_sfb .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：AttachInstances。|
|ScalingGroupId|String|是|伸缩组的ID。|
|InstanceId.N|String|是|ECS实例的ID。最多可以输入20个。|

## 返回参数 {#section_hnz_n1l_sfb .section}

|名称|类型|描述|
|:-|:-|:-|
|ScalingActivityId|String|伸缩活动的ID。|

## 示例 {#section_ah2_t1l_sfb .section}

请求示例

```
http://ess.aliyuncs.com/?Action=AttachInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&InstanceId.1=i-28wt48iaa
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<AttachInstancesResponse>
    <ScalingActivityId>bybj9OcaOT4ucPMbFhcqHfA3</ScalingActivityId>
    <RequestId>DD0309B7-2613-4792-9B86-275906695253</RequestId>
</AttachInstancesResponse>
```

`JSON` 格式

```
"RequestId": "6469DCD0-13AC-487E-85A0-CE4922908FDE",
"ScalingActivityId": "ebta5WbUzC8gcwUWvfchyT4U"
```

## 错误码 {#section_pp4_p1l_sfb .section}

对于所有接口的通用性错误，请参考 [客户端错误](intl.zh-CN/API参考/错误代码/客户端错误.md#) 或 [服务器端错误](intl.zh-CN/API参考/错误代码/服务器端错误.md#)。

|HttpCode|错误码|错误信息|描述|
|--------|:--|:---|:-|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|指定的伸缩组在该用户账号下不存在。|
|403|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|用户并未向弹性伸缩完整授权Open API接口。|
|400|IncorrectScalingGroupStatus|The current status of the specified scaling group does not support this action.|指定的伸缩组为非active状态。|
|404|InvalidInstanceId.NotFound|Instance “XXX” does not exist.|指定的ECS实例在该用户账号下不存在。|
|400|InvalidInstanceId. RegionMismatch|Instance “XXX” and the specified scaling group are not in the same Region.|指定的ECS实例与伸缩组所属的地域不匹配。|
|400|InvalidInstanceId.InstanceTypeMismatch|Instance “XXX” and existing active scaling configurations have different instance types.|指定的ECS实例与伸缩配置的实例规格不匹配。|
|400|IncorrectInstanceStatus|The current status of instance “XXX” does not support this action.|指定的ECS实例为非running状态。|
|400|InvalidInstanceId. NetworkTypeMismatch|The network type of instance “XXX” does not support this action.|ECS实例的网络类型与伸缩组的网络类型不匹配。|
|400|InvalidInstanceId.VPCMismatch|Instance “XXX” and the specified scaling group are not in the same VPC.|指定的伸缩组与添加的ECS实例不在同一个VPC当中。|
|400|InvalidInstanceId.InUse|Instance “XXX” is already attached to another scaling group.|指定的ECS实例已加入其它伸缩组。|
|400|ScalingActivityInProgress|You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress for the specified scaling group.|指定的伸缩组有伸缩活动正在进行。|
|400|IncorrectLoadBalancerStatus|The current status of the specified load balancer does not support this action.|指定的伸缩组的负载均衡实例为非active状态。|
|400|IncorrectLoadBalancerHealthCheck|The current health check type of specified load balancer does not support this action.|指定的伸缩组的负载均衡实例未开启健康检查。|
|400|InvalidLoadBalancerId.IncorrectInstanceNetworkType|The network type of the instance in specified load balancer does not support this action.|指定的负载均衡实例含有的ECS实例的网络类型与伸缩组的网络类型不匹配。|
|400|InvalidLoadBalancerId.VPCMismatch|The specified virtual switch and the instance in specified load balancer are not in the same VPC.|指定的伸缩组的负载均衡实例含有的ECS实例与VSwitchId不在同一个VPC当中。|
|400|IncorrectDBInstanceStatus|The current status of DB instance “XXX” does not support this action.|指定的伸缩组的RDS实例为非running状态。|
|400|QuotaExceeded.DBInstanceSecurityIP|Security IP quota exceeded in DB instance “XXX”.|指定的伸缩组的RDS实例访问白名单的IP个数达到上限。|
|400|QuotaExceeded.SecurityGroupInstance|Instance quota exceeded in the specified security group.|指定的安全组已添加的ECS实例个数达到上限。|
|400|IncorrectCapacity.MaxSize|To attach the instances, the total capacity will be greater than the MaxSize.|加入的ECS实例数使得Total Capacity超过MaxSize。|

