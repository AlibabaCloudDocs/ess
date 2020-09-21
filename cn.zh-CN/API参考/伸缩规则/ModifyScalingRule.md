# ModifyScalingRule

调用ModifyScalingRule修改一条伸缩规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=ModifyScalingRule&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyScalingRule|系统规定参数。取值：ModifyScalingRule |
|ScalingRuleId|String|是|asr-bp1dvirgwkoowxk7\*\*\*\*|待修改伸缩规则的ID。 |
|ScalingRuleName|String|否|scalingrule\*\*\*\*|伸缩规则的显示名称，2~64个英文或中文字符，以数字、大小字母或中文开头，可包含数字、下划线（\_）、连字符（-）或点号（.）。同一用户账号同一地域同一伸缩组内唯一。 |
|Cooldown|Integer|否|60|伸缩规则的冷却时间，仅适用于简单规则。

 取值范围：0~86400，单位：秒。 |
|MinAdjustmentMagnitude|Integer|否|1|伸缩规则最小调整实例数，仅当伸缩规则类型为SimpleScalingRule或StepScalingRule，且AdjustmentType为PercentChangeInCapacity时生效。 |
|AdjustmentType|String|否|QuantityChangeInCapacity|伸缩规则的调整方式， 适用于简单规则和步进规则，且此时该项必选。取值范围：

 -   QuantityChangeInCapacity：增加或减少指定数量的 ECS 实例。
-   PercentChangeInCapacity：增加或减少指定比例的 ECS 实例。
-   TotalCapacity： 将当前伸缩组的 ECS 实例数量调整到指定数量。 |
|AdjustmentValue|Integer|否|100|伸缩规则的调整值， 适用于简单规则和步进规则，且此时该项必选。任何情况下，单次调整的ECS实例台数都不能超过1000。不同调整方式对应的取值范围：

 -   QuantityChangeInCapacity：-1000~1000
-   PercentChangeInCapacity：-100~10000
-   TotalCapacity：0~2000 |
|EstimatedInstanceWarmup|Integer|否|60|实例预热时间，适用于目标追踪规则和步进规则。处于预热状态的ECS实例将正常的加入伸缩组，但是期间将不会向云监控上报监控数据。

 **说明：** 动态计算需要扩缩容的ECS实例数量时，处于预热状态的实例不计入现有实例数量。

 取值范围：0~86400，单位：秒。 |
|MetricName|String|否|CpuUtilization|预定义监控项，适用于目标追踪规则和预测规则，且此时该项必选。

 目标追踪规则取值范围：

 -   CpuUtilization：平均CPU使用率
-   ClassicInternetRx：经典网络公网入流量平均值
-   ClassicInternetTx：经典网络公网出流量平均值
-   VpcInternetRx：VPC网络公网入流量平均值
-   VpcInternetTx：VPC网络公网出流量平均值
-   IntranetRx：内网入流量平均值
-   IntranetTx ：内网出流量平均值

 预测规则取值范围：

 -   CpuUtilization：平均CPU使用率
-   IntranetRx：内网入流量平均值
-   IntranetTx ：内网出流量平均值 |
|TargetValue|Float|否|0.125|目标值，适用于目标追踪规则和预测规则。TargetValue最多保留小数点后三位，且必须大于0。 |
|DisableScaleIn|Boolean|否|true|是否禁用缩容，仅适用于目标追踪规则。 |
|ScaleInEvaluationCount|Integer|否|15|创建目标追踪规则后，会自动创建报警任务。本参数用于指定对应的缩容报警任务触发报警时，所需连续满足阈值条件的次数。 |
|ScaleOutEvaluationCount|Integer|否|3|创建目标追踪规则后，会自动创建报警任务。本参数用于指定对应的扩容报警任务触发报警时，所需连续满足阈值条件的次数。 |
|StepAdjustment.N.MetricIntervalLowerBound|Float|否|1.0|分步步骤的下边界，仅适用于步进规则，取值范围：-9.999999E18~9.999999E18。 |
|StepAdjustment.N.MetricIntervalUpperBound|Float|否|5.0|分步步骤的上边界，仅适用于步进规则，取值范围：-9.999999E18~9.999999E18。 |
|StepAdjustment.N.ScalingAdjustment|Integer|否|1|分步步骤对应的实例扩展数量，仅适用于步进规则。 |
|PredictiveScalingMode|String|否|PredictAndScale|预测规则的模式。取值范围：

 -   PredictAndScale：产生预测结果并创建预测任务。
-   PredictOnly：产生预测结果，但不会创建预测任务。 |
|PredictiveValueBehavior|String|否|MaxOverridePredictiveValue|预测规则最大值处理方式。取值范围：

 -   MaxOverridePredictiveValue：初始最大值会覆盖预测值。预测值大于初始最大值时，预测任务的最大值采用初始最大值。
