# CreateScalingRule {#doc_api_Ess_CreateScalingRule .reference}

You can call this operation to create a scaling rule, so as to define a scaling action.

## Description {#description .section}

A scaling rule defines the scaling action to be executed, such as adding or removing a certain number of ECS instances. If the number of ECS instances after a scaling rule is executed is smaller than MinSize or greater than MaxSize of a scaling group, Auto Scaling automatically adds or removes ECS instances. In this case, Auto Scaling keeps the number of ECS instances in the scaling group to MinSize or MaxSize while the specified number of ECS instances to be adjusted in the scaling rule is ignored and remains unchanged. You can create scaling rules based on input parameters.

-   Example 1: A scaling group has a MaxSize of 3, a TotalCapacity of 2, and a scaling rule of adding three ECS instances. When executing this scaling rule, Auto Scaling adds only one ECS instance to the group to prevent TotalCapacity \(the current number of ECS instances in the group\) from exceeding MaxSize \(the maximum number of ECS instances allowed in the group\).
-   Example 2: A scaling group has a MinSize of 2, a TotalCapacity of 3, and a scaling rule of removing five ECS instances. When executing this scaling rule, Auto Scaling removes only one ECS instance from the group to prevent TotalCapacity \(the current number of ECS instances in the group\) from becoming smaller than MinSize \(the minimum number of ECS instances allowed in the group\).

You can create scaling rules based on input parameters.

-   When AdjustmentType is set to TotalCapacity, the number of ECS instances currently in the scaling group is adjusted to the specified value. The value of AdjustmentValue must be greater than or equal to 0.
-   When AdjustmentType is set to QuantityChangeInCapacity or PercentChangeInCapacity, a positive value of AdjustmentValue indicates the number of ECS instances to be added, and a negative value of AdjustmentValue indicates the number of ECS instances to be removed.
-   When AdjustmentType is set to PercentChangeInCapacity, Auto Scaling rounds the number of ECS instances to be adjusted to a nearest integer based on the formula: Number of ECS instances to be adjusted = Current number of ECS instances \(Total Capacity\) x AdjustmentValue/100.
-   When the cooldown time \(Cooldown\) is specified in a scaling rule, the specified time applies to the scaling group after this rule is executed. Otherwise, DefaultCooldown applies to the scaling group.
-   A scaling group can have a maximum of 50 scaling rules.
-   The following operations use the unique identifier of a scaling rule \(ScalingRuleAri\) returned by CreateScalingRule:
    -   ExecuteScalingRule: You can call this operation to manually execute a specified scaling rule by setting ScalingRuleAri to the identifier.
    -   CreateScheduledTask: You can call this operation to create a scheduled task for a specified scaling rule by setting ScheduledAction to the identifier.

## Debugging {#apiExplorer .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=CreateScalingRule) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|ScalingGroupId|String|Yes|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|The ID of the scaling group to which the scaling rule belongs.

 |
|Action|String|No|CreateScalingRule|The operation that you want to perform. Set the value to CreateScalingRule.

 |
|ScalingRuleName|String|No|TestSr|The display name of the scaling rule. The name must be 2 to 40 characters in length. It must start with a letter or digit. It can contain digits, uppercase letters, lowercase letters, underscores \(\_\), hyphens \(-\), and periods \(.\). This parameter must be unique within a scaling group. The default value is the ID of the scaling rule.

 |
|Cooldown|Integer|No|60|The cooldown time in the scaling rule. This parameter is only applicable to simple scaling rules. Valid values: 0 to 86400. Unit: seconds. Default value: null.

 |
|MinAdjustmentMagnitude|Integer|No|1|The minimum number of ECS instances to be adjusted in a scaling rule. This parameter only takes effect when the scaling rule type is SimpleScalingRule or StepScalingRule and AdjustmentType is PercentChangeInCapacity.

 |
|AdjustmentType|String|No|QuantityChangeInCapacity|The adjustment method of the scaling rule. This parameter is required and only applicable to simple scaling rules. Valid values:

 -   QuantityChangeInCapacity: adds or removes a specified number of ECS instances.
-   PercentChangeInCapacity: adds or removes a specified proportion of ECS instances.
-   TotalCapacity: adds or removes ECS instances to ensure that the current scaling group has a specified number of ECS instances.

 |
|AdjustmentValue|Integer|No|100|The number of ECS instances to be adjusted in the scaling rule. This parameter is required and only applicable to simple scaling rules. The number of ECS instances to be adjusted in a single scaling activity cannot exceed 500. Valid values:

 -   If AdjustmentType is set to QuantityChangeInCapacity, the value range is -500 to 500.
-   If AdjustmentType is set to PercentChangeInCapacity, the value range is -100 to 10000.
-   If AdjustmentType is set to TotalCapacity, the value range is 0 to 1000.

 |
