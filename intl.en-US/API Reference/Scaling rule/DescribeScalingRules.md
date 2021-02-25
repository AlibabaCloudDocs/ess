# DescribeScalingRules

You can call this operation to query all scaling rules in a scaling group and list information about the scaling rules.

## Description

You can specify a scaling group ID to query all scaling rules in the scaling group. You can also specify the scaling rule ID, name, unique identifier, and type in the request parameters as filter conditions.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeScalingRules&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeScalingRules|The operation that you want to perform. Set the value to DescribeScalingRules. |
|RegionId|String|Yes|cn-qingdao|The region ID of the scaling group. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default value: 1 |
|PageSize|Integer|No|50|The number of entries to return on each page. Valid values: 1 to 50.

Default value: 10 |
|ScalingGroupId|String|No|asg-bp1ffogfdauy0jw0\*\*\*\*|The ID of the scaling group. |
|ScalingRuleType|String|No|SimpleScalingRule|The type of the scaling rule. Valid values:

-   SimpleScalingRule: simple scaling rules, which scale the number of ECS instances based on the values of AdjustmentType and AdjustmentValue.
-   TargetTrackingScalingRule: target tracking scaling rules, which calculate the number of ECS instances to be scaled and try to keep the value of a predefined metric close to the value of TargetValue.
-   StepScalingRule: step scaling rules, which scale the number of ECS instances in steps based on specified thresholds and metric values.
-   PredictiveScalingRule: predicative scaling rules, which use machine learning to analyze historical monitoring data of the scaling group and predict the future values of metrics. Then, the predicative scaling rules automatically create scheduled tasks to set the boundary values for the scaling group. |
|ShowAlarmRules|Boolean|No|false|Specifies whether to return Cloud Monitor event-triggered tasks associated with scaling rules. Valid values:

-   true: The Cloud Monitor event-triggered tasks associated with a scaling rule are returned.
-   false: The Cloud Monitor event-triggered tasks associated with a scaling rule are not returned.

Default value: false |
|ScalingRuleId.N|RepeatList|No|asr-bp1dvirgwkoowxk7\*\*\*\*|The ID of scaling rule N to be queried. Valid values of N: 1 to 10. |
|ScalingRuleName.N|RepeatList|No|scalingrule\*\*\*\*|The name of scaling rule N to be queried. Valid values of N: 1 to 10. |
|ScalingRuleAri.N|RepeatList|No|ari:acs:ess:cn-hangzhou:140692647406\*\*\*\*:scalingrule/asr-bp1dvirgwkoowxk7\*\*\*\*|The unique identifier of scaling rule N to be queried. Valid values of N: 1 to 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|50|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|ScalingRules|Array of ScalingRule| |Details about the scaling rules. |
|ScalingRule| | | |
|AdjustmentType|String|QuantityChangeInCapacity|The adjustment mode of the scaling rule. Valid values:

-   QuantityChangeInCapacity: adds or removes the specified number of ECS instances to or from the scaling group.
-   PercentChangeInCapacity: adds or removes the specified percentage of ECS instances to or from the scaling group.
-   TotalCapacity: adjusts the number of ECS instances in the scaling group to the specified number. |
|AdjustmentValue|Integer|1|The adjustment value specified for the scaling rule. |
|Alarms|Array of Alarm| |The Cloud Monitor event-triggered tasks associated with scaling rules. The Cloud Monitor event-triggered tasks associated with scaling rules are returned only when the ShowAlarmRules parameter is set to true. Otherwise, an empty list is returned. |
|Alarm| | | |
|AlarmTaskId|String|asg-bp18p2yfxow2dloq\*\*\*\*\_1f9458d1-70e1-4bee-8c7f-7a47695b\*\*\*\*|The ID of the event-triggered task associated with the scaling rule. |
|AlarmTaskName|String|alarmtask\*\*\*\*|The name of the event-triggered task associated with the scaling rule. |
|ComparisonOperator|String|\>=|The comparison operator between the metric value and the threshold for the event-triggered task associated with the scaling rule. It indicates the relationship in which the metric value and the threshold can meet the condition. Valid values:

