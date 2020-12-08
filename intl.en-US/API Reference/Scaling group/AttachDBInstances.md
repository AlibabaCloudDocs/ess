# AttachDBInstances

You can call this operation to associate one or more ApsaraDB RDS instances with a scaling group.

## Description

Before you associate an ApsaraDB RDS instance with a scaling group, make sure that the ApsaraDB RDS instance meets the following requirements:

-   The ApsaraDB RDS instance and the scaling group must be in the same account.
-   The ApsaraDB RDS instance must be unlocked. For more information about the lock policy, see [RDS usage instructions](~~41872~~).
-   The ApsaraDB RDS instance must be in the Running state.

After an ApsaraDB RDS instance is associated with the scaling group, the default whitelist of the ApsaraDB RDS instance can contain a maximum of 1,000 IP addresses. For more information about the whitelist of ApsaraDB RDS instances, see [Configure whitelists](~~43185~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=AttachDBInstances&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AttachDBInstances|The operation that you want to perform. Set the value to AttachDBInstances. |
|DBInstance.N|RepeatList|Yes|rm-bp12cy3\*\*\*\*|The ID of ApsaraDB RDS instance N. Valid values of N: 1 to 5. |
|ScalingGroupId|String|Yes|asg-bp1avr6ensitts3w\*\*\*\*|The ID of the scaling group. |
|ForceAttach|Boolean|No|false|Specifies whether to add the private IP addresses of all ECS instances in the specified scaling group to the whitelist of the ApsaraDB RDS instance. Valid values:

-   true: adds the private IP addresses to the whitelist.
-   false: does not add the private IP addresses to the whitelist.

Default value: false. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25965~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=AttachDBInstances
&ScalingGroupId=asg-bp1avr6ensitts3w****
&DBInstance.1=rm-bp12cy3****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<AttachDBInstancesResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</AttachDBInstancesResponse>
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

|QuotaExceeded.RDS

|"RDS" quota exceeded.

|The error message returned because the maximum number of ApsraDB RDS instances that can be associated with the scaling group has been reached. |
|400

|InvalidDBInstanceId.NotFound

|The specified value of parameter "%s" is not valid.

|The error message returned because the specified ApsaraDB RDS instance does not exist. |
|400

|IncorrectDBInstanceStatus

|The current status of DB instance "%s" does not support this action.

|The error message returned because the operation is not supported while the ApsraDB RDS instance is in the current state. |
|400

|QuotaExceeded.DBInstanceSecurityIP

|Security IP quota exceeded in DB instance "%s".

|The error message returned because the maximum number of IP addresses in the whitelist of the ApsraDB RDS instance has been reached. |
|400

|InvalidInstanceIds.PrivateIpNotFound

|Can not find all private ips of instances in specific scaling group.

|The error message returned because the private IP address of an ApsraDB RDS instance associated with the scaling group cannot be obtained. |

