# RebalanceInstances {#concept_71516_zh .concept}

You can call this operation to rebalance the distribution of ECS instances in a scaling group that is specified with multiple zones \(`RebalanceInstances`\).

## Description {#section_ab3_mml_lgb .section}

You can achieve the rebalance of zones by creating new ECS instances to replace the previous ECS instances. Newly created ECS instances are started first before stopping previous ECS instances. The rebalance operation will not affect the performance and availability of your applications.

-   You can perform the rebalance operation for ECS instances in a scaling group that is specified with multiple zones only when you set `MultiAZPolic=Balance`.
-   You can only perform the rebalance operation when the instances in the scaling group are significantly imbalanced.
-   A single rebalance operation can replace up to 20 ECS instances.
-   You are temporarily allowed to exceed 10% of the total capacity of the scaling group. This occurs during a rebalance operation when the number of ECS instances is approaching or reaches the maximum number \(specified in `MaxSize`\) of a scaling group and the operation is still running. The minimum number is one ECS instance. Generally, the duration of a rebalance operation from the status of exceeding the maximum capacity of a scaling group to the normal status is approximately one to six minutes.

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set the value to RebalanceInstances.|
|ScalingGroupId|String|Yes|The ID of the scaling group.|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|RequestId|String|The request ID.|
|ScalingActivityId|String|The ID of the scaling activity.|

## Examples { .section}

Sample requests

```
http://ess.aliyuncs.com/?Action=RebalanceInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ 
& <Common request parameters>
```

Successful response examples

`XML` format

```
<RebalanceInstancesResponse> 
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
    <ScalingActivityId>asa-kjgffgdfadahghda</ScalingActivityId>
</RebalanceInstancesResponse> 
```

`JSON` format

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368",
    "ScalingActivityId": "asa-kjgffgdfadahghda"
}
```

## Error codes { .section}

The following table lists the error codes that the `RebalanceInstances` operation can return. For more information, see [Client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) and [Server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|HttpCode|Error code|Error message|Description|
|--------|:---------|:------------|:----------|
|400|IncorrectScalingGroupStatus|The current status of the specified scaling group does not support this action.|The error message returned when you have not [enabled a scaling group](reseller.en-US/API-Reference/Scaling group/Enable a scaling group.md#).|
|400|OperationDenied|This operation is denied because the specified scaling group does not support this action.|The error message returned when you have not set the `MultiAZPolic=Balance` policy in the specified scaling group or the great imbalance issue of the distribution of ECS instances does not occur.|
|403|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|The error message returned when you have not been authorized to use the `RebalanceInstances` operation.|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|The error message returned when the specified scaling group does not exist in this account.|

