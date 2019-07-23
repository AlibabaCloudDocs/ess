# DeleteLifecycleHook {#doc_api_Ess_DeleteLifecycleHook .reference}

You can call this operation to delete a lifecycle hook.

## Description {#description .section}

The wait state is terminated if the corresponding lifecycle hook is deleted. You can use either of the following methods to delete a lifecycle hook:

-   Specify the lifecycle hook ID \(`LifecycleHookId`\). This way, you do not need to specify the `ScalingGroupId` or `LifecycleHookName` parameter.
-   Specify the `ScalingGroupId` and `LifecycleHookName` parameters at the same time.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=DeleteLifecycleHook) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|No|DeleteLifecycleHook|The operation that you want to perform. Set the value to DeleteLifecycleHook.

 |
|LifecycleHookId|String|No|ash-\*\*\*\*|The ID of the lifecycle hook.

 |
|LifecycleHookName|String|No|hook\_name\_test|The name of the lifecycle hook.

 |
|ScalingGroupId|String|No|dP8VqSd9ENXPc0ciVmbc\*\*\*\*|The ID of the scaling group.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DeleteLifecycleHook
&LifecycleHookId=ash-****
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DeleteLifecycleHookResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</DeleteLifecycleHookResponse>

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

|InvalidLifecycleHookId.NotExist

|The specified lifecycleHookId does not exist.

|The error message returned when the specified lifecycle hook ID does not exist.

|
|400

|InvalidLifecycleHookName.NotExist

|The specified lifecycleHookName you provided does not exist.

|The error message returned when the specified lifecycle hook name does not exist.

|

