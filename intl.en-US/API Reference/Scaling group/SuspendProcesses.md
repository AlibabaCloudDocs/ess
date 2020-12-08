# SuspendProcesses

You can call this operation to suspend specified processes in a scaling group.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=SuspendProcesses&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SuspendProcesses|The operation that you want to perform. Set the value to SuspendProcesses. |
|Process.N|RepeatList|Yes|ScaleIn|Activity type N that you want to suspend. Valid values of N: 1 to 100. Valid values:

-   ScaleIn: scale-in activity.
-   ScaleOut: scale-out activity.
-   HealthCheck: health check.
-   AlarmNotification: event-triggered task.
-   ScheduledAction: scheduled task.

You can suspend five types of scaling activities. If you specify more than five types, the duplicate types are automatically removed. |
|ScalingGroupId|String|Yes|asg-bp15oubotmrq11xe\*\*\*\*|The ID of the scaling group. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25965~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|3E2033F0-03B4-419D-BCE2-C2339DB51B30|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=SuspendProcesses
&ScalingGroupId=asg-bp15oubotmrq11xe****
&Process.1=ScaleIn
&Process.2=ScaleOut
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SuspendProcessesResponse>
    <RequestId>3E2033F0-03B4-419D-BCE2-C2339DB51B30</RequestId>
</SuspendProcessesResponse>
```

`JSON` format

```
{
    "RequestId": "3E2033F0-03B4-419D-BCE2-C2339DB51B30"
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

|InvalidParameter

|The specified value of parameter "%s" is not valid.

|The error message returned because a specified parameter is invalid. |

