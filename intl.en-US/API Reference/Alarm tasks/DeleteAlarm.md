# DeleteAlarm

You can call this operation to delete an event-triggered task.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DeleteAlarm&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteAlarm|The operation that you want to perform. Set the value to DeleteAlarm. |
|AlarmTaskId|String|Yes|asg-bp1hvbnmkl10vll5\*\*\*\*\_f95ce797-dc2e-4bad-9618-14fee7d1\*\*\*\*|The ID of the event-triggered task. |
|RegionId|String|Yes|cn-qingdao|The region ID of the event-triggered task. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AlarmTaskId|String|asg-bp1hvbnmkl10vll5\*\*\*\*\_f95ce797-dc2e-4bad-9618-14fee7d1\*\*\*\*|The ID of the event-triggered task. |
|RequestId|String|6EF9BFEE-FE07-4627-B8FB-14326FB9\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DeleteAlarm
&RegionId=cn-qingdao
&AlarmTaskId=asg-bp1hvbnmkl10vll5****_f95ce797-dc2e-4bad-9618-14fee7d1****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteAlarmResponse>
    <AlarmTaskId>asg-bp1hvbnmkl10vll5****_f95ce797-dc2e-4bad-9618-14fee7d1****</AlarmTaskId>
    <RequestId>6EF9BFEE-FE07-4627-B8FB-14326FB9****</RequestId>
</DeleteAlarmResponse>
```

`JSON` format

```
{
	"AlarmTaskId": "asg-bp1hvbnmkl10vll5****_f95ce797-dc2e-4bad-9618-14fee7d1****",
	"RequestId": "6EF9BFEE-FE07-4627-B8FB-14326FB9****"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

