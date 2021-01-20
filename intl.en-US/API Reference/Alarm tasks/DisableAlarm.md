# DisableAlarm

You can call this operation to disable an event-triggered task.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DisableAlarm&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DisableAlarm|The operation that you want to perform. Set the value to DisableAlarm. |
|AlarmTaskId|String|Yes|asg-bp1hvbnmkl10vll5\*\*\*\*\_f95ce797-dc2e-4bad-9618-14fee7d1\*\*\*\*|The ID of the event-triggered task. |
|RegionId|String|Yes|cn-qingdao|The region ID of the event-triggered task. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|086EFCD4-C76F-4DC6-9EE9-0D9B711E\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DisableAlarm
&RegionId=cn-qingdao
&AlarmTaskId=asg-bp1hvbnmkl10vll5****_f95ce797-dc2e-4bad-9618-14fee7d1****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DisableAlarmResponse>
    <RequestId>086EFCD4-C76F-4DC6-9EE9-0D9B711E****</RequestId>
</DisableAlarmResponse>
```

`JSON` format

```
{
	"RequestId": "086EFCD4-C76F-4DC6-9EE9-0D9B711E****"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

