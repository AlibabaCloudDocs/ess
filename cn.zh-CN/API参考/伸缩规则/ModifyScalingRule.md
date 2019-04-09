# ModifyScalingRule {#doc_api_Ess_ModifyScalingRule .reference}

修改一条已有的伸缩规则，重新定义伸缩动作。

## 描述 {#description .section}

修改一条已有伸缩规则的指定属性，应对新的场景。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=ModifyScalingRule)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ScalingRuleId|String|是|eMKWG8SRNb9dBLAjweN\*\*\*\*|伸缩规则的 ID。

 |
|Action|String|否|ModifyScalingRule|系统规定参数，取值：ModifyScalingRule。

 |
|AdjustmentType|String|否|QuantityChangeInCapacity|伸缩规则的调整方式， 仅适用于简单伸缩规则。可选值：

 -   QuantityChangeInCapacity：增加或减少指定数量的 ECS 实例。
-   PercentChangeInCapacity：增加或减少指定比例的 ECS 实例。
-   TotalCapacity： 将当前伸缩组的 ECS 实例数量调整到指定数量。

 |
|AdjustmentValue|Integer|否|100|伸缩规则的调整值， 仅适用于简单伸缩规则。任何情况下，单次调整的 ECS 实例台数都不能超过 500。不同调整方式对应的取值范围：

 -   QuantityChangeInCapacity：-500~500
-   PercentChangeInCapacity：-100~10000
-   TotalCapacity：0~1000

 |
|Cooldown|Integer|否|60|伸缩规则的冷却时间，仅适用于简单伸缩规则。

 取值范围：0~86400，单位：秒，默认值：空。

 |
|DisableScaleIn|Boolean|否|true|是否禁用缩容，仅适用于目标追踪伸缩规则。

 |
|EstimatedInstanceWarmup|Integer|否|60|实例预热时间，适用于目标追踪伸缩规则和步进伸缩规则。处于预热状态的 ECS 实例将正常的加入伸缩组，但是期间将不会向云监控上报监控数据。

 **说明：** 动态计算需要扩缩容的 ECS 实例数量时，处于预热状态的实例不计入现有实例数量。

 取值范围：0~86400，单位：秒。

 |
|MetricName|String|否|CpuUtilization|预定义监控项，仅适用于目标追踪伸缩规则。可选值：

 -   CpuUtilization：平均 CPU 使用率
-   ClassicInternetRx：经典网络公网入流量平均值
-   ClassicInternetTx：经典网络公网出流量平均值
-   VpcInternetRx：VPC 网络公网入流量平均值
-   VpcInternetTx：VPC 网络公网出流量平均值
-   IntranetRx：内网入流量平均值
-   IntranetTx ：内网出流量平均值

 |
|MinAdjustmentMagnitude|Integer|否|1|伸缩规则最小调整实例数，仅当伸缩规则类型为SimpleScalingRule或StepScalingRule，且AdjustmentType为PercentChangeInCapacity时生效。

 |
|ScalingRuleName|String|否|测试sr|伸缩规则的显示名称，2~40 个英文或中文字符，以数字、大小字母或中文开头，可包含数字，"\_"、"-" 或 ”.”。同一用户账号同一地域同一伸缩组内唯一。如果没有指定该参数，默认值为 ScalingRuleId。

 |
|StepAdjustment.N.MetricIntervalLowerBound|Float|否|1.0|分步步骤的下边界，取值范围-9.999999E18~9.999999E18。

 |
|StepAdjustment.N.MetricIntervalUpperBound|Float|否|5.0|分步步骤的上边界，取值范围-9.999999E18~9.999999E18。

 |
|StepAdjustment.N.ScalingAdjustment|Integer|否|1|分步步骤对应的实例扩展数量。

 |
|TargetValue|Float|否|0.125|目标值，仅适用于目标追踪伸缩规则。TargetValue 最多保留小数点后三位，且必须大于 0。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=ModifyScalingRule
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&AdjustmentType=QuantityChangeInCapacity
&AdjustmentValue=-10
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyScalingRuleResponse>
  <ScalingRuleAri>ari:acs:ess:cn-qingdao:1344371:scalingrule/eMKWG8SRNb9dBLAjweNI1Ik</ScalingRuleAri>
  <ScalingRuleId>eMKWG8SRNb9dBLAjweN****</ScalingRuleId>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyScalingRuleResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"ScalingRuleAri":"ari:acs:ess:cn-qingdao:1344371:scalingrule/eMKWG8SRNb9dBLAjweNI1Ik",
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"ScalingRuleId":"eMKWG8SRNb9dBLAjweN****"
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
|400

|InvalidScalingRuleName.Duplicate

|The specified value of parameter <parameter name\> is duplicated.

|伸缩规则名字已存在。

|
|400

|QuotaExceeded.ScalingRule

|Scaling rule quota exceeded in the specified scaling group.

|用户的伸缩规则使用个数达到上限。

|
|400

|TargetTrackingScalingRule.UnsupportedMetric

|Specific metric is not supported for target tracking scaling rule.

|目标追踪伸缩规则不支持当前监控指标。

|
|400

|TargetTrackingScalingRule.DumplicateMetric

|Only one TargetTrackingScaling rule for a given metric specification is allowed.

|一个伸缩组中，同一监控指标只能存在一条目标追踪规则。

|
|400

|InvalidMinAdjustmentMagnitudeMismatchAdjustmentType

|MinAdjustmentMagnitude is not supported by the specified adjustment type.

|MinAdjustmentMagnitude不支持当前伸缩规则调整类型。

|
|400

|InvalidStepAdjustments.MultipleNullUpperBound

|At most one StepAdjustment may have an unspecified upper bound.

|最多只能有一个分步步骤不指定分步上界。

|
|400

|InvalidStepAdjustments.MultipleNullLowerBound

|At most one StepAdjustment may have an unspecified lower bound.

|最多只能有一个分步步骤不指定分步下界。

|
|400

|InvalidStepAdjustments.NoNullLowerBound

|There must be a StepAdjustment with an unspecified lower bound when one StepAdjustment has a negative lower bound.

|当存在一个分步下界为负数时，则必须有一个未指定分步下界的分步步骤。

|
|400

|InvalidStepAdjustments.NoNullUpperBound

|There must be a StepAdjustment with an unspecified upper bound when one StepAdjustment has a positive upper bound.

|当存在一个正数的分步上界时，则必有一个未指定分步上界的分步步骤。

|
|400

|InvalidStepAdjustments.Gap

|StepAdjustment intervals can not have gaps between them.

|分步步骤之间不能有间隔。

|
|400

|InvalidStepAdjustments.Overlap

|StepAdjustment intervals can not overlap.

|分步步骤之间不能重叠。

|
|400

|InvalidStepAdjustments.LowerGtUpper

|LowerBound must be less than the UpperBound for StepAdjustment :%s.

|同一分步步骤中，分步下界必须小于分步上界。

|
|400

|InvalidStepAdjustments.BothNull

|Both lower and upper bounds of a StepAdjustment can not be left unspecified.

|同一分步步骤中，分步上界和分步下界不能同时不指定。

|
|400

|InvalidStepAdjustments.MaxNum

|Your scaling rule can have at most %s StepAdjustments.

|同一伸缩组中分步步骤数量超过阈值。

|
|400

|StepBeyondPermitRange

|Specific parameter "%s" beyond permit range.

|分步步骤的上界或下界超过了可选范围。

|

