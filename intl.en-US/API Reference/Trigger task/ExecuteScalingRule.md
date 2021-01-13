# ExecuteScalingRule

You can call this operation to executes a scaling rule.

## Description

Before you call this operation, make sure that the following conditions are met:

-   The scaling group is in the Active state.
-   The scaling group does not have scaling activities in progress.

If no scaling activity is being executed in the scaling group, this operation can trigger scaling activities immediately without waiting for the cooldown time to expire.

If the call is successful, Auto Scaling has accepted the request. However, this does not mean that the scaling activity will succeed. You can determine the status of a scaling activity based on the return value of the ScalingActivityId parameter.

If the number of ECS instances to be added will leave the number of instances in the scaling group greater than MaxSize, Auto Scaling adds the proper number of ECS instances to maintain the number of ECS instances in the scaling group equal to the MaxSize value.

If the number of ECS instances to be removed will leave the number of instances in the scaling group less than MinSize, Auto Scaling removes the proper number of ECS instances to maintain the number of ECS instances in the scaling group equal to the MinSize value.

A limited number of ECS instances can be adjusted at a time. For more information, see the description about the AdjustmentValue parameter in [CreateScalingRule](~~25948~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=ExecuteScalingRule&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ExecuteScalingRule|The operation that you want to perform. Set the value to ExecuteScalingRule. |
|ScalingRuleAri|String|Yes|ari:acs:ess:cn-hangzhou:140692647406\*\*\*\*:scalingrule/asr-bp1dvirgwkoowxk7\*\*\*\*|The unique identifier of the scaling rule.

**Note:** You can call the ExecuteScalingRule operation to execute only simple scaling rules and step scaling rules. To execute a step scaling rule, you must specify both BreachThreshold and MetricValue. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25965~~). |
|BreachThreshold|Float|No|1.0|The threshold specified when the step scaling rule is executed. Valid values: -9.999999E18~9.999999E18. |
|MetricValue|Float|No|1.0|The metric value specified when the step scaling rule is executed. Valid values: -9.999999E18~9.999999E18. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|ScalingActivityId|String|asa-bp13o672yeautiil\*\*\*\*|The ID of the scaling activity. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=ExecuteScalingRule
&ScalingRuleAri=ari:acs:ess:cn-hangzhou:140692647406****:scalingrule/asr-bp1dvirgwkoowxk7****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ExecuteScalingRuleResponse>
      <ScalingActivityId>asa-bp13o672yeautiil****</ScalingActivityId>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3****</RequestId>
</ExecuteScalingRuleResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "ScalingActivityId": "asa-bp13o672yeautiil****"
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

|InvalidScalingRuleAri.NotFound

|The specified scaling rule Ari does not exist.

|The error message returned because the specified scaling rule does not exist in the current account. |
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned because Auto Scaling is not authorized to call the specified operation. |
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|The error message returned because the scaling group to which the specified scaling rule belongs is not in the Active state. |
|400

|ScalingActivityInProgress

|You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress for the specified scaling group.

|The error message returned because the scaling group to which the specified scaling rule belongs has a scaling activity in progress. |
|400

|InsufficientBalance

|Your account does not have enough balance.

|The error message returned because the balance in your account is insufficient. Add funds to your account and try again. |
|400

|QuotaExceed.Instance

|Living instance quota exceeded.

|The error message returned because the maximum number of ECS instances has been reached. |
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|The error message returned because the specified Server Load Balancer \(SLB\) instance associated with the scaling group to which the specified scaling rule belongs is not in the Active state. |
|400

|IncorrectLoadBalancerHealthCheck

|The current health check type of specified load balancer does not support this action.

|The error message returned because health check is not enabled for an SLB instance of the scaling group to which the specified scaling rule belongs. |
|400

|InvalidLoadBalancerId.IncorrectInstanceNetworkType

|The network type of the instance in specified load balancer does not support this action.

|The error message returned because the network type of the ECS instance associated with the specified SLB instance is different from that of the scaling group. |
|400

|InvalidLoadBalancerId.VPCMismatch

|The specified virtual switch and the instance in specified load balancer are not in the same VPC.

|The error message returned because the ECS instance associated with the specified SLB instance is not in the same VPC as the vSwitch specified by VSwitchID. |
|400

|IncorrectDBInstanceStatus

|The current status of DB instance “XXX” does not support this action.

|The error message returned because the specified ApsaraDB RDS instance of the scaling group to which the specified scaling rule belongs is not in the Running state. |
|400

|QuotaExceeded.DBInstanceSecurityIP

|Security IP quota exceeded in DB instance “XXX”.

|The error message returned because for the scaling group to which the specified scaling rule belongs, the maximum number of IP addresses in the whitelist of the associated ApsaraDB RDS instance has been reached. |
|400

|QuotaExceeded.SecurityGroupInstance

|Instance quota exceeded in the specified security group.

|The error message returned because the maximum number of ECS instances in the specified security group has been reached. |
|400

|IncorrectCapacity.NoChange

|To execute the specified scaling rule, the total capacity will not change.

|The error message returned because no changes to the number of instances in the scaling group are made after the scaling rule is executed. |
|400

|QuotaExceeded.ScalingInstance

|Scaling instance quota exceeded.

|The error message returned because the maximum number of ECS instances that can be scaled has been reached. |
|400

|QuotaExceeded.AfterpayInstance

|Living afterpay instance quota exceeded.

|The error message returned because the maximum number of pay-as-you-go ECS instances has been reached. |
|400

|ResourceNotAvailable.ECS

|The specified region or zone does not offer the specified disk or instance category.

|The error message returned because the specified type of ECS instance or disk cannot be created in the specified region. |
|400

|ScalingRule.InvalidScalingRuleType

|Specific scaling rule type: %s can not be executed.

|The error message returned because the specified type of scaling rule cannot be executed. |
|400

|InvalidStepAdjustments.NoStepFound

|No adjustment step found for a metric value of: %s.

|The error message returned because no matching adjustment steps are found for the specified metric. |
|400

|MissingParameter.MetricValue

|Metric value must be specified for StepScalingRule.

|The error message returned because no metric value is specified for the step scaling rule. |
|400

|MissingParameter.BreachThreshold

|Breach threshold must be specified for StepScalingRule.

|The error message returned because no threshold is specified for the step scaling rule. |
|400

|MetricValueBeyondPermitRange

|Specific parameter "%s" beyond permit range.

|The error message returned because the specified metric value is invalid. |
|400

|BreachThresholdBeyondPermitRange

|Specific parameter "%s" beyond permit range.

|The error message returned because the specified threshold is invalid. |

