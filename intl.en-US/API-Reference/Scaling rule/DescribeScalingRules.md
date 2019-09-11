# DescribeScalingRules {#doc_api_Ess_DescribeScalingRules .reference}

You can call this operation to query all scaling rules in a scaling group and list information about the scaling rules.

## Description {#description .section}

You can query all scaling rules in a scaling group by specifying the scaling group ID and filter rules to be returned by specifying the ID, name, unique identifier, and type of scaling rules.

## Debugging {#api_explorer .section}

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeScalingRules&type=RPC&version=2014-08-28)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|RegionId|String|Yes|cn-qingdao|The region ID of the scaling group to which a scaling rule belongs.

 |
|Action|String|No|DescribeScalingRules|The operation that you want to perform. Set the value to DescribeScalingRules.

 |
|PageNumber|Integer|No|1|The page number of the scaling rule list to return. Pages start from page 1.

 Default value: 1.

 |
|PageSize|Integer|No|50|The number of entries to return on each page. Maximum value: 50.

 Default value: 10.

 |
|ScalingGroupId|String|No|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|The ID of the scaling group.

 |
|ScalingRuleAri.1|String|No|ari:acs:ess:cn-qingdao:1344371:scalingRule/eMKWG8SRNb9dBLAjweNI1Ik|The unique identifier of scaling rule N to be queried. Valid values of N: 1 to 10.

 |
|ScalingRuleId.1|String|No|eMKWG8SRNb9dBLAjweN\*\*\*\*|The ID of scaling rule N to be queried. Valid values of N: 1 to 10.

 |
|ScalingRuleName.1|String|No|eMKWG8SRNb9dBLAjweN\*\*\*\*|The name of scaling rule N to be queried. Valid values of N: 1 to 10.

 |
|ScalingRuleType|String|No|SimpleScalingRule|The type of the scaling rule. Valid values:

 -   SimpleScalingRule: scales ECS instances based on the values of AdjustmentType and AdjustmentValue.
-   TargetTrackingScalingRule: dynamically calculates the number of ECS instances to be scaled and tries to keep the value of a predefined metric close to TargetValue.
-   StepScalingRule: scales ECS instances in steps based on specified thresholds and metric values.
-   PredictiveScalingRule: analyzes historical monitoring data of the scaling group and uses machine learning to predict the future values of metrics. This rule automatically creates scheduled tasks to set the boundary values for the scaling group.

 Default value: SimpleScalingRule.

 |
|ShowAlarmRules|Boolean|No|false|Specifies whether to return the CloudMonitor monitoring task associated with a scaling rule. Valid values:

 -   true: The CloudMonitor monitoring task associated with a scaling rule is returned.
-   false: The CloudMonitor monitoring task associated with a scaling rule is not returned.

 Default value: false.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The current page number.

 |
|PageSize|Integer|50|The number of entries returned on each page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request.

 |
|ScalingRules| | |The set of scaling rules.

 |
|AdjustmentType|String|QuantityChangeInCapacity|The method used by the scaling rule to adjust the number of instances. Valid values:

 -   QuantityChangeInCapacity: adds or removes a specified number of ECS instances.
-   PercentChangeInCapacity: adds or removes a specified proportion of ECS instances.
-   TotalCapacity: adds or removes ECS instances to ensure that the current scaling group has a specified number of ECS instances.

 |
|AdjustmentValue|Integer|1|The adjustment amount specified for the scaling rule.

 |
|Alarms| | |The CloudMonitor monitoring tasks associated with scaling rules. The CloudMonitor monitoring tasks associated with scaling rules are returned only when the ShowAlarmRules parameter is set to true. Otherwise, an empty list is returned.

 |
|AlarmTaskId|String|asg-bp18p2yfxow2dloq\*\*\*\*\_1f9458d1-70e1-4bee-8c7f-7a47695b\*\*\*\*|The ID of the monitoring task associated with a scaling rule.

 |
|AlarmTaskName|String|event-notified\*\*\*\*|The name of the monitoring task associated with a scaling rule.

 |
|ComparisonOperator|String|\>=|The comparison operator of the metric value and threshold for the monitoring task associated with a scaling rule. Valid values:

 -   <=: The metric value is smaller than or equal to the threshold.
