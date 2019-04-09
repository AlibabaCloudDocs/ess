# DetachInstances {#doc_api_Ess_DetachInstances .reference}

从一个伸缩组分离一台或多台 ECS 实例。

## 描述 {#description .section}

分离 ECS 实例之后，ECS 实例可以独立于伸缩组存在，您可以将 ECS 实例附加到其他伸缩组（[AttachInstances](~~25954~~)）。分离一台 ECS 实例并不会停止或释放该 ECS 实例，若有相关需要，您可以手动 [停止](~~25501~~) 或 [释放](~~25507~~) ECS 实例。

**说明：** 说明：

-   目标伸缩组必须处于 **启用**（`Enable`） 状态。
-   目标伸缩组不能有正在进行的伸缩活动。
-   目标伸缩组没有正在进行的伸缩活动时，该接口可以绕过 [冷却时间](~~25912~~) 直接执行。
-   接口成功调用后，仅表示接受了该接口调用的请求。可以照常触发伸缩活动，但不能保证伸缩活动的成功性，您需要通过返回的 `ScalingActivityId` 查看伸缩活动的状态。
-   目标伸缩组的 ECS 数减去当前分离的 ECS 数不能小于伸缩组最小实例数（`MinSize`）。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=DetachInstances)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId.N|RepeatList|是|i-28wt4\*\*\*\*|ECS 实例 ID。N 的取值范围为 1~20。

 |
|ScalingGroupId|String|是|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组 ID。

 |
|Action|String|否|DetachInstances|系统规定参数，取值： DetachInstances。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |
|ScalingActivityId|String|asa-\*\*\*\*|伸缩活动 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DetachInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&InstanceId.1=i-28wt4****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DetachInstancesResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
  <ScalingActivityId>asa-xxxxxxxxx</ScalingActivityId>
</DetachInstancesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"ScalingActivityId":"asa-****"
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
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|目标伸缩组必须处于 启用（Enable） 状态。

|
|400

|ScalingActivityInProgress

|You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress for the specified scaling group.

|目标伸缩组不能有正在进行的伸缩活动。

|
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|目标伸缩组内的负载均衡实例必须处于 运行中（Active）状态。

|
|400

|IncorrectDBInstanceStatus

|The current status of DB instance “XXX” does not support this action.

|目标伸缩组内的 RDS 实例必须处于 运行中（Running）状态。

|
|400

|IncorrectCapacity.MinSize

|To remove the instances, the total capacity will be lesser than the MinSize.

|目标伸缩组的 ECS 实例数减去当前分离的 ECS 实例数不能小于伸缩组最少实例数（MinSize）。

|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|您暂未被授权使用 DetachInstances 接口。

|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|指定的伸缩组不存在。

|
|404

|InvalidInstanceId.NotFound

|Instance “XXX” does not exist.

|指定的 ECS 实例不存在。

|

