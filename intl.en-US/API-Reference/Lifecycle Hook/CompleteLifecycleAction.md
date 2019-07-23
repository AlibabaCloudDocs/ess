# CompleteLifecycleAction {#doc_api_Ess_CompleteLifecycleAction .reference}

You can call this operation to terminate the wait state of a specified scaling activity before the corresponding lifecycle hook times out.

After the wait state is terminated, you can have the current scaling activity continue or \(`CONTINUE`\) roll back this scaling activity \(`ABANDON`\).

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=CompleteLifecycleAction) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|LifecycleActionToken|String|Yes|aaaa-bbbbb-cccc-ddddd|The token that indicates a specific scaling activity associated with an instance. You can obtain this token from an MNS queue or MNS topic specified for the lifecycle hook.

 |
|LifecycleHookId|String|Yes|ash-\*\*\*\*|The ID of the lifecycle hook.

 |
|Action|String|No|CompleteLifecycleAction|The operation that you want to perform. Set the value to CompleteLifecycleAction.

 |
|LifecycleActionResult|String|No|CONTINUE|The action that the scaling group takes when the wait state terminates. Valid values:

 -   CONTINUE: The scaling group continues with the scale-in or scale-out process.
-   ABANDON: The scaling group stops the ongoing scale-in or scale-out event.

 Default value: CONTINUE

 If the scaling group has multiple lifecycle hooks and one of them is terminated by the `SCALE_IN`parameter during a scale-in event \(`DefaultResult=ABANDON`\), the wait states triggered by remaining lifecycle hooks in the same scaling group are also terminated. Otherwise, the action following the wait state is the next action, as specified in the DefaultResult parameter, after the last lifecycle event in the same scaling group.

 |
|OwnerAccount|String|No|ECSforCloud@Alibaba.com|The logon name of a RAM user.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=CompleteLifecycleAction
&LifecycleHookId=ash-****
&LifecycleActionToken=aaaa-bbbbb-cccc-ddddd
&LifecycleActionResult=CONTINUE
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CompleteLifecycleActionResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</CompleteLifecycleActionResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
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

|InvalidParamter

|The specified value of parameter is invalid.

|The error message returned when the value of the parameter is invalid.

|
|400

|LifecycleHookIdAndLifecycleActionToken.Invalid

|The specified lifecycleActionToken and lifecycleHookId you provided does not match any in process lifecycle action.

|The error message returned when the specified lifecycle action token does not match the lifecycle hook ID.

|

