# DeleteScalingRule

You can call this operation to delete a scaling rule.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DeleteScalingRule&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteScalingRule|The operation that you want to perform. Set the value to DeleteScalingRule. |
|ScalingRuleId|String|Yes|asr-bp163l21e07uhnyt\*\*\*\*|The ID of the scaling rule to be deleted. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DeleteScalingRule
&ScalingRuleId=asr-bp163l21e07uhnyt****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteScalingRuleResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DeleteScalingRuleResponse>
```

`JSON` format

```
{
  "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|404

|InvalidScalingRuleId.NotFound

|The specified scaling rule does not exist.

|The error message returned because the specified scaling rule does not exist in the current account. |

