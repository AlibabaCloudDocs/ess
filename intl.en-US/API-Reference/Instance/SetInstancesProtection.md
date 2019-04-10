# SetInstancesProtection {#concept_71517_zh .concept}

You can call this operation to enable or disable the protection for one or more ECS instances in a scaling group \(`SetInstancesProtection`\).

## Description {#section_jjh_5ml_lgb .section}

After the protection is enabled for an ECS instance:

-   The instance keeps running in the protected state until you disable the protection.
-   The changes in the number of instances in a scaling group and scale-in activities triggered by monitoring tasks will not remove protected ECS instances. You must manually [Remove an ECS instance](reseller.en-US/API-Reference/Trigger task/Remove an ECS instance.md#) to release the instance.
-   When an ECS instance is stopped or restarted, the health check status of the ECS instance is not updated.

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set the value to SetInstancesProtection.|
|ScalingGroupId|String|Yes|The ID of the scaling group.|
|InstanceId.N|String|Yes|The ID of the ECS instance. Valid values of `N`: 1 to 20.|
|ProtectedFromScaleIn|Boolean|Yes|Indicates whether the protection for an ECS instance is enabled. Active protection when scale-in activities occur prevents the ECS instance from being stopped or removed from a scaling group. Valid values:-   True
-   False

|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|RequestId|String|The request ID.|

## Examples { .section}

Sample requests

```
http://ess.aliyuncs.com/?Action=SetInstancesProtection
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ 
&InstanceId. 1=i-28wt48iaa
&InstanceId. 1=i-28wt48ibb
&ProtectedFromScaleIn=true
& <Common request parameters>
```

Successful response examples

`XML` format

```
<SetInstancesProtectionResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId> 
</SetInstancesProtectionResponse>
```

`JSON` format

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## Error codes { .section}

The following table lists the error codes that the `SetInstancesProtection` operation can return. For more information, see [Client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) and [Server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|HttpCode|Error code|Error message|Description|
|--------|:---------|:------------|:----------|
|400|IncorrectScalingGroupStatus|The current status of the specified scaling group does not support this action.|The error message returned when you have not [Enable a scaling group](reseller.en-US/API-Reference/Scaling group/Enable a scaling group.md#).|
|403|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|The error message returned when you are not authorized to use the `SetInstancesProtection` operation.|
|404|InvalidInstanceId.NotFound|Instance “XXX” does not exist.|The error message returned when the specified ECS instance does not exist.|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|The error message returned when the specified scaling group does not exist.|