|ScalingRuleType|String|No|SimpleScalingRule|The type of the scaling rule. Valid values:

 -   SimpleScalingRule: scales ECS instances based on the values of AdjustmentType and AdjustmentValue.
-   TargetTrackingScalingRule: dynamically calculates the number of ECS instances to be adjusted and tries to keep the value of a predefined monitoring metric close to TargetValue.
-   StepScalingRule: scales ECS instances in steps based on specified thresholds and metric values.
-   PredictiveScalingRule: analyzes historical monitoring data of the scaling group and then predicts the future values of monitored metrics based on machine learning, then automatically creates scheduled tasks to set the boundary values for the scaling group.

 Default value: SimpleScalingRule.

 |
|EstimatedInstanceWarmup|Integer|No|300|The warm-up period of the ECS instances. This parameter is applicable to target tracking scaling rules and step scaling rules. The system adds ECS instances that are in the warm-up state to the scaling group, but does not report monitoring data to CloudMonitor during the warm-up period.

 **Note:** When calculating the number of ECS instances to be adjusted, the system does not count ECS instances in the warm-up state as part of the current capacity of the scaling group.

 Valid values: 0 to 86400. Unit: seconds. Default value: 300.

 |
|MetricName|String|No|CpuUtilization|The predefined metric that you specify to monitor. This parameter is required and only applicable to target tracking scaling rules and predictive scaling rules.

 Valid values for a target tracking scaling rule:

 -   CpuUtilization: the average CPU utilization
-   ClassicInternetRx: the average Internet inbound traffic over the classic network
-   ClassicInternetTx: the average Internet outbound traffic over the classic network
-   VpcInternetRx: the average Internet inbound traffic over the VPC network
-   VpcInternetTx: the average Internet outbound traffic over the VPC network
-   IntranetRx: the average intranet inbound traffic
-   IntranetTx: the average intranet outbound traffic

 Valid values for a predictive scaling rule:

 -   CpuUtilization: the average CPU utilization
-   IntranetRx: the average intranet inbound traffic
-   IntranetTx: the average intranet outbound traffic

 |
|TargetValue|Float|No|0.125|The target value of a metric. This parameter is required and only applicable to target tracking scaling rules and predictive scaling rules. The value of TargetValue must be greater than 0 and can have a maximum of three decimal places.

 |
|DisableScaleIn|Boolean|No|false|Specifies whether to disable scale-in. This parameter is only applicable to target tracking scaling rules. Default value: false.

 |
|InitialMaxSize|Integer|No|100|The maximum number of ECS instances in the scaling group, which is used together with PredictiveValueBehavior.

 Default value: the same as the value of MaxSize.

 |
|PredictiveScalingMode|String|No|PredictAndScale|The mode of the predictive scaling rule. Valid values:

 -   PredictAndScale: generates both forecasts and forecast tasks.
-   PredictOnly: generates forecasts but does not generate forecast tasks.

 Default value: PredictAndScale.

 |
|PredictiveTaskBufferTime|Integer|No|30|The amount of buffer time ahead of the forecast task execution time. By default, all scheduled tasks that are automatically created for a predictive scaling rule are executed at the beginning of each hour. You can set a buffer time to execute forecast tasks ahead of schedule, so that resources can be prepared in advance. Valid values: 0 to 60.

 Default value: 0.

 |
|PredictiveValueBehavior|String|No|MaxOverridePredictiveValue|The action taken on the predicted maximum value. Valid values:

 -   MaxOverridePredictiveValue: uses the initial maximum capacity as the maximum value for forecast tasks when the predicted value is greater than the initial maximum capacity.
-   PredictiveValueOverrideMax: uses the predicted value as the maximum value for forecast tasks when the predicted value is greater than the initial maximum capacity.
-   PredictiveValueOverrideMaxWithBuffer: increases the predicted value with a ratio, which is specified by PredictiveValueBuffer. If the value after increase is greater than the initial maximum capacity, the value after increase is used as the maximum value for forecast tasks.

 Default value: MaxOverridePredictiveValue.

 |
|PredictiveValueBuffer|Integer|No|50|The ratio of the increment to the predicted value when PredictiveValueBehavior is set to PredictiveValueOverrideMaxWithBuffer. When the value after increase is greater than the initial maximum capacity, the value after increase is used for forecast tasks. Valid values: 0 to 100.

 Default value: 0.

 |
|StepAdjustment.N.MetricIntervalLowerBound|Float|No|1.0|The lower limit value specified in step adjustment N. Valid values: -9.999999E18 to 9.999999E18.

 |
|StepAdjustment.N.MetricIntervalUpperBound|Float|No|5.0|The upper limit value specified in step adjustment N. Valid values: -9.999999E18 to 9.999999E18.

 |
