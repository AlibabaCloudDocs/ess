# DetachLoadBalancers

Disassociates one or more Server Load Balancer \(SLB\) instances from a scaling group.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DetachLoadBalancers&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DetachLoadBalancers|The operation that you want to perform. Set the value to DetachLoadBalancers. |
|LoadBalancer.N|RepeatList|Yes|lb-2zeur05gfs\*\*\*\*|The ID of SLB instance N. You can disassociate up to five SLB instances from a scaling group at a time. |
|ScalingGroupId|String|Yes|asg-bp1ffogfdauy0jw0\*\*\*\*|The ID of the scaling group. |
|ForceDetach|Boolean|No|false|Specifies whether to remove Elastic Compute Service \(ECS\) instances in the specified scaling group from the backend server groups of the SLB instance. Valid values:

-   true: removes the ECS instances.
-   false: does not remove the ECS instances.

Default value: false. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to guarantee the idempotence of the request. You can use the client to generate the value, but you must make sure that the value is unique among different requests. The token can contain only ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25965~~). |
|Async|Boolean|No|false|Specifies whether to use asynchronous calls when you associate an SLB instance with the scaling group. Asynchronous calls ensure the transactional nature of operations, which means that all operations are successfully performed or the execution results do not take effect if some operations fail. We recommend that you use asynchronous calls.

Valid values:

-   true: asynchronous calls. The request returns the ID of the scaling activity.
-   false: synchronous calls.

Default value: false. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|ScalingActivityId|String|asa-bp140qd7mak8k63f\*\*\*\*|The ID of the scaling activity.

This parameter value is returned only when Async is set to true. You can call the [DescribeScalingActivities](~~25961~~) operation to query the IDs of returned scaling activities and view the execution status of the scaling activities. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DetachLoadBalancers
&ScalingGroupId=asg-bp1ffogfdauy0jw0****
&LoadBalancer.1=lb-2zeur05gfs****
&<Common request parameters>
```

Sample success response

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

|The error message returned when the specified scaling group does not exist within the current account. |
|404

|InvalidLoadBalancerId.NotFound

|The Load Balancer "%s" does not exist.

|The error message returned because the specified SLB instance is not associated with the scaling group. |

