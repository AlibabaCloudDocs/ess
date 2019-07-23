# SetInstancesProtection {#doc_api_Ess_SetInstancesProtection .reference}

You can call this operation to enable or disable protection for one or more ECS instances in a scaling group.

## Description {#description .section}

After protection is enabled for an ECS instance:

-   The instance keeps running in the protected state until you disable the protection.
-   The changes in the number of instances in a scaling group and scale-in activities triggered by monitoring tasks will not remove protected ECS instances. You must manually [remove an ECS instance](~~25955~~) to release the instance.
-   When an ECS instance is stopped or restarted, its health check status is not updated.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=SetInstancesProtection) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|InstanceId.N|RepeatList|Yes|i-28wt4\*\*\*\*|The IDs of ECS instances. Valid values of N: 1 to 20.

 |
|ProtectedFromScaleIn|Boolean|Yes|true|Indicates whether protection is enabled for an ECS instance. Active protection prevents the ECS instance from being stopped or removed from a scaling group during scale-in activities. Valid values:

 -   true
-   false

 |
|ScalingGroupId|String|Yes|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|The ID of the scaling group.

 |
|Action|String|No|SetInstancesProtection|The operation that you want to perform. Set the value to SetInstancesProtection.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description |
|---------|----|-------|------------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=SetInstancesProtection
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&InstanceId. 1=i-28wt4****
&InstanceId. 2=i-28wt4****
&ProtectedFromScaleIn=true
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<SetInstancesProtectionResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</SetInstancesProtectionResponse>

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
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|The error message returned when you have not enabled the specified scaling group.

|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned when you are not authorized to use the SetInstancesProtection operation.

|
|404

|InvalidInstanceId.NotFound

|Instance "XXX" does not exist.

|The error message returned when the specified ECS instance does not exist.

|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned when the specified scaling group does not exist.

|

