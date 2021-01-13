# SetInstanceHealth

You can call this operation to set the health status of the ECS instances in a scaling group.

## Description

Auto Scaling performs health checks on ECS instances in a scaling group and removes unhealthy ECS instances. If you want to reserve an ECS instance, you can switch the ECS instance to the Standby or Protected state. For more information, see [EnterStandby](~~69678~~) and [SetInstancesProtection](~~71517~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=SetInstanceHealth&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SetInstanceHealth|The operation that you want to perform. Set the value to SetInstanceHealth. |
|HealthStatus|String|Yes|Healthy|The health status of an ECS instance. Valid values:

-   Healthy
-   Unhealthy |
|InstanceId|String|Yes|i-bp1ap6bro51a7fsa\*\*\*\*|The ID of an ECS instance in a scaling group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|B755AE57-6093-43E4-938E-DEA422A9B10F|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=SetInstanceHealth
&HealthStatus=Unhealthy
&InstanceId=i-bp1ap6bro51a7fsa****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SetInstanceHealthResponse>
        <RequestId>B755AE57-6093-43E4-938E-DEA422A9B10F</RequestId>
</SetInstanceHealthResponse>
```

`JSON` format

```
{
    "RequestId": "B755AE57-6093-43E4-938E-DEA422A9B10F"
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

|InvalidInstanceId.NotFound

|Instance "%s" does not exist.

|The error message returned because the specified instance does not exist in the scaling group. |
|400

|InvalidParameter

|The specified value of parameter "%s" is not valid.

|The error message returned because a specified parameter is invalid. |

