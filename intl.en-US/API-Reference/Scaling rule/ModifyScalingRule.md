# ModifyScalingRule {#doc_api_Ess_ModifyScalingRule .reference}

You can call this operation to modify an existing scaling rule and redefine the scaling action it executes.

## Description {#description .section}

You can call this operation to modify specific attributes of an existing scaling rule to apply the rule in new scenarios.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=ModifyScalingRule) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|ScalingRuleId|String|Yes|eMKWG8SRNb9dBLAjweN\*\*\*\*|The ID of the scaling rule.

 |
|Action|String|No|ModifyScalingRule|The operation that you want to perform. Set the value to ModifyScalingRule.

 |
|AdjustmentType|String|No|QuantityChangeInCapacity|The method used by the scaling rule to adjust the number of instances. This parameter is only applicable to simple scaling rules. Valid values:

 -   QuantityChangeInCapacity: adds or removes a specified number of ECS instances.
-   PercentChangeInCapacity: adds or removes a specified proportion of ECS instances.
-   TotalCapacity: adds or removes ECS instances to ensure that the current scaling group has a specified number of ECS instances.

 |
|AdjustmentValue|Integer|No|100|The specified number of ECS instances to be adjusted in the scaling rule. This parameter is only applicable to simple scaling rules. The number of ECS instances to be adjusted in a single scaling activity cannot exceed 500. Valid values:

 -   If AdjustmentType is set to QuantityChangeInCapacity, the value range is -500 to 500.
-   If AdjustmentType is set to PercentChangeInCapacity, the value range is -100 to 10000.
-   If AdjustmentType is set to TotalCapacity, the value range is 0 to 1000.

 |
|Cooldown|Integer|No|60|The cooldown period in the scaling rule. This parameter is only applicable to simple scaling rules.

 Valid values: 0 to 86400. Unit: seconds. Default value: null.

 |
|DisableScaleIn|Boolean|No|true|Indicates whether to disable scale-in. This parameter is only applicable to target tracking scaling rules.

 |
|EstimatedInstanceWarmup|Integer|No|60|The warm-up period of the instance. This parameter is applicable to target tracking scaling rules and step scaling rules. The system adds ECS instances that are in the warm-up state to the scaling group, but does not report monitoring data to CloudMonitor during the warm-up period.

 **Note:** When calculating the number of ECS instances to be scaled, the system does not count instances in the warm-up state as part of the current capacity of the scaling group.

 Valid values: 0 to 86400. Unit: seconds.

 |
|MetricName|String|No|CpuUtilization|The predefined metric that you specify to monitor. This parameter is only applicable to target tracking scaling rules. Valid values:

 -   CpuUtilization: the average CPU utilization
-   ClassicInternetRx: the average Internet inbound traffic over the classic network
-   ClassicInternetTx: the average Internet outbound traffic over the classic network
-   VpcInternetRx: the average Internet inbound traffic over the VPC network
-   VpcInternetTx: the average Internet outbound traffic over the VPC network
-   IntranetRx: the average intranet inbound traffic
-   IntranetTx: the average intranet outbound traffic

 |
|MinAdjustmentMagnitude|Integer|No|1|The minimum number of instances to be scaled in a scaling rule. This parameter only takes effect when the scaling rule type is SimpleScalingRule or StepScalingRule and AdjustmentType is PercentChangeInCapacity.

 |
|ScalingRuleName|String|No|TestSr|The display name of the scaling rule. The name must be 2 to 40 characters in length. It must start with a letter or digit. It can contain digits, uppercase letters, lowercase letters, underscores \(\_\), hyphens \(-\), and periods \(.\). This parameter must be unique within a scaling group. The default value is the ID of the scaling rule.

 |
|StepAdjustment.N.MetricIntervalLowerBound|Float|No|1.0|The lower limit value specified in step adjustment N. Valid values: -9.999999E18 to 9.999999E18.

 |
|StepAdjustment.N.MetricIntervalUpperBound|Float|No|5.0|The upper limit value specified in step adjustment N. Valid values: -9.999999E18 to 9.999999E18.

 |
