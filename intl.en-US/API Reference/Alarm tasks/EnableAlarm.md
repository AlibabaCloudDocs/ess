# EnableAlarm

You can call this operation to enable an event-triggered task.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=EnableAlarm&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|EnableAlarm|The operation that you want to perform. Set the value to EnableAlarm. |
|AlarmTaskId|String|Yes|asg-bp1hvbnmkl10vll5\*\*\*\*\_f95ce797-dc2e-4bad-9618-14fee7d1\*\*\*\*|The ID of the event-triggered task. |
|RegionId|String|Yes|cn-qingdao|The region ID of the event-triggered task. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|688B18B8-FB1E-42EB-A1ED-7F55B090\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=EnableAlarm
&RegionId=cn-qingdao
&AlarmTaskId=asg-bp1hvbnmkl10vll5****_f95ce797-dc2e-4bad-9618-14fee7d1****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<EnableAlarmResponse>
    <RequestId>688B18B8-FB1E-42EB-A1ED-7F55B090****</RequestId>
</EnableAlarmResponse>
```

`JSON` format

```
{
	"RequestId": "688B18B8-FB1E-42EB-A1ED-7F55B090****"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

