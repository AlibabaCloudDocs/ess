# DetachDBInstances

You can call this operation to disassociate one or more ApsaraDB RDS instances from a scaling group.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DetachDBInstances&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DetachDBInstances|The operation that you want to perform. Set the value to DetachDBInstances. |
|DBInstance.N|RepeatList|Yes|rm-bp12cy3\*\*\*\*|The ID of ApsaraDB RDS instance N. You can disassociate up to five ApsaraDB RDS instances from a scaling group at a time. |
|ScalingGroupId|String|Yes|asg-bp1igpak5ft1flyp\*\*\*\*|The ID of the scaling group. |
|ForceDetach|Boolean|No|false|Specifies whether to remove the private IP addresses of ECS instances in the scaling group from the whitelist of the ApsaraDB RDS instance. Valid values:

-   true: removes the private IP addresses of the ECS instances.
-   false: does not remove the private IP addresses of the ECS instances.

Default value: false. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25965~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DetachDBInstances
&ScalingGroupId=asg-bp1igpak5ft1flyp****
&DBInstance.1=rm-bp12cy3****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DetachDBInstancesResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DetachDBInstancesResponse>
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

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist in the current account. |
|400

|InvalidDBInstanceId.NotFound

|DB instance "%s" does not exist.

|The error message returned because the specified ApsaraDB RDS instance does not exist. |

