# CreateScalingRule

You can call this operation to create a scaling rule.

## Description

A scaling rule defines a specific scaling activity, such as adding or removing N ECS instances. If the number of ECS instances in a scaling group after a scaling rule is executed is less than the MinSize value or greater than the MaxSize value, Auto Scaling automatically adds or removes ECS instances to or from the scaling group. In this way, Auto Scaling keeps the number of ECS instances in the scaling group to the MinSize or MaxSize value while the specified number of ECS instances to be scaled in the scaling rule remains unchanged. Examples:

-   A scaling group has a MaxSize value of 3 and a scaling rule of adding three ECS instances, and contains two ECS instances. When this scaling rule is executed, Auto Scaling adds only one ECS instance to the scaling group. The specified number of ECS instances to be scaled in the scaling rule is still 3.
-   A scaling group has a MinSize of value 2 and a scaling rule of removing five ECS instances, and contains three ECS instances. When this scaling rule is executed, Auto Scaling removes only one ECS instance from the scaling group. The specified number of ECS instances to be scaled in the scaling rule is still 5.

Take note of the following parameter descriptions:

-   When AdjustmentType is set to TotalCapacity, the number of ECS instances in the scaling group is adjusted to the specified value. The value of AdjustmentValue must be greater than or equal to 0.
-   When AdjustmentType is set to QuantityChangeInCapacity or PercentChangeInCapacity, a positive value of AdjustmentValue indicates the number of ECS instances to be added, and a negative value of AdjustmentValue indicates the number of ECS instances to be removed.
-   When AdjustmentType is set to PercentChangeInCapacity, Auto Scaling rounds the value calculated based on based on the following formula to a nearest integer to determine the number of ECS instances to be scaled: Number of ECS instances to be scaled = Current number of ECS instances \(Total Capacity\) x AdjustmentValue/100.
-   When the cooldown time \(Cooldown\) is specified in a scaling rule, the specified time applies to the scaling group after this rule is executed. Otherwise, DefaultCooldown applies to the scaling group.
-   Only a limited number of scaling rules can be created for a scaling group. For more information, see [Limits](~~25863~~).
-   The following API operations use the unique identifier of a scaling rule \(ScalingRuleAri\) returned by CreateScalingRule:
    -   ExecuteScalingRule: You can call this operation to manually execute a specific scaling rule by setting ScalingRuleAri to the unique identifier.
    -   CreateScheduledTask: You can call this operation to create a scheduled task for a specific scaling rule by setting ScheduledAction to the unique identifier.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=CreateScalingRule&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateScalingRule|The operation that you want to perform. Set the value to CreateScalingRule. |
|ScalingGroupId|String|Yes|asg-bp1ffogfdauy0jw0\*\*\*\*|The region ID of the scaling group to which a scaling rule belongs. |
|ScalingRuleName|String|No|scalingrule\*\*\*\*|The name of the scaling rule. It must be 2 to 64 characters in length, and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a letter or a digit. The name of a scaling rule must be unique within the scaling group to which it belongs.

If this parameter is not specified, the ScalingRuleId value is used by default. |
|Cooldown|Integer|No|60|The cooldown period of the scaling rule. This parameter takes effect only when ScalingRuleType is set to SimpleScalingRule. Valid values: 0 to 86400. Unit: seconds.

This parameter is empty by default. |
|MinAdjustmentMagnitude|Integer|No|1|The minimum number of ECS instances to be scaled in a scaling rule. This parameter takes effect only when ScalingRuleType is set to SimpleScalingRule or StepScalingRule and AdjustmentType is set to PercentChangeInCapacity. |
|AdjustmentType|String|No|QuantityChangeInCapacity|The adjustment method of the scaling rule. This parameter is required and takes effect only when ScalingRuleType is set to SimpleScalingRule or StepScalingRule. Valid values:

-   QuantityChangeInCapacity: adds or removes the specified number of ECS instances to or from the scaling group.
-   PercentChangeInCapacity: adds or removes the specified percentage of ECS instances to or from the scaling group.
-   TotalCapacity: adjusts the number of ECS instances in the scaling group to the specified number. |
|AdjustmentValue|Integer|No|100|The adjustment value specified for the scaling rule. This parameter is required and takes effect only when ScalingRuleType is set to SimpleScalingRule or StepScalingRule. The number of ECS instances to be scaled in a single scaling activity cannot exceed 1,000. Valid values based on the AdjustmentType value:

-   Valid values when AdjustmentType is set to QuantityChangeInCapacity: -1000 to 1000
-   Valid values when AdjustmentType is set to PercentChangeInCapacity: -100 to 10000
-   Valid values when AdjustmentType is set to TotalCapacity: 0 to 2000 |
|ScalingRuleType|String|No|SimpleScalingRule|The type of the scaling rule. Valid values:

-   SimpleScalingRule: simple scaling rules, which scale the number of ECS instances based on the values of AdjustmentType and AdjustmentValue.
-   TargetTrackingScalingRule: target tracking scaling rules, which calculate the number of ECS instances to be scaled and try to keep the value of a predefined metric close to the value of TargetValue.
-   StepScalingRule: step scaling rules, which scale the number of ECS instances in steps based on specified thresholds and metric values.
-   PredictiveScalingRule: predicative scaling rules, which use machine learning to analyze historical monitoring data of the scaling group and predict the future values of metrics. Then, the predicative scaling rules automatically create scheduled tasks to set the boundary values for the scaling group.

Default value: SimpleScalingRule |
|EstimatedInstanceWarmup|Integer|No|300|The warmup period of an ECS instance. This parameter takes effect only when ScalingRuleType is set to TargetTrackingScalingRule or PredictiveScalingRule. Auto Scaling adds ECS instances that are in the warmup state to the scaling group, but does not report monitoring data to Cloud Monitor during the warmup period.

**Note:** Auto Scaling calculates the number of ECS instances to be scaled, but does not count ECS instances in the warmup state as part of the current capacity of the scaling group.

Valid values: 0 to 86400. Unit: seconds.

Default value: 300 |
|MetricName|String|No|CpuUtilization|The predefined metric to monitor. This parameter is required and takes effect only when ScalingRuleType is set to TargetTrackingScalingRule or PredictiveScalingRule.

Valid values for target tracking scaling rules:

-   CpuUtilization: the average CPU utilization
-   ClassicInternetRx: the average inbound public traffic over the classic network
-   ClassicInternetTx: the average outbound public traffic over the classic network
-   VpcInternetRx: the average inbound public traffic over a VPC
-   VpcInternetTx: the average outbound public traffic over a VPC
-   IntranetRx: the average inbound internal traffic
-   IntranetTx: the average outbound internal traffic

Valid values for predictive scaling rules:

-   CpuUtilization: the average CPU utilization
-   IntranetRx: the average inbound internal traffic
-   IntranetTx: the average outbound internal traffic |
|TargetValue|Float|No|0.125|The target value. This parameter is required and takes effect only when ScalingRuleType is set to TargetTrackingScalingRule or PredictiveScalingRule. The value must be greater than 0 and can have a maximum of three decimal places. |
|DisableScaleIn|Boolean|No|false|Specifies whether to disable scale-in. This parameter takes effect only when ScalingRuleType is set to TargetTrackingScalingRule.

Default value: false |
|ScaleInEvaluationCount|Integer|No|15|The number of consecutive times when the event-triggered task created for scale-in events meets the threshold conditions to trigger an alert. After a target tracking scaling rule is created, an event-triggered task is automatically created and associated with the target tracking scaling rule.

Default value: 15 |
|ScaleOutEvaluationCount|Integer|No|3|The number of consecutive times when the event-triggered task created for scale-out events meets the threshold conditions to trigger an alert. After a target tracking scaling rule is created, an event-triggered task is automatically created and associated with the target tracking scaling rule.

Default value: 3 |
|StepAdjustment.N.MetricIntervalLowerBound|Float|No|1.0|The lower limit value specified in a step adjustment. This parameter takes effect only when ScalingRuleType is set to StepScalingRule. Valid values: -9.999999E18 to 9.999999E18. |
|StepAdjustment.N.MetricIntervalUpperBound|Float|No|5.0|The upper limit value specified in a step adjustment. This parameter takes effect only when ScalingRuleType is set to StepScalingRule. Valid values: -9.999999E18 to 9.999999E18. |
|StepAdjustment.N.ScalingAdjustment|Integer|No|1|The specified number of ECS instances to be scaled in a step adjustment. This parameter takes effect only when ScalingRuleType is set to StepScalingRule. |
|PredictiveScalingMode|String|No|PredictAndScale|The mode of the predictive scaling rule. Valid values:

-   PredictAndScale: produces predictions and creates prediction tasks.
-   PredictOnly: produces predictions but does not create prediction tasks.

Default value: PredictAndScale |
|PredictiveValueBehavior|String|No|MaxOverridePredictiveValue|The action to take on the predicted maximum value. Valid values:

-   MaxOverridePredictiveValue: uses the initial maximum capacity as the maximum value for prediction tasks when the predicted value is greater than the initial maximum capacity.
-   PredictiveValueOverrideMax: uses the predicted value as the maximum value for prediction tasks when the predicted value is greater than the initial maximum capacity.
-   PredictiveValueOverrideMaxWithBuffer: increases the predicted value by a ratio which is specified by PredictiveValueBuffer. If the predicted value increased by this ratio is greater than the initial maximum capacity, the increased value is used as the maximum value for prediction tasks.

Default value: MaxOverridePredictiveValue |
|PredictiveValueBuffer|Integer|No|50|The ratio of the increment to the predicted value when PredictiveValueBehavior is set to PredictiveValueOverrideMaxWithBuffer. If the predicted value increased by this ratio is greater than the initial maximum capacity, the increased value is used as the maximum value for prediction tasks. Valid values: 0 to 100.