-   <: The metric value is smaller than the threshold.
-   \>: The metric value is greater than the threshold.
-   \>=: The metric value is greater than or equal to the threshold.

 |
|Dimensions| | |The dimensions of the monitoring task associated with a scaling rule.

 |
|DimensionKey|String|scaling\_group|The key values of dimensions associated with a metric. Valid values:

 -   scaling\_group: the ID of the scaling group.
-   userId: the ID of the user account.

 |
|DimensionValue|String|asg-bp18p2yfxow2dloq\*\*\*\*|The attribute values of dimensions associated with a metric.

 |
|EvaluationCount|Integer|3|The consecutive number of times for which the monitoring task associated with a scaling rule meets the threshold expression to trigger an alert.

 |
|MetricName|String|CpuUtilization|The name of the metric of the monitoring task associated with a scaling rule.

 |
|Statistics|String|Average|The statistical method of the monitoring task associated with a scaling rule. Valid values:

 -   Average
-   Maximum
-   Minimum

 |
|Threshold|Float|50|The alert threshold for the monitoring task associated with a scaling rule.

 |
|Cooldown|Integer|20|The cooldown period of the scaling rule. This parameter is only applicable to simple scaling rules. Valid values: 0 to 86400. Unit: seconds.

 |
|DisableScaleIn|Boolean|true|Indicates whether scale-in is disabled. This parameter is only applicable to target tracking scaling rules. Valid values:

 -   true: Scale-in is disabled.
-   false: Scale-in is enabled.

 |
|EstimatedInstanceWarmup|Integer|300|The warmup period of an ECS instance.

 |
|InitialMaxSize|Integer|100|The maximum number of ECS instances in the scaling group. This parameter is used in combination with the PredictiveValueBehavior parameter.

 |
|MaxSize|Integer|2|The maximum number of ECS instances in the scaling group.

 |
|MetricName|String|CpuUtilization|The predefined metric that you specified to monitor. This parameter is applicable to target tracking scaling rules and predictive scaling rules.

 Valid values for target tracking scaling rules:

 -   CpuUtilization: the average CPU utilization
-   ClassicInternetRx: the average public network inbound traffic over the classic network
-   ClassicInternetTx: the average public network outbound traffic over the classic network
-   VpcInternetRx: the average public network inbound traffic over the VPC
-   VpcInternetTx: the average public network outbound traffic over the VPC
-   IntranetRx: the average inbound internal traffic
-   IntranetTx: the average outbound internal traffic

 Valid values for predictive scaling rules:

 -   CpuUtilization: the average CPU utilization
-   IntranetRx: the average inbound internal traffic
-   IntranetTx: the average outbound internal traffic

 |
|MinAdjustmentMagnitude|Integer|1|The minimum number of ECS instances scaled in a scaling rule. This parameter only takes effect when the scaling rule type is SimpleScalingRule or StepScalingRule and AdjustmentType is PercentChangeInCapacity.

 |
|MinSize|Integer|1|The minimum number of ECS instances in the scaling group.

 |
|PredictiveScalingMode|String|PredictAndScale|The mode of the predictive scaling rule. Valid values:

 -   PredictAndScale: produces forecasts and creates prediction tasks.
-   PredictOnly: produces forecasts but does not create prediction tasks.

 |
|PredictiveTaskBufferTime|Integer|30|The amount of buffer time ahead of the prediction task execution time. By default, all scheduled tasks that are automatically created for a predictive scaling rule are executed at the beginning of each hour. You can set a buffer time to execute prediction tasks ahead of schedule, so that resources can be prepared in advance. Valid values: 0 to 60. Unit: minutes.

 |
|PredictiveValueBehavior|String|MaxOverridePredictiveValue|The action taken on the predicted maximum value. Valid values:

 -   MaxOverridePredictiveValue: uses the initial maximum capacity as the maximum value for prediction tasks when the predicted value is greater than the initial maximum capacity.
-   PredictiveValueOverrideMax: uses the predicted value as the maximum value for prediction tasks when the predicted value is greater than the initial maximum capacity.
-   PredictiveValueOverrideMaxWithBuffer: increases the predicted value by a ratio which is specified by PredictiveValueBuffer. If the predicted value increased by this ratio is greater than the initial maximum capacity, the predicted value after increase is used as the maximum value for prediction tasks.

 |
