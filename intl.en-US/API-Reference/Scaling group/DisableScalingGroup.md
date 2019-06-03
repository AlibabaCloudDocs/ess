# DisableScalingGroup {#doc_api_1163778 .reference}

You can call this operation to disable a scaling group.

## Description {#description .section}

This operation disables a specified scaling group.

-   Scaling activities that are currently being executed by the specified scaling group before this operation is called will continue until they are completed. Scaling activity requests that are made to the target scaling group after this operation has been called will be rejected.
-   When you call this operation, note that the scaling group must be **active**.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=DisableScalingGroup) simplifies API usage. You can use OpenAPI Explorer to perform operations such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|ScalingGroupId|String|Yes|dmIDKNcyWfzncX9MWX1\*\*\*\*|The ID of the scaling group.

 |
|Action|String|No|DisableScalingGroup|The operation that you want to perform. Set the value to DisableScalingGroup.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description |
|---------|----|-------|------------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DisableScalingGroup
&ScalingGroupId=dmIDKNcyWfzncX9MWX1****
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DisableScalingGroupResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</DisableScalingGroupResponse>

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
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned when the specified scaling group does not exist in the current account.

|