-   PredictiveValueOverrideMax：预测值会覆盖初始最大值。预测值大于初始最大值时， 预测任务的最大值采用预测值。
-   PredictiveValueOverrideMaxWithBuffer：预测值会附加一定比例。预测值会按照PredictiveValueBuffer比例增加，当增加后的值大于初始最大值时，会采用增加后的值。 |
|PredictiveValueBuffer|Integer|否|50|PredictiveValueBehavior为PredictiveValueOverrideMaxWithBuffer时生效，预测值会按照该比例增加，当增加后的值大于初始最大值时，会采用增加后的值。取值范围：0~100。 |
|PredictiveTaskBufferTime|Integer|否|30|预测规则自动创建的预测任务默认均在整点执行，您可以设置预启动时间提前执行预测任务，预先准备资源。取值范围：0~60。 |
|InitialMaxSize|Integer|否|100|伸缩组实例数上限，和PredictiveValueBehavior结合使用。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=ModifyScalingRule
&ScalingRuleId=asg-bp1ffogfdauy0jw0****
&AdjustmentType=QuantityChangeInCapacity
&AdjustmentValue=-10
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ModifyScalingRuleResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <ScalingRuleId>asr-bp1dvirgwkoowxk7****</ScalingRuleId>
      <ScalingRuleAri>ari:acs:ess:cn-hangzhou:140692647406****:scalingrule/asr-bp1dvirgwkoowxk7****</ScalingRuleAri>
</ModifyScalingRuleResponse>
```

`JSON` 格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "ScalingRuleId": "asr-bp1dvirgwkoowxk7****",
    "ScalingRuleAri": "ari:acs:ess:cn-hangzhou:140692647406****:scalingrule/asr-bp1dvirgwkoowxk7****"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|404

|InvalidScalingRuleId.NotFound

|The specified scaling rule does not exist.

|指定的伸缩组规则在该用户账号下不存在。 |
|400

|InvalidScalingRuleName.Duplicate

|The specified value of parameter <parameter name\> is duplicated.

|伸缩规则名字已存在。 |
|400

|QuotaExceeded.ScalingRule

|Scaling rule quota exceeded in the specified scaling group.

|用户的伸缩规则使用个数达到上限。 |
|400

|TargetTrackingScalingRule.UnsupportedMetric

|Specific metric is not supported for target tracking scaling rule.

|目标追踪规则不支持当前监控指标。 |
|400

|TargetTrackingScalingRule.DumplicateMetric

|Only one TargetTrackingScaling rule for a given metric specification is allowed.

|一个伸缩组中，同一监控指标只能存在一条目标追踪规则。 |
|400

|InvalidMinAdjustmentMagnitudeMismatchAdjustmentType

|MinAdjustmentMagnitude is not supported by the specified adjustment type.

|MinAdjustmentMagnitude不支持当前伸缩规则调整类型。 |
|400

|InvalidStepAdjustments.MultipleNullUpperBound

|At most one StepAdjustment may have an unspecified upper bound.

|最多只能有一个分步步骤不指定分步上界。 |
|400

|InvalidStepAdjustments.MultipleNullLowerBound

|At most one StepAdjustment may have an unspecified lower bound.

|最多只能有一个分步步骤不指定分步下界。 |
|400

|InvalidStepAdjustments.NoNullLowerBound

|There must be a StepAdjustment with an unspecified lower bound when one StepAdjustment has a negative lower bound.

|当存在一个分步下界为负数时，则必须有一个未指定分步下界的分步步骤。 |
|400

|InvalidStepAdjustments.NoNullUpperBound

|There must be a StepAdjustment with an unspecified upper bound when one StepAdjustment has a positive upper bound.

|当存在一个正数的分步上界时，则必有一个未指定分步上界的分步步骤。 |
|400

|InvalidStepAdjustments.Gap

|StepAdjustment intervals can not have gaps between them.

|分步步骤之间不能有间隔。 |
|400

|InvalidStepAdjustments.Overlap

|StepAdjustment intervals can not overlap.

|分步步骤之间不能重叠。 |
|400

|InvalidStepAdjustments.LowerGtUpper

|LowerBound must be less than the UpperBound for StepAdjustment :%s.

|同一分步步骤中，分步下界必须小于分步上界。 |
|400

|InvalidStepAdjustments.BothNull

|Both lower and upper bounds of a StepAdjustment can not be left unspecified.

|同一分步步骤中，分步上界和分步下界不能同时不指定。 |
|400

|InvalidStepAdjustments.MaxNum

|Your scaling rule can have at most %s StepAdjustments.

|同一伸缩组中分步步骤数量超过阈值。 |
|400

|StepBeyondPermitRange

|Specific parameter "%s" beyond permit range.

|分步步骤的上界或下界超过了可选范围。 |

