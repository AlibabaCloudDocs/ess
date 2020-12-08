# DetachLoadBalancers

You can call this operation to disassociate one or more Server Load Balancer \(SLB\) instances from a scaling group.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DetachLoadBalancers&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DetachLoadBalancers|The operation that you want to perform. Set the value to DetachLoadBalancers. |
|LoadBalancer.N|RepeatList|Yes|lb-2zeur05gfs\*\*\*\*|The ID of SLB instance N. You can disassociate up to five SLB instances from a scaling group at a time. |
|ScalingGroupId|String|Yes|asg-bp1ffogfdauy0jw0\*\*\*\*|The ID of the scaling group. |
|ForceDetach|Boolean|No|false|Specifies whether to remove ECS instances in the specified scaling group from the backend server groups of the SLB instance. Valid values:

-   true: removes the ECS instances.
-   false: does not remove the ECS instances.

Default value: false. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25965~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DetachLoadBalancers
&ScalingGroupId=asg-bp1ffogfdauy0jw0****
&LoadBalancer.1=lb-2zeur05gfs****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DetachLoadBalancersResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DetachLoadBalancersResponse>
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

|The error message returned because Auto Scaling is not authorized to call the specified operation. |
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist in the current account. |
|404

|InvalidLoadBalancerId.NotFound

|The Load Balancer "%s" does not exist.

|The error message returned because the specified SLB instance is not associated with the scaling group. |

