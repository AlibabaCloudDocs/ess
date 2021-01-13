# RebalanceInstances

You can call this operation to rebalance the distribution of ECS instances in a multiple-zone scaling group.

## Description

To rebalance the distribution of ECS instances in a multiple-zone scaling group, Auto Scaling creates new ECS instances to replace existing ones. Auto Scaling starts new instances before it terminates the existing instances. This ensures that the performance and availability of your applications are not affected.

-   You can call this operation only when you set the MultiAZPolicy parameter of the multi-zone scaling group to BALANCE.
-   You can perform rebalancing only when the distribution of ECS instances in a scaling group is significantly imbalanced.
-   A maximum of 20 ECS instances can be replaced in one rebalancing activity.
-   If the number of ECS instances in the scaling group is about to reach or reaches the maximum number of instances specified by the MaxSize parameter during a rebalancing activity and you must continue with the rebalancing activity, Auto Scaling allows the number of ECS instances in the scaling group to temporarily exceed the value of MaxSize. The excess number of instances ranges from one to 10% of the value of MaxSize. The exceeding status lasts until the rebalancing activity ends, typically for 1 to 6 minutes.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=RebalanceInstances&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RebalanceInstances|The operation that you want to perform. Set the value to RebalanceInstances. |
|ScalingGroupId|String|Yes|asg-bp18p2yfxow2dloq\*\*\*\*|The ID of the scaling group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|ScalingActivityId|String|asa-kjgffgdfadah\*\*\*\*|The ID of the scaling activity. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=RebalanceInstances
&ScalingGroupId=asg-bp18p2yfxow2dloq****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RebalanceInstancesResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <ScalingActivityId>asa-kjgffgdfadah****</ScalingActivityId>
</RebalanceInstancesResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "ScalingActivityId": "asa-kjgffgdfadah****"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|The error message returned because the scaling group is disabled. |
|400

|OperationDenied

|This operation is denied because the specified scaling group does not support this action.

|The error message returned because the MultiAZPolicy parameter of the specified scaling group is not set to BALANCE, or because the distribution of ECS instances in the scaling group is not significantly imbalanced. |
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned because you are not authorized to call the RebalanceInstances operation. |
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist in the current account. |

