# CompleteLifecycleAction

You can call this operation to terminate the wait state of a specified scaling activity before the corresponding lifecycle hook times out.

## Description

You can set the action following the wait state to CONTINUE to complete this scaling activity or to ABANDON to terminate this scaling activity.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=CompleteLifecycleAction&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CompleteLifecycleAction|The operation that you want to perform. Set the value to CompleteLifecycleAction. |
|LifecycleActionToken|String|Yes|aaaa-bbbbb-cccc-ddddd|The token that indicates a specific scaling activity. You can obtain this token by using an MNS queue or MNS topic specified for the lifecycle hook. |
|LifecycleHookId|String|Yes|ash-bp14g3ee6bt3sc98\*\*\*\*|The ID of the lifecycle hook. |
|LifecycleActionResult|String|No|CONTINUE|The action that the scaling group takes when the lifecycle hook times out. Valid values:

-   CONTINUE: The scaling group continues to respond to a scale-in or scale-out event.
-   ABANDON: The scaling group releases the created ECS instances if the scaling activity type is scale-out or removes the ECS instances to be scaled in if the scaling activity type is scale-in.

If a scaling group has multiple lifecycle hooks and one of them is terminated when the LifecycleActionResult parameter is set to ABANDON during a scale-in event, the remaining lifecycle hooks in the same scaling group are also terminated. Otherwise, the scaling activity will proceed normally after the lifecycle hook times out and continue with the action specified by the DefaultResult parameter.

Default value: CONTINUE. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25965~~). |

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

|The error message returned because the specified LifecycleActionToken parameter does not match any lifecycle hook IDs. |

