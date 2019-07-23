# RebalanceInstances {#doc_api_Ess_RebalanceInstances .reference}

You can call this operation to rebalance the distribution of ECS instances in a multi-zone scaling group.

## Description {#description .section}

When rebalancing, Auto Scaling starts new instances before terminating the old ones. This ensures that the performance and availability of your application is not compromised by rebalancing instances.

-   You can perform the rebalance operation for ECS instances in a multi-zone scaling group only when you set `MultiAZPolicy=Balance`.
-   You can perform the rebalance operation only when the instances in the scaling group are significantly imbalanced.
-   A single rebalance operation can redistribute up to 20 ECS instances.
-   The system can temporarily exceed the maximum capacity of a scaling group specified by `MaxSize` by a 10% margin. The minimum number of ECS instances in a scaling group is 1. You can exceed the maximum capacity for as long as it takes for the rebalance operation to complete, typically one to six minutes.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=RebalanceInstances) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|ScalingGroupId|String|Yes|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|The ID of the scaling group.

 |
|Action|String|No|RebalanceInstances|The operation that you want to perform. Set the value to RebalanceInstances.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |
|ScalingActivityId|String|asa-kjgffgdfadah\*\*\*\*|The ID of the scaling activity.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=RebalanceInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<RebalanceInstancesResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
  <ScalingActivityId>asa-kjgffgdfadah****</ScalingActivityId>
</RebalanceInstancesResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"ScalingActivityId":"asa-kjgffgdfadah****"
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
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|The error message returned when you have not enabled the specified scaling group.

|
|400

|OperationDenied

|This operation is denied because the specified scaling group does not support this action.

|The error message returned when the MultiAZPolicy parameter of the specified scaling group is not set to Balance, or when the distribution of ECS instances is not sufficiently imbalanced to perform this operation.

|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned when you are not authorized to use the RebalanceInstances operation.

|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned when the specified scaling group does not exist in the current account.

|

