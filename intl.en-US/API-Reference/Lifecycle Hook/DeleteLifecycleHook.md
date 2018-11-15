# DeleteLifecycleHook {#concept_73841_zh .concept}

Delete a lifecycle hook \(`DeleteLifecycleHook`\).

The wait state will be terminated once the corresponding lifecycle hook is deleted. You can delete a lifecycle hook using either of the following methods:

-   Specify the parameter `LifecycleHookId`. `ScalingGroupId` and `LifecycleHookName` are ignored.
-   Specify the parameters `ScalingGroupId` and `LifecycleHookName`.

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: DeleteLifecycleHook.|
|LifecycleHookId|String|No|The ID of the lifecycle hook|
|ScalingGroupId|String|No|The ID of the scaling group|
|LifecycleHookName|String|No|The name of the lifecycle hook|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|RequestId|String|The request ID|

## Request example { .section}

```
Http://ess.aliyuncs.com /? Action = fig
&LifecycleHookId=ash-xxxxxxxxxxx
&<Public request parameter>
```

## Response example { .section}

XML format:

```
<DeleteLifecycleHookResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</DeleteLifecycleHookResponse>
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
|InvalidLifecycleHookId.NotExist|The specified lifecycleHookId does not exist.|400|The specified lifecycle hook ID does not exist.|
|InvalidLifecycleHookName.NotExist|The specified lifecycleHookName you provided does not exist.|400|The specified lifecycle hook name does not exist.|

