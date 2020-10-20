# DeleteScalingConfiguration

You can call this operation to delete a scaling configuration.

## Description

The scaling configuration cannot be deleted in one of the following conditions:

-   The scaling configuration in the scaling group is in the Active state.
-   The scaling group contains ECS instances that were created based on the scaling configuration.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer automatically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DeleteScalingConfiguration&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteScalingConfiguration|The operation that you want to perform. Set the value to DeleteScalingConfiguration. |
|ScalingConfigurationId|String|Yes|asc-bp1bx8mzur534edp\*\*\*\*|The ID of the scaling configuration to be deleted. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DeleteScalingConfiguration
&ScalingConfigurationId=asc-bp1bx8mzur534edp****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteScalingConfigurationResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DeleteScalingConfigurationResponse>
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

|InvalidScalingConfigurationId.NotFound

|The specified scaling configuration does not exist.

|The error message returned because the specified scaling configuration does not exist in the current account. |
|400

|IncorrectScalingConfigurationLifecycleState

|The current lifecycle state of specified scaling configuration does not support this action.

|The error message returned because the specified scaling configuration is not in the Inactive state. |
|400

|InstanceInUse

|You cannot delete a scaling configuration or scaling group while there is an instance associated with it.

|The error message returned because the scaling group contains ECS instances that were created based on the specified scaling configuration. |

