# AttachDBInstances {#doc_api_1163790 .reference}

You can call this operation to add one or more RDS instances.

## Description {#description .section}

Due to limits, the following conditions must be met when you add an RDS instance to a scaling group:

-   The SLB instance and the scaling group must belong to the same account.
-   The RDS instance must be in the **Unlocked** state. For more information about the lock policy, see [RDS usage instructions](~~41872~~).
-   The SLB instance must be in the **Running** state.
-   After an RDS instance is added, the default group of the RDS IP whitelist can contain up to 1,000 IP addresses. For more information about the IP whitelist, see [Configure the whitelist](~~26198~~).

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=AttachDBInstances) simplifies API usage. You can use OpenAPI Explorer to perform operations such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description |
|---------|----|--------|-------|------------|
|DBInstance.N|RepeatList|Yes|rm-bp12cy3\*\*\*\*|The IDs of RDS instances. Up to five RDS instances can be added at a time.

 |
|ScalingGroupId|String|Yes|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|The ID of the scaling group.

 |
|Action|String|No|AttachDBInstances|The operation that you want to perform. Set the value to AttachDBInstances.

 |
|ForceAttach|Boolean|No|false|Indicates whether to add the private IP addresses of all instances in the current scaling group to the IP whitelist of the RDS instance:

 -   true: Add the private IP addresses to the IP whitelist.
-   false: Do not add the private IP addresses to the IP whitelist.

 Default value: false.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=AttachDBInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&DBInstance. 1=rm-bp12cy3****
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<AttachDBInstancesResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</AttachDBInstancesResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Ess)

|HTTP status code

|Error code

|Error message

|Description

|
|------------------|------------|---------------|-------------|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned when the specified scaling group does not exist in the current account.

|
|400

|QuotaExceeded.RDS

|"RDS" quota exceeded.

|The error message returned when the number of RDS instances in the scaling group exceeds the quota.

|
|400

|InvalidDBInstanceId.NotFound

|The specified value of parameter "%s" is not valid.

|The error message returned when the specified RDS instance does not exist.

|
|400

|IncorrectDBInstanceStatus

|The current status of DB instance "%s" does not support this action.

|The error message returned when the RDS instance is in a state that does not support the current operation.

|
|400

|QuotaExceeded.DBInstanceSecurityIP

|Security IP quota exceeded in DB instance "%s".

|The error message returned when the number of back-end IP addresses in the whitelist of the RDS instance exceeds the quota.

|
|400

|InvalidInstanceIds.PrivateIpNotFound

|Can not find all private ips of instances in specific scaling group.

|The error message returned when the private IP addresses of an RDS instance in the group cannot be obtained.

|

