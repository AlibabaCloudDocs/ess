# ExitStandby

You can call this operation to change the state of ECS instances in a scaling group from Standby to Running.

## Description

If a scaling group is associated with Server Load Balancer \(SLB\) instances, the weight of ECS instances in the scaling group are set to the value defined in the scaling configuration when the state of the ECS instances are changed from Standby to Running.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=ExitStandby&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ExitStandby|The operation that you want to perform. Set the value to ExitStandby. |
|InstanceId.N|RepeatList|Yes|i-28wt4\*\*\*\*|The ID of ECS instance N. The value of this parameter can be a JSON array that consists of up to 20 instance IDs. Separate multiple instance IDs with commas \(,\). |
|ScalingGroupId|String|Yes|asg-bp1fo0dbtsbmqa9h\*\*\*\*|The ID of the scaling group. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25965~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=ExitStandby
&ScalingGroupId=asg-bp1fo0dbtsbmqa9h****
&InstanceId.1=i-28wt4****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ExitStandbyResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ExitStandbyResponse>
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
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned because the RAM user is not authorized to call this operation. Contact the Alibaba Cloud account for the authorization and try again. |
|404

|InvalidInstanceId.NotFound

|A required authorization for the specified action is not supplied.

|The error message returned because the specified ECS instance does not exist. |
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist in the current account. |

