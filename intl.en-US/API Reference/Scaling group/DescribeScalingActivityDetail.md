# DescribeScalingActivityDetail

You can call this operation to query detailed information about a scaling activity.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeScalingActivityDetail&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeScalingActivityDetail|The operation that you want to perform. Set the value to DescribeScalingActivityDetail. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Detail|String|new ECS instances \\"i-bp16t2cgmiiymeqv\*\*\*\*\\" are created.|The detailed information about the scaling activity. |
|ScalingActivityId|String|asa-bp1c9djwrgxjyk31\*\*\*\*|The ID of the scaling activity. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DescribeScalingActivityDetail
&ScalingActivityId=asa-bp1c9djwrgxjyk31****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeScalingActivityDetailResponse>
    <Detail>new ECS instances "i-bp16t2cgmiiymeqv****" are created.
</Detail>
    <ScalingActivityId>asa-bp1c9djwrgxjyk31****</ScalingActivityId>
</DescribeScalingActivityDetailResponse>
```

`JSON` format

```
{
    "Detail": "new ECS instances \"i-bp16t2cgmiiymeqv****\" are created.\n",
    "ScalingActivityId": "asa-bp1c9djwrgxjyk31****"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|400

|InvalidParameter

|The input parameter \\"ScalingActivityId\\" that is mandatory for processing this request is not supplied

|The error message returned because the ID of the scaling activity is not provided. |

