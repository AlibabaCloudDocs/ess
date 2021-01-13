# RemoveInstances

调用RemoveInstances从一个伸缩组删除一台或多台ECS实例。

## 接口说明

调用本接口前请确保满足以下条件：

-   伸缩组处于启用（Active）状态。
-   伸缩组中没有正在执行的伸缩活动。

当伸缩组没有执行中的伸缩活动时，该接口可以绕过冷却时间（DefaultCooldown）直接执行。

如果一台ECS实例由弹性伸缩自动创建，或者您手动添加但已托管给伸缩组，从伸缩组删除该ECS实例时，ECS实例进入停机不收费状态或者被释放。

如果一台ECS实例由您手动添加且未托管给伸缩组，从伸缩组删除该ECS实例时，ECS实例不会被停止或者释放。

调用该接口返回成功，只是表示弹性伸缩服务接受了该接口调用的请求，伸缩活动可以执行，但不代表伸缩活动能够执行成功。您需要通过返回的ScalingActivityId查看该伸缩活动的执行状态。

如果当前伸缩组的实例数（TotalCapacity）减去该接口指定的实例数小于伸缩组内最小实例数（MinSize），则调用失败。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=RemoveInstances&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RemoveInstances|系统规定参数。取值：RemoveInstances |
|InstanceId.N|RepeatList|是|i-28wt4\*\*\*\*|待删除ECS实例的ID。N的取值范围：1~20。 |
|ScalingGroupId|String|是|asg-bp18p2yfxow2dloq\*\*\*\*|伸缩组的ID。 |
|RemovePolicy|String|否|release|指定被删除ECS实例的动作。取值范围：

 -   recycle：ECS实例进入停机不收费状态。

**说明：** 仅在ScalingPolicy为recycle时生效。

-   release：ECS实例被释放。

 CreateScalingGroup的ScalingPolicy参数指定伸缩组的回收模式，但实例被删除时的具体动作，由RemoveInstances的RemovePolicy参数决定。例如：

 -   ScalingPolicy为recycle，且RemovePolicy为recycle，ECS实例进入停机不收费状态。
-   ScalingPolicy为recycle，且RemovePolicy为release，ECS实例被释放。
-   ScalingPolicy为release，且RemovePolicy为recycle，ECS实例被释放。
-   ScalingPolicy为release，且RemovePolicy为release，ECS实例被释放。

 默认值：release |
|DecreaseDesiredCapacity|Boolean|否|true|是否修改期望实例数。取值范围：

 -   true：从伸缩组删除ECS实例后，期望实例数也减少相应台数。
-   false：从伸缩组删除ECS实例后，期望实例数不会变化。

 默认值：true |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|ScalingActivityId|String|asa-bp175o6f6ego3r2j\*\*\*\*|伸缩活动的ID。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=RemoveInstances
&ScalingGroupId=asg-bp18p2yfxow2dloq****
&InstanceId.1=i-28wt4****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<RemoveInstancesResponse>
      <ScalingActivityId>asa-bp175o6f6ego3r2j****</ScalingActivityId>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</RemoveInstancesResponse>
```

`JSON` 格式

```
{
    "ScalingActivityId":"asa-bp175o6f6ego3r2j****",
    "RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ess)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|指定的伸缩组在该用户账号下不存在。 |
|404

|InvalidInstanceId.NotFound

|Instance "XXX" does not exist.

|指定的ECS实例在伸缩组下不存在。 |
|400

|InvalidParameter

|The specified group does not support the specified RemovePolicy.

|当前伸缩组不支持停机回收策略。 |
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|您未向弹性伸缩授予完整的OpenAPI接口权限。 |
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|指定的伸缩组未处于Active状态。 |
|400

|ScalingActivityInProgress

|You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress for the specified scaling group.

|指定的伸缩组有进行中的伸缩活动。 |
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|指定伸缩规则所属的伸缩组的负载均衡实例未处于Active状态。 |
|400

|IncorrectDBInstanceStatus

|The current status of DB instance "XXX" does not support this action.

|指定伸缩规则所属的伸缩组的RDS实例未处于Running状态。 |
|400

|IncorrectCapacity.MinSize

|To remove the instances, the total capacity will be lesser than the MinSize.

|删除ECS实例使得TotalCapacity小于MinSize。 |

