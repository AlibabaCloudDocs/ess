# RemoveInstances {#doc_api_Ess_RemoveInstances .reference}

从指定的伸缩组里移出 ECS 实例。

## 描述 {#description .section}

-   从伸缩组移出弹性伸缩自动创建的 ECS 实例时，ECS 实例进入停机不收费状态或者被释放。
-   从伸缩组移出用户手工加入的 ECS 实例时，不停止和释放该 ECS 实例。
-   当伸缩组为 **Active** 状态，才可以调用该接口。
-   当伸缩组没有伸缩活动正在执行，才可以调用该接口。
-   当伸缩组没有伸缩活动正在执行时，该接口可以绕过冷却时间（Cooldown）直接执行。
-   调用该接口返回成功，只是表示弹性伸缩服务接受了该接口调用的请求，伸缩活动可以执行，但不代表伸缩活动能够执行成功。用户需要通过返回的 ScalingActivityId 查看该伸缩活动的执行状态。
-   如果当前伸缩组的实例数（Total Capacity）减去该接口指定的实例数小于 MinSize 时，则调用失败。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=RemoveInstances)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId.N|RepeatList|是|i-28wt4\*\*\*\*|ECS 实例的 ID。最多可以输入 20 个。

 |
|ScalingGroupId|String|是|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组的 ID。

 |
|Action|String|否|RemoveInstances|操作接口名，系统规定参数，取值：RemoveInstances。

 |
|RemovePolicy|String|否|release|指定被移出实例的动作，可选值：

 -   recycle：实例进入停机不收费状态

**说明：** 只在 **ScalingPolicy** 为 recycle 时生效。

-   release：实例被释放

 默认值：release

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |
|ScalingActivityId|String|bybj9OcaOT4ucPMbFhcq\*\*\*\*|伸缩活动的 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=RemoveInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&InstanceId.1=i-28wt4****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RemoveInstancesResponse>
  <ScalingActivityId>bybj9OcaOT4ucPMbFhcqHfA3</ScalingActivityId>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</RemoveInstancesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
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
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|指定的伸缩组在该用户账号下不存在。

|
|404

|InvalidInstanceId.NotFound

|Instance "XXX" does not exist.

|指定的ECS实例在伸缩组下不存在。

|
|400

|InvalidParameter

|The specified group does not support the specified RemovePolicy.

|当前伸缩组不支持停机回收策略。

|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|您未向弹性伸缩授予完整的Open API接口权限。

|
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|指定的伸缩组为非active状态。

|
|400

|ScalingActivityInProgress

|You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress for the specified scaling group.

|指定的伸缩组有进行中的伸缩活动。

|
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|指定伸缩规则所属的伸缩组的负载均衡实例为非active状态。

|
|400

|IncorrectDBInstanceStatus

|The current status of DB instance "XXX" does not support this action.

|指定伸缩规则所属的伸缩组的RDS实例为非running状态。

|
|400

|IncorrectCapacity.MinSize

|To remove the instances, the total capacity will be lesser than the MinSize.

|移出的实例数使得Total Capacity小于MinSize。

|

