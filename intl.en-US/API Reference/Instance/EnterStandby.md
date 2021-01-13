# EnterStandby

You can call this operation to put ECS instances in a scaling group into the Standby state.

## Description

-   If a scaling group is associated with Server Load Balancer \(SLB\) instances, the weight of the ECS instances in the scaling group that serve as the backend servers of the SLB instances is set to 0 when the ECS instances are put into the Standby state.
-   When an ECS instance is in the Standby state, you can manually remove the instance from the scaling group and release the instance.
-   During scale-in events that are triggered by changes in the number of ECS instances in a scaling group or by the event-triggered tasks, the ECS instances in the Standby state are not removed.
-   If an ECS instance in the Standby state is detected as unhealthy, such as in the Stopping or Restarting state, this health status is not updated and does not trigger a scale-in event to remove the ECS instance. The health status of the instance is updated only after the instance exits the Standby state.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=EnterStandby&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|EnterStandby|The operation that you want to perform. Set the value to EnterStandby. |
|InstanceId.N|RepeatList|Yes|i-28wt4\*\*\*\*|The ID of ECS instance N. |
|ScalingGroupId|String|Yes|asg-bp1fo0dbtsbmqa9h\*\*\*\*|The ID of the scaling group. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25965~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=EnterStandby
&ScalingGroupId=asg-bp1fo0dbtsbmqa9h****
&InstanceId.1=i-28wt4****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<EnterStandbyResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</EnterStandbyResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned because the RAM user is not authorized to call this operation. Contact the Alibaba Cloud account for the authorization and try again. |
|404

|InvalidInstanceId.NotFound

|Instance “XXX” does not exist.

|The error message returned because the specified ECS instance does not exist. |
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist. |

