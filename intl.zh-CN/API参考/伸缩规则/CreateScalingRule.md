# CreateScalingRule {#doc_api_Ess_CreateScalingRule .reference}

创建一条伸缩规则，用于定义具体的伸缩动作。

## 描述 {#description .section}

伸缩规则（Scaling Rule）定义了具体的扩张或收缩操作，例如加入或移出N个实例。如果执行伸缩规则会造成伸缩组的ECS实例数低于MinSize或高于MaxSize，则弹性伸缩会自动调整需要加入或移出的ECS实例数，使得伸缩组的ECS实例数调整到MinSize或MaxSize，但伸缩规则的设定值不会变化。根据传入参数创建伸缩规则。

-   例：某个伸缩组，MaxSize = 3，当前实例数Total Capacity =2，伸缩规则指定“加3台ECS实例”，则在实际执行过程中只会加1台ECS实例，但伸缩规则的设定值仍然3。
-   例：某个伸缩组，MinSize = 2，当前实例数Total Capacity = 3，伸缩规则指定“减去5台ECS实例”，则在实际执行过程中只会减1台ECS实例，但伸缩规则的设定值仍然5。

根据传入参数创建伸缩规则。

-   当AdjustmentType是TotalCapacity时，表示将当前伸缩组的ECS实例数量调整到指定数量，对应的AdjustmentValue值必须大于等于0。
-   当AdjustmentType是QuantityChangeInCapacity或PercentChangeInCapacity，对应的AdjustmentValue值为正数表示增加实例、为负数表示减少实例。
-   当AdjustmentType是PercentChangeInCapacity，弹性伸缩服务以伸缩组当前实例数（Total Capacity） x AdjusmentValue/100，并使用四舍五入原则来确认增加或减少的ECS实例个数。
-   当伸缩规则指定了冷却时间（Cooldown），则执行该伸缩规则的伸缩活动完成后，会以伸缩规则中指定的冷却时间对伸缩组进行冷却处理，如果伸缩规则未指定冷却时间，则以伸缩组指定的冷却时间（DefaultCooldown）为准。
-   一个伸缩组内最多只能创建50条伸缩规则。
-   返回的伸缩规则唯一标识符（ScalingRuleAri），主要可以被以下接口所使用：
    -   在执行伸缩规则（ExecuteScalingRule）的ScalingRuleAri参数中指定，用户可以手工执行该伸缩规则。
    -   在创建定时任务（CreateScheduledTask）的ScheduledAction参数中指定，用户可以定时执行该伸缩规则。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=CreateScalingRule)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ScalingGroupId|String|是|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩规则所属的伸缩组 ID。

 |
|Action|String|否|CreateScalingRule|操作接口名，系统规定参数，取值：CreateScalingRule。

 |
|ScalingRuleName|String|否|测试sr|伸缩规则的显示名称，2~40 个英文或中文字符，以数字、大小字母或中文开头，可包含数字，“\_”、“-”或“.”。同一用户账号同一地域同一伸缩组内唯一。如果没有指定该参数，默认值为 ScalingRuleId。 

 |
|Cooldown|Integer|否|60|伸缩规则的冷却时间，仅适用于简单伸缩规则。 取值范围：0~86400，单位：秒，默认值：空。

 |
|MinAdjustmentMagnitude|Integer|否|1|伸缩规则最小调整实例数，仅当伸缩规则类型为SimpleScalingRule或StepScalingRule，且AdjustmentType为PercentChangeInCapacity时生效。

 |
|AdjustmentType|String|否|QuantityChangeInCapacity|伸缩规则的调整方式， 仅适用于简单伸缩规则，且此时该项必选。可选值：

 -   QuantityChangeInCapacity：增加或减少指定数量的ECS实例。
-   PercentChangeInCapacity：增加或减少指定比例的ECS实例。
-   TotalCapacity： 将当前伸缩组的ECS实例数量调整到指定数量。

 |
|AdjustmentValue|Integer|否|100|伸缩规则的调整值， 仅适用于简单伸缩规则，且此时该项必选。任何情况下，单次调整的ECS实例台数都不能超过 500。不同调整方式对应的取值范围：

 -   QuantityChangeInCapacity：-500~500
-   PercentChangeInCapacity：-100~10000
-   TotalCapacity：0~1000

 |
|ScalingRuleType|String|否|SimpleScalingRule|伸缩规则类型。可选值：

 -   SimpleScalingRule：简单伸缩规则。根据调整方式（AdjustmentType）和调整值（AdjustmentValue）调整ECS实例数量。
-   TargetTrackingScalingRule：目标追踪伸缩规则。根据预定义监控（MetricName）项动态计算需要扩缩容的ECS实例数量，尽量将预定义监控项的指标值维持在目标值（TargetValue）附近。
-   StepScalingRule： 步进伸缩规则，根据阈值和指标值提供分步扩展方式。

 默认值：SimpleScalingRule。

 |
|EstimatedInstanceWarmup|Integer|否|300|实例预热时间，适用于目标追踪伸缩规则和步进伸缩规则。处于预热状态的ECS实例将正常的加入伸缩组，但是期间将不会向云监控上报监控数据。

 **说明：** 动态计算需要扩缩容的ECS实例数量时，处于预热状态的实例不计入现有实例数量。

 取值范围：0~86400，单位：秒，默认值：300。

 |
|MetricName|String|否|CpuUtilization|预定义监控项，仅适用于目标追踪伸缩规则，且此时该项必选。可选值：

 -   CpuUtilization：平均CPU使用率
-   ClassicInternetRx：经典网络公网入流量平均值
-   ClassicInternetTx：经典网络公网出流量平均值
-   VpcInternetRx：VPC网络公网入流量平均值
-   VpcInternetTx：VPC网络公网出流量平均值
-   IntranetRx：内网入流量平均值
-   IntranetTx ：内网出流量平均值

 |
|TargetValue|Float|否|0.125|目标值，仅适用于目标追踪伸缩规则，且此时该项必选。TargetValue 最多保留小数点后三位，且必须大于 0。

 |
|DisableScaleIn|Boolean|否|false|是否禁用缩容，仅适用于目标追踪伸缩规则。 默认值：false。

 |
|StepAdjustment.N.MetricIntervalLowerBound|Float|否|1.0|分步步骤的下边界，取值范围-9.999999E18~9.999999E18。

 |
|StepAdjustment.N.MetricIntervalUpperBound|Float|否|5.0|分步步骤的上边界，取值范围-9.999999E18~9.999999E18。

 |
|StepAdjustment.N.ScalingAdjustment|Integer|否|1|分步步骤对应的实例扩展数量。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |
|ScalingRuleAri|String|ari:acs:ess:cn-qingdao:1344371:scalingrule/eMKWG8SRNb9dBLAjweNI1Ik|伸缩规则的唯一标识符。

 |
|ScalingRuleId|String|eMKWG8SRNb9dBLAjweN\*\*\*\*|伸缩规则的 ID，由系统生成，全局唯一。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=CreateScalingRule
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&AdjustmentType=QuantityChangeInCapacity
&AdjustmentValue=-10
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateScalingRuleResponse>
  <ScalingRuleAri>ari:acs:ess:cn-qingdao:1344371:scalingrule/eMKWG8SRNb9dBLAjweNI1Ik</ScalingRuleAri>
  <ScalingRuleId>eMKWG8SRNb9dBLAjweN****</ScalingRuleId>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</CreateScalingRuleResponse>

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

