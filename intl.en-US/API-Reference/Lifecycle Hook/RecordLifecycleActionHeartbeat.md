# RecordLifecycleActionHeartbeat {#concept_73846_zh .concept}

You can use the `RecordLifecycleActionHeartbeat` operation to extend the timeout by the length of time required to keep the instance in a wait state.

An ECS instance can be kept in the wait state for no longer than six hours. The length of time for each wait state can be extended up to 20 times.

## Request parameters {#section_lll_nrl_sfb .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: RecordLifecycleActionHeartbeat.|
|LifecycleHookId|String|Yes|The ID of the lifecycle hook|
|LifecycleActionToken|String|Yes|A token that indicates a specific lifecycle action associated with an instance. You can obtain this token using an MNS queue or MNS topic specified for the lifecycle hook.|
|HeartbeatTimeout|Integer|No|The time, in seconds, that can elapse before the lifecycle hook times out. If the lifecycle hook times out, the scaling group performs the default action \(DefaultResult\). The range is \[30, 21600\]. The default is 600 seconds.You can prevent the lifecycle hook from timing out by calling the RecordLifecycleActionHeartbeat API. You can also terminate the lifecycle action by calling the [CompleteLifecycleAction](reseller.en-US/API-Reference/Lifecycle Hook/CompleteLifecycleAction.md#) API.

|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|RequestId|String|The Request ID|

## Request example { .section}

```
http://ess.aliyuncs.com/?Action=RecordLifecycleActionHeartbeat
&LifecycleHookId=ash-xxxxxxxxxxx
&LifecycleActionToken=aaaa-bbbbb-cccc-ddddd
&LifecycleActionResult=CONTINUE
&<Public request parameter>
```

## Response example { .section}

XML format:

```
<RecordLifecycleActionHeartbeatResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</RecordLifecycleActionHeartbeatResponse>
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
|InvalidParamter|The specified value of parameter is not valid.|400|The specified value of the parameter is invalid.|
|LifecycleHookIdAndLifecycleActionToken.Invalid|The specified lifecycleActionToken and lifecycleHookId you provided does not match any in process lifecycle action.|400|The specified `LifecycleActionToken` does not match any `LifecycleHookId`.|
|LifecycleAction.TimeExceeded|The specified parameter heartbeatTime exceed lifecycleAction max suspend time.|400|An ECS instance can be kept in the wait state for no longer than six hours.|
|LifecycleAction.RecordTimesExceeded|The specified lifecycleAction exceed lifecycleAction max record times.|400|The length of time for each wait state can be extended up to 20 times.|

