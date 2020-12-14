# SetGroupDeletionProtection

You can call this operation to enable or disable deletion protection for a scaling group.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=SetGroupDeletionProtection&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SetGroupDeletionProtection|The operation that you want to perform. Set the value to SetGroupDeletionProtection. |
|GroupDeletionProtection|Boolean|Yes|true|Specifies whether to enable deletion protection for the scaling group. Valid values:

-   true: enables deletion protection. After the feature is enabled, you cannot delete the scaling group by using the console or by calling an API operation. If you want to delete the scaling group, you must disable deletion protection for the scaling group.
-   false: disables deletion protection.

Default value: false. |
|ScalingGroupId|String|Yes|asg-bp1igpak5ft1flyp\*\*\*\*|The ID of the scaling group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|CCC29E24-3AEC-4F2C-8A14-78B14FA738B7|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=SetGroupDeletionProtection
&ScalingGroupId=asg-bp1igpak5ft1flyp****
&GroupDeletionProtection=true
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SetGroupDeletionProtectionResponse>
    <RequestId>CCC29E24-3AEC-4F2C-8A14-78B14FA738B7</RequestId>
</SetGroupDeletionProtectionResponse>
```

`JSON` format

```
{
    "RequestId": "CCC29E24-3AEC-4F2C-8A14-78B14FA738B7"
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

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist. |
|400

|InvalidOperation.Conflict

|Specific operation may conflicts with other operations, please retry later.

|The error message returned because the operation conflicts with another operation in progress. Try again later. |

