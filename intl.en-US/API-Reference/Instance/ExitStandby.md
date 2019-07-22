# ExitStandby {#doc_api_1163345 .reference}

You can call this operation to take specified instances in a scaling group out of the standby state.

## Description {#description .section}

If a Server Load Balancer \(SLB\) instance is specified in the scaling group, the weight of an ECS instance attached to the SLB instance is set to the value defined in the scaling configuration.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=ExitStandby) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|InstanceId.N|RepeatList|Yes|i-28wt4\*\*\*\*|The IDs of ECS instances. The value can be a JSON array consisting of multiple instance IDs. You can specify up to 20 instance IDs. Separate multiple IDs by using commas \(,\).

 |
|ScalingGroupId|String|Yes|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|The ID of the scaling group.

 |
|Action|String|No|ExitStandby|The operation that you want to perform. Set the value to ExitStandby.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=ExitStandby
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&InstanceId. 1=i-28wt4****
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ExitStandbyResponse> 
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</ExitStandbyResponse>

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
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned when the RAM user does not have permission to call this operation. Contact the owner of the Alibaba Cloud account to grant permission to the RAM user before trying again.

|
|404

|InvalidInstanceId.NotFound

|A required authorization for the specified action is not supplied.

|The error message returned when the specified ECS instance does not exist.

|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned when the specified scaling group does not exist in the current account.

|