|StepAdjustment.N.ScalingAdjustment|Integer|No|1|The specified number of ECS instances to be adjusted in step adjustment N.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. The system returns a unique RequestId for each API request, regardless of whether the API operation is successful.

 |
|ScalingRuleAri|String|ari:acs:ess:cn-qingdao:1344371:scalingrule/eMKWG8SRNb9dBLAjweNI1Ik|The unique identifier of the scaling rule.

 |
|ScalingRuleId|String|eMKWG8SRNb9dBLAjweN\*\*\*\*|The globally unique scaling rule ID generated by the system.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}

http://ess.aliyuncs.com/?Action=CreateScalingRule
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&AdjustmentType=QuantityChangeInCapacity
&AdjustmentValue=-10
&<Common request parameters>

```

Sample success response

`XML` format

``` {#xml_return_success_demo}
<CreateScalingRuleResponse>
  <ScalingRuleAri>ari:acs:ess:cn-qingdao:1344371:scalingrule/eMKWG8SRNb9dBLAjweNI1Ik</ScalingRuleAri>
  <ScalingRuleId>eMKWG8SRNb9dBLAjweN****</ScalingRuleId>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</CreateScalingRuleResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"ScalingRuleAri":"ari:acs:ess:cn-qingdao:1344371:scalingrule/eMKWG8SRNb9dBLAjweNI1Ik",
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"ScalingRuleId":"eMKWG8SRNb9dBLAjweN****"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Ess)

|HTTP status code

|Error code

|Error message

|Description

|
|------------------|------------|---------------|-------------|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist in the current account.

|
|400

|InvalidScalingRuleName.Duplicate

|The specified value of parameter <parameter name\> is duplicated.

|The error message returned because the scaling rule name already exists.

|
|400

|QuotaExceeded.ScalingRule

|Scaling rule quota exceeded in the specified scaling group.

|The error message returned because the number of scaling rules in the specified scaling group has reached the upper limit.

|
|400

|TargetTrackingScalingRule.UnsupportedMetric

|Specific metric is not supported for target tracking scaling rule.

|The error message returned because target tracking scaling rules do not support the specified monitoring metric.

|
|400

|TargetTrackingScalingRule.DumplicateMetric

|Only one TargetTrackingScaling rule for a given metric specification is allowed.

|The error message returned because the monitoring metric is already specified for a target tracking scaling rule in the scaling group.

|
|400

|InvalidMinAdjustmentMagnitudeMismatchAdjustmentType

|MinAdjustmentMagnitude is not supported by the specified adjustment type.

|The error message returned because the MinAdjustmentMagnitude parameter cannot be applied to the specified adjustment method of the scaling rule.

|
|400

|InvalidStepAdjustments.MultipleNullUpperBound

|At most one StepAdjustment may have an unspecified upper bound.

|The error message returned because a step adjustment with an unspecified upper limit value already exists.

|
|400

|InvalidStepAdjustments.MultipleNullLowerBound

|At most one StepAdjustment may have an unspecified lower bound.

|The error message returned because a step adjustment with an unspecified lower limit value already exists.

|
|400

|InvalidStepAdjustments.NoNullLowerBound

|There must be a StepAdjustment with an unspecified lower bound when one StepAdjustment has a negative lower bound.

|The error message returned because the lower limit value of a step adjustment is negative, but a different step adjustment with an unspecified lower limit value does not exist.

|
|400

|InvalidStepAdjustments.NoNullUpperBound

|There must be a StepAdjustment with an unspecified upper bound when one StepAdjustment has a positive upper bound.

|The error message returned because the upper limit value of a step adjustment is positive, but a different step adjustment with an unspecified upper limit value does not exist.

|
|400

|InvalidStepAdjustments.Gap

|StepAdjustment intervals cannot have gaps between them.

|The error message returned because the specified ranges of step adjustments have gaps between them.

|
|400

|InvalidStepAdjustments.Overlap

|StepAdjustment intervals cannot overlap.

|The error message returned because the specified ranges of step adjustments overlap.

|
|400

|InvalidStepAdjustments.LowerGtUpper

|LowerBound must be less than the UpperBound for StepAdjustment :%s.

|The error message returned because the lower limit value of a step adjustment is greater than or equal to the upper limit value.

|
|400

|InvalidStepAdjustments.BothNull

|Both lower and upper bounds of a StepAdjustment cannot be left unspecified.

|The error message returned because neither the upper limit value nor the lower limit value for a step adjustment is specified.

|
|400

|InvalidStepAdjustments.MaxNum

|Your scaling rule can have at most %s StepAdjustments.

|The error message returned because the maximum number of step adjustments in a scaling group has reached the upper limit.

|
|400

|StepBeyondPermitRange

|Specific parameter "%s" beyond permit range.

|The error message returned because the specified upper limit value or lower limit value of a step adjustment is not within the range of valid values.

|

