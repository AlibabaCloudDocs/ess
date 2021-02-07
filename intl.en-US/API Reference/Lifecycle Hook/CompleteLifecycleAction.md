# CompleteLifecycleAction

You can call this operation to terminate the wait state of a specified scaling activity before the corresponding lifecycle hook times out.

## Description

You can set the action following the wait state of a scaling activity to CONTINUE to complete the scaling activity or to ABANDON to terminate the scaling activity.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=CompleteLifecycleAction&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CompleteLifecycleAction|The operation that you want to perform. Set the value to CompleteLifecycleAction. |
|LifecycleActionToken|String|Yes|aaaa-bbbbb-cccc-ddddd|The token that indicates the wait state of a specific scaling activity. You can obtain this token by using a Message Service \(MNS\) queue or MNS topic specified for the lifecycle hook. |
|LifecycleHookId|String|Yes|ash-bp14g3ee6bt3sc98\*\*\*\*|The ID of the lifecycle hook. |
|LifecycleActionResult|String|No|CONTINUE|The action to be taken after the lifecycle hook times out. Valid values:

-   CONTINUE: Auto Scaling continues to respond to a scale-out event and adds ECS instances to the scaling group or respond to a scale-in event and removes ECS instances from the scaling group.
-   ABANDON: Auto Scaling terminates a scale-out event and releases the created ECS instances or continues to respond to a scale-in event and removes ECS instances from the scaling group.

Default value: CONTINUE.

If multiple lifecycle hooks exist in a scaling group and are triggered at the same time, the following results may occur:

-   When a lifecycle hook of the ABANDON type that applies to scale-in events times out, the subsequent lifecycle hooks are terminated in advance. ECS instances are removed from the scaling group.
-   When a lifecycle hook of the CONTINUE type that applies to scale-in events or a lifecycle hook that applies to scale-out events times out, the subsequent lifecycle hooks continue to put ECS instances into the wait state until the last lifecycle hook times out. The final action to take is determined by the type of the last lifecycle hook. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25965~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=CompleteLifecycleAction
&LifecycleHookId=ash-bp14g3ee6bt3sc98****
&LifecycleActionToken=aaaa-bbbbb-cccc-ddddd
&LifecycleActionResult=CONTINUE
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CompleteLifecycleActionResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</CompleteLifecycleActionResponse>
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
|400

|InvalidParamter

|The specified value of parameter is invalid.

|The error message returned because the specified parameter is invalid. |
|400

|LifecycleHookIdAndLifecycleActionToken.Invalid

|The specified lifecycleActionToken and lifecycleHookId you provided does not match any in process lifecycle action.

|The error message returned because the specified LifecycleActionToken parameter does not match the specified LifecycleHookId parameter. |