Default value: 0 |
|PredictiveTaskBufferTime|Integer|No|30|The amount of buffer time ahead of when the prediction task is executed. By default, all scheduled tasks that are automatically created for a predictive scaling rule are executed on the hour. You can set a buffer time to execute prediction tasks ahead of schedule, so that resources can be prepared in advance. Valid values: 0 to 60. Unit: minutes.

Default value: 0 |
|InitialMaxSize|Integer|No|100|The maximum number of ECS instances in the scaling group. This parameter is used in combination with the PredictiveValueBehavior parameter.

The default value of this parameter is the value of MaxSize. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|ScalingRuleAri|String|ari:acs:ess:cn-hangzhou:140692647406\*\*\*\*:scalingrule/asr-bp1dvirgwkoowxk7\*\*\*\*|The unique identifier of the scaling rule. |
|ScalingRuleId|String|asr-bp1dvirgwkoowxk7\*\*\*\*|The globally unique scaling rule ID generated by the system. |

## Examples

Sample requests

```
http://ess.aliyuncs.com/?Action=CreateScalingRule
&ScalingGroupId=asg-bp1ffogfdauy0jw0****
&AdjustmentType=QuantityChangeInCapacity
&AdjustmentValue=-10
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateScalingRuleResponse>   
      <ScalingRuleAri>ari:acs:ess:cn-hangzhou:140692647406****:scalingrule/asr-bp1dvirgwkoowxk7****</ScalingRuleAri>
      <ScalingRuleId>asr-bp1dvirgwkoowxk7****</ScalingRuleId>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</CreateScalingRuleResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "ScalingRuleId": "asr-bp1dvirgwkoowxk7****",
    "ScalingRuleAri": "ari:acs:ess:cn-hangzhou:140692647406****:scalingrule/asr-bp1dvirgwkoowxk7****"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist in the current account. |
|400

|InvalidScalingRuleName.Duplicate

|The specified value of parameter <parameter name\> is duplicated.

|The error message returned because the scaling rule name already exists. |
|400

|QuotaExceeded.ScalingRule

|Scaling rule quota exceeded in the specified scaling group.

|The error message returned because the maximum number of scaling rules in the specified scaling group has been reached. |
|400

|TargetTrackingScalingRule.UnsupportedMetric

|Specific metric is not supported for target tracking scaling rule.

|The error message returned because target tracking scaling rules do not support the specified monitoring metric. |
|400

|TargetTrackingScalingRule.DumplicateMetric

|Only one TargetTrackingScaling rule for a given metric specification is allowed.

|The error message returned because the monitoring metric is already specified for a target tracking scaling rule in the scaling group. |
|400

|InvalidMinAdjustmentMagnitudeMismatchAdjustmentType

|MinAdjustmentMagnitude is not supported by the specified adjustment type.

|The error message returned because the MinAdjustmentMagnitude parameter cannot be applied to the specified adjustment method of the scaling rule. |
|400

|InvalidStepAdjustments.MultipleNullUpperBound

|At most one StepAdjustment may have an unspecified upper bound.

|The error message returned because a step adjustment without an upper limit value already exists. |
|400

|InvalidStepAdjustments.MultipleNullLowerBound

|At most one StepAdjustment may have an unspecified lower bound.

|The error message returned because a step adjustment without a lower limit value already exists. |
|400

|InvalidStepAdjustments.NoNullLowerBound

|There must be a StepAdjustment with an unspecified lower bound when one StepAdjustment has a negative lower bound.

|The error message returned because the lower limit value of a step adjustment is negative, but a different step adjustment without a lower limit value does not exist. |
|400

|InvalidStepAdjustments.NoNullUpperBound

|There must be a StepAdjustment with an unspecified upper bound when one StepAdjustment has a positive upper bound.

|The error message returned because the upper limit value of a step adjustment is positive, but a different step adjustment without an upper limit value does not exist. |
|400

|InvalidStepAdjustments.Gap

|StepAdjustment intervals can not have gaps between them.

|The error message returned because the specified ranges of step adjustments have gaps between them. |
|400

|InvalidStepAdjustments.Overlap

|StepAdjustment intervals can not overlap.

|The error message returned because the specified ranges of step adjustments overlap. |
|400

|InvalidStepAdjustments.LowerGtUpper

|LowerBound must be less than the UpperBound for StepAdjustment :%s.

|The error message returned because the lower limit value of a step adjustment is greater than or equal to the upper limit value. |
|400

|InvalidStepAdjustments.BothNull

|Both lower and upper bounds of a StepAdjustment can not be left unspecified.

|The error message returned because the upper limit value or the lower limit value for a step adjustment must be specified. |
|400

|InvalidStepAdjustments.MaxNum

|Your scaling rule can have at most %s StepAdjustments.

|The error message returned because the maximum number of step adjustments in a scaling group has been reached. |
|400

|StepBeyondPermitRange

|Specific parameter "%s" beyond permit range.

|The error message returned because the specified upper limit value or lower limit value of a step adjustment is not within the range of valid values. |

