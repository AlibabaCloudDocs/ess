# DeleteScheduledTask

You can call this operation to delete a scheduled task.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DeleteScheduledTask&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteScheduledTask|The operation that you want to perform. Set the value to DeleteScheduledTask. |
|ScheduledTaskId|String|Yes|edRtShc57WGXdt8TlPbr\*\*\*\*|The ID of the scheduled task. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DeleteScheduledTask
&ScheduledTaskId=edRtShc57WGXdt8TlPbr****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteScheduledTaskResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DeleteScheduledTaskResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HttpCode

|Error code

|Error message

|Description |
|----------|------------|---------------|-------------|
|404

|InvalidScheduledTaskId.NotFound

|The specified scheduled task does not exist.

|The error message returned because the specified scheduled task does not exist in this account. |

