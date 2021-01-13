# SetInstancesProtection

You can call this operation to enable or disable protection for one or more ECS instances in a scaling group.

## Description

After an ECS instance is put into the Protected state, the following limits apply to the instance:

-   The instance remains in the Protected state until you remove the instance from the Protected state.
-   Even if a scale-in event is triggered for a scaling group due to a change in the number of ECS instances or due to an event-triggered task, Auto Scaling does not remove the ECS instances in the Protected state. You must remove the ECS instance from the Protected state before Auto Scaling can remove the ECS instance from the scaling group and release the instance. For information about how to remove an ECS instance from a scaling group, see [Remove an ECS instance from a scaling group](~~25955~~).
-   When the ECS instance is stopped or restarted, the health status of the instance remains unchanged.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=SetInstancesProtection&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SetInstancesProtection|The operation that you want to perform. Set the value to SetInstancesProtection. |
|InstanceId.N|RepeatList|Yes|i-28wt4\*\*\*\*|The ID of ECS instance N. Valid values of N: 1 to 20. |
|ProtectedFromScaleIn|Boolean|Yes|true|Specifies whether to enable protection for an ECS instance to prevent the ECS instance from being stopped or removed from the scaling group during scale-in events. Valid values:

-   true: enables protection for the ECS instance.
-   false: disables protection for the ECS instance. |
|ScalingGroupId|String|Yes|asg-bp18p2yfxow2dloq\*\*\*\*|The ID of the scaling group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=SetInstancesProtection
&ScalingGroupId=asg-bp18p2yfxow2dloq****
&InstanceId.1=i-28wt4****
&InstanceId.2=i-bp1j1****
&ProtectedFromScaleIn=true
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SetInstancesProtectionResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</SetInstancesProtectionResponse>
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
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|The error message returned because the scaling group is disabled. |
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned because you are not authorized to call the SetInstancesProtection operation. |
|404

|InvalidInstanceId.NotFound

|Instance “XXX” does not exist.

|The error message returned because the specified ECS instance does not exist. |
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist. |