-   \>=: The metric value is greater than or equal to the threshold.
-   <=: The metric value is less than or equal to the threshold.
-   \>: The metric value is greater than the threshold.
-   <: The metric value is less than the threshold. |
|Dimensions|Array of Dimension| |The dimensions of the event-triggered task associated with the scaling rule. |
|Dimension| | | |
|DimensionKey|String|scaling\_group|The key values of dimensions associated with a metric. Valid values:

-   scaling\_group: the ID of the scaling group
-   userId: the ID of the user account |
|DimensionValue|String|asg-bp18p2yfxow2dloq\*\*\*\*|The attribute values of dimensions associated with a metric. |
|EvaluationCount|Integer|3|The number of consecutive times when the event-triggered task associated with a scaling rule meets the threshold expression to trigger an alert. |
|MetricName|String|CpuUtilization|The name of the metric of the event-triggered task associated with the scaling rule. |
|Statistics|String|Average|The statistical method of the event-triggered task associated with the scaling rule. Valid values:

-   Average
-   Maximum
-   Minimum |
|Threshold|Float|50|The alert threshold for the event-triggered task associated with the scaling rule. |
|Cooldown|Integer|20|The cooldown period of the scaling rule. This parameter takes effect only when ScalingRuleType is set to SimpleScalingRule. Valid values: 0 to 86400. Unit: seconds. |
|DisableScaleIn|Boolean|true|Indicates whether scale-in is disabled. This parameter takes effect only when ScalingRuleType is set to TargetTrackingScalingRule. Valid values:

-   true: Scale-in is disabled.
-   false: Scale-in is enabled. |
|EstimatedInstanceWarmup|Integer|300|The warmup period of an ECS instance. |
|InitialMaxSize|Integer|100|The maximum number of ECS instances in the scaling group. This parameter is used in combination with the PredictiveValueBehavior parameter. |
|MaxSize|Integer|2|The maximum number of ECS instances in the scaling group. |
|MetricName|String|CpuUtilization|The predefined metric to monitor. This parameter is required and takes effect only when ScalingRuleType is set to TargetTrackingScalingRule or PredictiveScalingRule.

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
|MinAdjustmentMagnitude|Integer|1|The minimum number of ECS instances that can be scaled by using a scaling rule. This parameter takes effect only when ScalingRuleType is set to SimpleScalingRule or StepScalingRule and AdjustmentType is set to PercentChangeInCapacity. |
|MinSize|Integer|1|The minimum number of ECS instances in the scaling group. |
|PredictiveScalingMode|String|PredictAndScale|The mode of the predictive scaling rule. Valid values:

-   PredictAndScale: produces predictions and creates prediction tasks.
-   PredictOnly: produces predictions but does not create prediction tasks. |
|PredictiveTaskBufferTime|Integer|30|The amount of buffer time ahead of when the prediction task is executed. By default, all scheduled tasks that are automatically created for a predictive scaling rule are executed on the hour. You can set a buffer time to execute prediction tasks ahead of schedule, so that resources can be prepared in advance. Valid values: 0 to 60. Unit: minutes. |
|PredictiveValueBehavior|String|MaxOverridePredictiveValue|The action to take on the predicted maximum value. Valid values:

-   MaxOverridePredictiveValue: uses the initial maximum capacity as the maximum value for prediction tasks when the predicted value is greater than the initial maximum capacity.
-   PredictiveValueOverrideMax: uses the predicted value as the maximum value for prediction tasks when the predicted value is greater than the initial maximum capacity.
-   PredictiveValueOverrideMaxWithBuffer: increases the predicted value by a ratio which is specified by PredictiveValueBuffer. If the predicted value increased by this ratio is greater than the initial maximum capacity, the increased value is used as the maximum value for prediction tasks. |
|PredictiveValueBuffer|Integer|50|The ratio of the increment to the predicted value when PredictiveValueBehavior is set to PredictiveValueOverrideMaxWithBuffer. If the predicted value increased by this ratio is greater than the initial maximum capacity, the increased value is used as the maximum value for prediction tasks. Valid values: 0 to 100. |
|ScaleInEvaluationCount|Integer|15|The number of consecutive times when the event-triggered task created for scale-in events meets the threshold conditions to trigger an alert. After a target tracking scaling rule is created, an event-triggered task is automatically created and associated with the target tracking scaling rule. |
|ScaleOutEvaluationCount|Integer|3|The number of consecutive times when the event-triggered task created for scale-out events meets the threshold conditions to trigger an alert. After a target tracking scaling rule is created, an event-triggered task is automatically created and associated with the target tracking scaling rule. |
|ScalingGroupId|String|asg-bp1ffogfdauy0jw0\*\*\*\*|The ID of the scaling group. |
|ScalingRuleAri|String|ari:acs:ess:cn-hangzhou:140692647406\*\*\*\*:scalingrule/asr-bp1dvirgwkoowxk7\*\*\*\*|The unique identifier of the scaling rule. |
|ScalingRuleId|String|asr-bp1dvirgwkoowxk7\*\*\*\*|The ID of the scaling rule. |
|ScalingRuleName|String|scalingrule\*\*\*\*|The name of the scaling rule. |
|ScalingRuleType|String|SimpleScalingRule|The type of the scaling rule. Valid values:

