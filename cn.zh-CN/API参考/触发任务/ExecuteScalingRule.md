# ExecuteScalingRule {#doc_api_Ess_ExecuteScalingRule .reference}

调用ExecuteScalingRule执行一条伸缩规则。

## 接口说明 {#description .section}

调用该接口前请确保满足以下条件：

-   伸缩组为Active状态。
-   伸缩组没有伸缩活动正在执行。

当伸缩组没有伸缩活动正在执行时，该接口可以绕过冷却时间（Cooldown）直接执行。

调用该接口返回成功，只是表示弹性伸缩服务接受了该接口的调用请求，伸缩活动可以执行，但不代表伸缩活动能够执行成功。用户需要通过返回的ScalingActivityId查看该伸缩活动的执行状态。

如果该伸缩规则需要增加的ECS实例数加上当前伸缩组的实例数（Total Capacity）大于MaxSize，则按Total Capacity = MaxSize的规则进行执行。

如果当前伸缩组的实例数（Total Capacity）减去该伸缩规则需要减少的ECS实例数小于MinSize，则按Total Capacity = MinSize的规则进行执行。

对于所有地域和所有伸缩组，一个用户最多能弹性伸缩1000台ECS实例。（此数量只包含自动创建的ECS实例，不包含手工添加的ECS实例。）

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=ExecuteScalingRule&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ScalingRuleAri|String|是|ari:acs:ess:cn-qingdao:1344371:scalingRule/cCBpdYdQuBe2cUxOdu6\*\*\*\*|伸缩规则唯一标识符。

 |
|Action|String|否|ExecuteScalingRule|系统规定参数，取值：ExecuteScalingRule。

 |
|BreachThreshold|Float|否|1.0|执行步进伸缩规则时指定的当前阈值，取值范围：-9.999999E18~9.999999E18。

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|用于保证请求的幂等性。由客户端生成该参数值，要保证在不同请求间唯一，最大不超过64个ASCII字符。详情请参见[如何保证幂等性](~~25965~~)。

 |
|MetricValue|Float|否|1.0|执行步进伸缩规则时指定的当前指标值，取值范围：-9.999999E18~9.999999E18。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |
|ScalingActivityId|String|ebta5WbUzC8gcwUWvfch\*\*\*\*|伸缩活动的ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=ExecuteScalingRule
&ScalingRuleAri=ari:acs:ess:cn-qingdao:1344371:scalingRule/cCBpdYdQuBe2cUxOdu6****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ExecuteScalingRuleResponse>
      <ScalingActivityId>ebta5WbUzC8gcwUWvfchyT4U</ScalingActivityId>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3****</RequestId>
</ExecuteScalingRuleResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"ScalingActivityId":"ebta5WbUzC8gcwUWvfch****"
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

|InvalidScalingRuleAri.NotFound

|The specified scaling rule Ari does not exist.

|指定的伸缩规则在该用户账号下不存在。

|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|用户并未向弹性伸缩完整授权Open API接口。

|
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|指定伸缩规则所属的伸缩组未处于active状态。

|
|400

|ScalingActivityInProgress

|You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress for the specified scaling group.

|指定伸缩规则所属的伸缩组有伸缩活动正在进行。

|
|400

|InsufficientBalance

|Your account does not have enough balance.

|用户账号余额不足。

|
|400

|QuotaExceed.Instance

|Living instance quota exceeded.

|用户的ECS实例个数使用达到上限。

|
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|指定伸缩规则所属的伸缩组的负载均衡实例未处于active状态。

|
|400

|IncorrectLoadBalancerHealthCheck

|The current health check type of specified load balancer does not support this action.

|指定伸缩规则所属的伸缩组的负载均衡实例未开启健康检查。

|
|400

|InvalidLoadBalancerId.IncorrectInstanceNetworkType

|The network type of the instance in specified load balancer does not support this action.

|指定的负载均衡实例含有的ECS实例的网络类型与伸缩组的网络类型不匹配。

|
|400

|InvalidLoadBalancerId.VPCMismatch

|The specified virtual switch and the instance in specified load balancer are not in the same VPC.

|指定的伸缩组的负载均衡实例含有的ECS实例与VSwitchId不在同一个VPC当中。

|
|400

|IncorrectDBInstanceStatus

|The current status of DB instance “XXX” does not support this action.

|指定伸缩规则所属的伸缩组的RDS实例未处于running状态

|
|400

|QuotaExceeded.DBInstanceSecurityIP

|Security IP quota exceeded in DB instance “XXX”.

|指定伸缩规则所属的伸缩组的RDS实例访问白名单的IP个数达到上限。

|
|400

|QuotaExceeded.SecurityGroupInstance

|Instance quota exceeded in the specified security group.

|指定的安全组已添加的ECS实例个数达到上限。

|
|400

|IncorrectCapacity.NoChange

|To execute the specified scaling rule, the total capacity will not change.

|伸缩规则未造成伸缩组实例数的变化。

|
|400

|QuotaExceeded.ScalingInstance

|Scaling instance quota exceeded.

|弹性伸缩的ECS实例使用个数达到上限。

|
|400

|QuotaExceeded.AfterpayInstance

|Living afterpay instance quota exceeded.

|按量付费ECS实例的使用个数达到上限。

|
|400

|ResourceNotAvailable.ECS

|The specified region or zone does not offer the specified disk or instance category.

|指定的区域无法创建指定的ECS实例类型或磁盘类型。

|
|400

|ScalingRule.InvalidScalingRuleType

|Specific scaling rule type: %s can not be executed.

|无法执行当前类型的伸缩规则。

|
|400

|InvalidStepAdjustments.NoStepFound

|No adjustment step found for a metric value of: %s.

|未找到符合条件的分步执行步骤。

|
|400

|MissingParameter.MetricValue

|Metric value must be specified for StepScalingRule.

|执行分步伸缩规则必须指定指标值。

|
|400

|MissingParameter.BreachThreshold

|Breach threshold must be specified for StepScalingRule.

|执行分步伸缩规则必须指定阈值。

|
|400

|MetricValueBeyondPermitRange

|Specific parameter "%s" beyond permit range.

|指标值超过了可选范围。

|
|400

|BreachThresholdBeyondPermitRange

|Specific parameter "%s" beyond permit range.

|阈值超过了可选范围。

|

