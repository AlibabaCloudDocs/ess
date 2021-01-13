# ExecuteScalingRule

调用ExecuteScalingRule执行一条伸缩规则。

## 接口说明

调用该接口前请确保满足以下条件：

-   伸缩组处于Active状态。
-   伸缩组没有执行中的伸缩活动。

当伸缩组没有执行中的伸缩活动时，该接口可以绕过冷却时间（Cooldown）直接执行伸缩活动。

调用该接口返回成功，只是表示弹性伸缩服务接受了该接口的调用请求，可以执行伸缩活动，但不代表伸缩活动能够执行成功。您需要通过返回的ScalingActivityId查看该伸缩活动的执行状态。

如果伸缩规则需要增加的ECS实例数加上当前伸缩组的实例数（Total Capacity）大于MaxSize，则按Total Capacity = MaxSize执行伸缩活动。

如果当前伸缩组的实例数（Total Capacity）减去伸缩规则需要减少的ECS实例数小于MinSize，则按Total Capacity = MinSize执行伸缩活动。

单次调整的ECS实例台数存在限制，请参见[CreateScalingRule](~~25948~~)中的AdjustmentValue参数说明。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=ExecuteScalingRule&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ExecuteScalingRule|系统规定参数。取值：ExecuteScalingRule |
|ScalingRuleAri|String|是|ari:acs:ess:cn-hangzhou:140692647406\*\*\*\*:scalingrule/asr-bp1dvirgwkoowxk7\*\*\*\*|伸缩规则唯一标识符。

 **说明：** 调用API执行伸缩规则时，只支持执行简单规则和步进规则，且执行步进规则时必须同时指定BreachThreshold和MetricValue。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|用于保证请求的幂等性。由客户端生成该参数值，要保证在不同请求间唯一，最大不超过64个ASCII字符。详情请参见[如何保证幂等性](~~25965~~)。 |
|BreachThreshold|Float|否|1.0|执行步进伸缩规则时指定的当前阈值，取值范围：-9.999999E18~9.999999E18。 |
|MetricValue|Float|否|1.0|执行步进伸缩规则时指定的当前指标值，取值范围：-9.999999E18~9.999999E18。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|ScalingActivityId|String|asa-bp13o672yeautiil\*\*\*\*|伸缩活动的ID。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=ExecuteScalingRule
&ScalingRuleAri=ari:acs:ess:cn-hangzhou:140692647406****:scalingrule/asr-bp1dvirgwkoowxk7****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ExecuteScalingRuleResponse>
      <ScalingActivityId>asa-bp13o672yeautiil****</ScalingActivityId>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3****</RequestId>
</ExecuteScalingRuleResponse>
```

`JSON` 格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "ScalingActivityId": "asa-bp13o672yeautiil****"
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

|InvalidScalingRuleAri.NotFound

|The specified scaling rule Ari does not exist.

|指定的伸缩规则在该账号下不存在。 |
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|您并未向弹性伸缩完整授权Open API接口。 |
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|指定伸缩规则所属的伸缩组未处于Active状态。 |
|400

|ScalingActivityInProgress

|You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress for the specified scaling group.

|指定伸缩规则所属的伸缩组有伸缩活动正在进行。 |
|400

|InsufficientBalance

|Your account does not have enough balance.

|账号余额不足。 |
|400

|QuotaExceed.Instance

|Living instance quota exceeded.

|ECS实例个数达到上限。 |
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|指定伸缩规则所属的伸缩组的负载均衡实例未处于active状态。 |
|400

|IncorrectLoadBalancerHealthCheck

|The current health check type of specified load balancer does not support this action.

|指定伸缩规则所属的伸缩组的负载均衡实例未开启健康检查。 |
|400

|InvalidLoadBalancerId.IncorrectInstanceNetworkType

|The network type of the instance in specified load balancer does not support this action.

|指定的负载均衡实例含有的ECS实例的网络类型与伸缩组的网络类型不匹配。 |
|400

|InvalidLoadBalancerId.VPCMismatch

|The specified virtual switch and the instance in specified load balancer are not in the same VPC.

|指定的伸缩组的负载均衡实例含有的ECS实例与VSwitchId不在同一个VPC当中。 |
|400

|IncorrectDBInstanceStatus

|The current status of DB instance “XXX” does not support this action.

|指定伸缩规则所属的伸缩组的RDS实例未处于running状态 |
|400

|QuotaExceeded.DBInstanceSecurityIP

|Security IP quota exceeded in DB instance “XXX”.

|指定伸缩规则所属的伸缩组的RDS实例访问白名单的IP个数达到上限。 |
|400

|QuotaExceeded.SecurityGroupInstance

|Instance quota exceeded in the specified security group.

|指定的安全组已添加的ECS实例个数达到上限。 |
|400

|IncorrectCapacity.NoChange

|To execute the specified scaling rule, the total capacity will not change.

|伸缩规则未造成伸缩组实例数的变化。 |
|400

|QuotaExceeded.ScalingInstance

|Scaling instance quota exceeded.

|弹性伸缩的ECS实例使用个数达到上限。 |
|400

|QuotaExceeded.AfterpayInstance

|Living afterpay instance quota exceeded.

|按量付费ECS实例的使用个数达到上限。 |
|400

|ResourceNotAvailable.ECS

|The specified region or zone does not offer the specified disk or instance category.

|指定的区域无法创建指定的ECS实例类型或磁盘类型。 |
|400

|ScalingRule.InvalidScalingRuleType

|Specific scaling rule type: %s can not be executed.

|无法执行当前类型的伸缩规则。 |
|400

|InvalidStepAdjustments.NoStepFound

|No adjustment step found for a metric value of: %s.

|未找到符合条件的分步执行步骤。 |
|400

|MissingParameter.MetricValue

|Metric value must be specified for StepScalingRule.

|执行分步伸缩规则必须指定指标值。 |
|400

|MissingParameter.BreachThreshold

|Breach threshold must be specified for StepScalingRule.

|执行分步伸缩规则必须指定阈值。 |
|400

|MetricValueBeyondPermitRange

|Specific parameter "%s" beyond permit range.

|指标值超过了可选范围。 |
|400

|BreachThresholdBeyondPermitRange

|Specific parameter "%s" beyond permit range.

|阈值超过了可选范围。 |

