# CompleteLifecycleAction {#concept_73847_zh .concept}

If you finish before the timeout period ends, complete the lifecycle action \(`CompleteLifecycleAction`\).

You can set the action following the wait state to Continue to complete this scaling event \(`CONTINUE`\) or to Abandon to terminate this scaling event \(`ABANDON`\).

## Request parameters {#section_jqw_qsl_sfb .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: CompleteLifecycleAction|
|LifecycleHookId|String|Yes|The ID of the lifecycle hook|
|LifecycleActionToken|String|Yes|A token that indicates a specific lifecycle action associated with an instance. You can obtain this token using an MNS queue or MNS topic specified for the lifecycle hook.|
|LifecycleActionResult|String|No|The action that the scaling group takes when the lifecycle hook times out Value range:-   CONTINUE: the scaling group continues with the scale-in or scale-out process.
-   ABANDON: the scaling group stops any remaining action of the scale-in or scale-out event.

Default value: CONTINUE

If the scaling group has multiple lifecycle hooks and one of them is terminated by the `DefaultResult=ABANDON` parameter during a scale-in event \(`SCALE_IN`\), the remaining lifecycle hooks under the same scaling group will also be terminated. Otherwise, the action following the wait state is the next action, as specified in the parameter DefaultResult, after the last lifecycle event under the same scaling group.

|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|RequestId|String|The Request ID|

## Request example { .section}

```
http://ess.aliyuncs.com/?Action=CompleteLifecycleAction
&LifecycleHookId=ash-xxxxxxxxxxx
&LifecycleActionToken=aaaa-bbbbb-cccc-ddddd
&LifecycleActionResult=CONTINUE
&<Public request parameter>
```

## Response example { .section}

XML format:

```
<CompleteLifecycleActionResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</CompleteLifecycleActionResponse>
```

JSON format:

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## Error codes { .section}

Error codes that are specific to this interface are as follows. Error codes that are specific to this interface are as follows. For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|Error code|Error message|HTTP status code|Description|
|:---------|:------------|:---------------|:----------|
|InvalidParamter|The specified value of parameter is invalid.|400|The specified value of the parameter is invalid.|
|LifecycleHookIdAndLifecycleActionToken.Invalid|The specified lifecycleActionToken and lifecycleHookId you provided does not match any in process lifecycle action.|400|The specified `LifecycleActionToken` does not match any `LifecycleHookId`.|