|PredictiveValueBuffer|Integer|50|The ratio of the increment to the predicted value when PredictiveValueBehavior is set to PredictiveValueOverrideMaxWithBuffer. If the predicted value increased by this ratio is greater than the initial maximum capacity, the value after the increase is used for prediction tasks. Valid values: 0 to 100.

 |
|ScalingGroupId|String|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|The ID of the scaling group.

 |
|ScalingRuleAri|String|ari:acs:ess:cn-qingdao:1344371:scalingRule/eMKWG8SRNb9dBLAjweNI1Ik|The unique identifier of the scaling rule.

 |
|ScalingRuleId|String|eMKWG8SRNb9dBLAjweN\*\*\*\*|The ID of the scaling rule.

 |
|ScalingRuleName|String|eMKWG8SRNb9dBLAjweN\*\*\*\*|The name of the scaling rule.

 |
|ScalingRuleType|String|SimpleScalingRule|The type of the scaling rule. Valid values:

 -   SimpleScalingRule: scales ECS instances based on the values of AdjustmentType and AdjustmentValue.
-   TargetTrackingScalingRule: dynamically calculates the number of ECS instances to be scaled and tries to keep the value of a predefined metric close to TargetValue.
-   StepScalingRule: scales ECS instances in steps based on specified thresholds and metric values.
-   PredictiveScalingRule: analyzes historical monitoring data of the scaling group and uses machine learning to predict the future values of metrics. This rule automatically creates scheduled tasks to set the boundary values for the scaling group.

 |
|StepAdjustments| | |The step adjustments of the step scaling rule.

 |
|MetricIntervalLowerBound|Float|1.0|The lower limit value specified in a step adjustment. Valid values: -9.999999E18 to 9.999999E18.

 |
|MetricIntervalUpperBound|Float|5.0|The upper limit value specified in a step adjustment. Valid values: -9.999999E18 to 9.999999E18.

 |
|ScalingAdjustment|Integer|1|The specified number of ECS instances scaled in a step adjustment.

 |
|TargetValue|Float|0.125|The target value.

 |
|TotalCount|Integer|1|The total number of scaling rules.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DescribeScalingRules
&RegionId=cn-qingdao
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&PageSize=50
&<Common request parameters>

```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
<DescribeScalingRulesResponse>
      <PageNumber>1</PageNumber>
      <PageSize>50</PageSize>
      <ScalingRules>
            <ScalingRule>
                  <AdjustmentType>QuantityChangeInCapacity</AdjustmentType>
                  <AdjustmentValue>1</AdjustmentValue>
                  <Cooldown>20</Cooldown>
                  <ScalingGroupId>AG6CQdPU8OKdwLjgZcJ****</ScalingGroupId>
                  <ScalingRuleAri>ari:acs:ess:cn-qingdao:1344371:scalingRule/eMKWG8SRNb9dBLAjweN****</ScalingRuleAri>
                  <ScalingRuleId>eMKWG8SRNb9dBLAjweN****</ScalingRuleId>                                                
                  <ScalingRuleName>eMKWG8SRNb9dBLAjweN****</ScalingRuleName>
            </ScalingRule>
      </ScalingRules>
      <TotalCount>1</TotalCount>
      <RequestId>3306A40D-3412-4101-9F19-5F81E3055DAD</RequestId>
</DescribeScalingRulesResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":10,
	"RequestId":"B583BFEF-A779-427A-9B74-262DDD249702",
	"ScalingRules":{
		"ScalingRule":[
			{
				"ScalingRuleAri":"ari:acs:ess:cn-qingdao:1344371:scalingRule/efcqrZdjlookc0UkE3dA****",
				"AdjustmentType":"TotalCapacity",
				"ScalingGroupId":"ccMvs9dcZlE5c9CtrwbX****",
				"AdjustmentValue":5,
				"ScalingRuleName":"KFJoxG****",
				"Cooldown":500,
				"ScalingRuleId":"efcqrZdjlookc0UkE3dA****"
			}
		]
	}
}
```

## Error codes { .section}