|StepAdjustment.N.ScalingAdjustment|Integer|No|1|The specified number of instances to be scaled in step adjustment N.

 |
|TargetValue|Float|No|0.125|The value of the target metric. This parameter is only applicable to target tracking scaling rules. The value of TargetValue must be greater than 0 and can have a maximum of three decimal places.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=ModifyScalingRule
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&AdjustmentType=QuantityChangeInCapacity
&AdjustmentValue=-10
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyScalingRuleResponse>
  <ScalingRuleAri>ari:acs:ess:cn-qingdao:1344371:scalingrule/eMKWG8SRNb9dBLAjweNI1Ik</ScalingRuleAri>
  <ScalingRuleId>eMKWG8SRNb9dBLAjweN****</ScalingRuleId>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyScalingRuleResponse>

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

|The error message returned when the specified scaling group does not exist in the current account.

|
|400

|InvalidScalingRuleName.Duplicate

|The specified value of parameter <parameter name\> is duplicated.

|The error message returned when the scaling rule name already exists.

|
|400

|QuotaExceeded.ScalingRule

|Scaling rule quota exceeded in the specified scaling group.

|The error message returned when the number of scaling rules in the specified scaling group has reached the upper limit.

|
|400

|TargetTrackingScalingRule.UnsupportedMetric

|Specific metric is not supported for target tracking scaling rule.

|The error message returned when target tracking scaling rules do not support the specified monitoring metric.

|
|400

|TargetTrackingScalingRule.DumplicateMetric

|Only one TargetTrackingScaling rule for a given metric specification is allowed.

|The error message returned when the monitoring metric is already specified for a target tracking scaling rule in the scaling group.

|
|400

|InvalidMinAdjustmentMagnitudeMismatchAdjustmentType

|MinAdjustmentMagnitude is not supported by the specified adjustment type.

|The error message returned when the MinAdjustmentMagnitude parameter cannot be applied to the specified adjustment method of the scaling rule.

|
|400

|InvalidStepAdjustments.MultipleNullUpperBound

|At most one StepAdjustment may have an unspecified upper bound.

|The error message returned when a step adjustment with an unspecified upper limit value already exists.

|
|400

|InvalidStepAdjustments.MultipleNullLowerBound

|At most one StepAdjustment may have an unspecified lower bound.

|The error message returned when a step adjustment with an unspecified lower limit value already exists.

|
|400

|InvalidStepAdjustments.NoNullLowerBound

|There must be a StepAdjustment with an unspecified lower bound when one StepAdjustment has a negative lower bound.

|The error message returned when the lower limit value of a step adjustment is negative, but a different step adjustment with an unspecified lower limit value does not exist.

|
|400

|InvalidStepAdjustments.NoNullUpperBound

|There must be a StepAdjustment with an unspecified upper bound when one StepAdjustment has a positive upper bound.

|The error message returned when the lower limit value of a step adjustment is positive, but a different step adjustment with an unspecified upper limit value does not exist.

|
|400

|InvalidStepAdjustments.Gap

|StepAdjustment intervals can not have gaps between them.

|The error message returned when the specified ranges of step adjustments have gaps between them.

|
|400

|InvalidStepAdjustments.Overlap

|StepAdjustment intervals can not overlap.

|The error message returned when the specified ranges of step adjustments overlap.

|
|400

|InvalidStepAdjustments.LowerGtUpper

|LowerBound must be less than the UpperBound for StepAdjustment :%s.

|The error message returned when the lower limit value of a step adjustment is greater than or equal to the upper limit value.

|
|400

|InvalidStepAdjustments.BothNull

|Both lower and upper bounds of a StepAdjustment can not be left unspecified.

|The error message returned when neither the upper limit value nor the lower limit value for a step adjustment is specified.

|
|400

|InvalidStepAdjustments.MaxNum

|Your scaling rule can have at most %s StepAdjustments.

|The error message returned when the maximum number of step adjustments in a scaling group has reached the upper limit.

|
|400

|StepBeyondPermitRange

|Specific parameter "%s" beyond permit range.

|The error message returned when the specified upper limit value or lower limit value of a step adjustment is not within the range of valid values.

|