-   SimpleScalingRule: simple scaling rules, which scale the number of ECS instances based on the values of AdjustmentType and AdjustmentValue.
-   TargetTrackingScalingRule: target tracking scaling rules, which calculate the number of ECS instances to be scaled and try to keep the value of a predefined metric close to the value of TargetValue.
-   StepScalingRule: step scaling rules, which scale ECS instances in steps based on specified thresholds and metric values.
-   PredictiveScalingRule: predictive scaling rules, which use machine learning to analyze historical monitoring data of the scaling group and predict the future values of metrics. Then, the predictive scaling rules automatically create scheduled tasks to set the boundary values for the scaling group. |
|StepAdjustments|Array of StepAdjustment| |The step adjustments of the step scaling rule. |
|StepAdjustment| | | |
|MetricIntervalLowerBound|Float|1.0|The lower limit value specified in a step adjustment. Valid values: -9.999999E18 to 9.999999E18. |
|MetricIntervalUpperBound|Float|5.0|The upper limit value specified in a step adjustment. Valid values: -9.999999E18 to 9.999999E18. |
|ScalingAdjustment|Integer|1|The specified number of ECS instances scaled in a step adjustment. |
|TargetValue|Float|0.125|The target value. |
|TotalCount|Integer|1|The total number of scaling rules. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DescribeScalingRules
&RegionId=cn-qingdao
&ScalingGroupId=asg-bp1ffogfdauy0jw0****
&PageSize=50
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeScalingRulesResponse>
      <PageNumber>1</PageNumber>
      <PageSize>50</PageSize>
      <ScalingRules>
            <ScalingRule>
                  <AdjustmentType>QuantityChangeInCapacity</AdjustmentType>
                  <AdjustmentValue>1</AdjustmentValue>
                  <Cooldown>20</Cooldown>
                  <ScalingGroupId>asg-bp1ffogfdauy0jw0****</ScalingGroupId>
                  <ScalingRuleAri>ari:acs:ess:cn-hangzhou:140692647406****:scalingrule/asr-bp1dvirgwkoowxk7****</ScalingRuleAri>
                  <ScalingRuleId>asr-bp1dvirgwkoowxk7****</ScalingRuleId>                                                
                  <ScalingRuleName>scalingrule****</ScalingRuleName>
            </ScalingRule>
      </ScalingRules>
      <TotalCount>1</TotalCount>
      <RequestId>3306A40D-3412-4101-9F19-5F81E3055DAD</RequestId>
</DescribeScalingRulesResponse>
```

`JSON` format

```
{
    "RequestId": "B583BFEF-A779-427A-9B74-262DDD249702",
    "TotalCount": 1,
    "PageNumber": 1,
    "PageSize": 10,
    "ScalingRules": {
        "ScalingRule": [
            {
                "ScalingRuleId": "asr-bp1dvirgwkoowxk7****",
                "ScalingRuleAri": "ari:acs:ess:cn-hangzhou:140692647406****:scalingrule/asr-bp1dvirgwkoowxk7****",
                "Cooldown": 500,
                "ScalingGroupId": "asg-bp1ffogfdauy0jw0****",
                "AdjustmentType": "TotalCapacity",
                "ScalingRuleName": "scalingrule****",
                "AdjustmentValue": 5
            }
        ]
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

