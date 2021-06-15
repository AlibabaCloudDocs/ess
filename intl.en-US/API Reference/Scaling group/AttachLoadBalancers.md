# AttachLoadBalancers

Associates one or more Server Load Balancer \(SLB\) instances with a scaling group.

## Description

Before you associate an SLB instance with a scaling group, make sure that the following requirements are met:

-   The SLB instance and the scaling group must be in the same account.
-   The SLB instance and the scaling group must be in the same region.
-   The SLB instance must be in the Running state.
-   The SLB instance must be configured with at least one listener. Health check is enabled for the SLB instance.
-   The SLB instance and the scaling group must be in the same VPC if their network type is VPC.
-   If the network type of the scaling group is VPC, the network type of the SLB instance is classic network, and the SLB backend server contains VPC-type instances, the instance and the scaling group must be in the same VPC.
-   The number of SLB instances cannot exceed the quota for SLB instances that can be associated with the scaling group. For more information about the quota, see [Limits](~~25863~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=AttachLoadBalancers&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AttachLoadBalancers|The operation that you want to perform. Set the value to AttachLoadBalancers. |
|LoadBalancer.N|RepeatList|Yes|lb-2zeur05gfs\*\*\*\*|The ID of SLB instance N. Valid values of N: 1 to 5. |
|ScalingGroupId|String|Yes|asg-bp1avr6ensitts3w\*\*\*\*|The ID of the scaling group. |
|ForceAttach|Boolean|No|false|Specifies whether to add all instances in the specified scaling group as backend servers to the SLB instance. Valid values:

-   true: adds all instances.
-   false: does not add all instances.

Default value: false. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to guarantee the idempotence of the request. You can use the client to generate the value, but you must make sure that the value is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25965~~). |
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
https://ess.aliyuncs.com/?Action=AttachLoadBalancers
&ScalingGroupId=asg-bp1avr6ensitts3w****
&LoadBalancer.1=lb-2zeur05gfs****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<AttachLoadBalancersResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</AttachLoadBalancersResponse>
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

|The error message returned because the specified scaling group does not exist within the current account. |
|400

|QuotaExceeded.LoadBalancer

|LoadBalancer quota exceeded in the scaling group "%s".

|The error message returned because the maximum number of SLB instances associated with the scaling group has been reached. |
|404

|InvalidLoadBalancerId.NotFound

|The load balancer "%s" does not exist.

|The error message returned because the specified SLB instance does not exist. |
|400

|InvalidLoadBalancerId.RegionMismatch

|The load balancer "%s" and the specified scaling group are not in the same Region.

|The error message returned because the SLB instance and the scaling group are not in the same region. |
|400

|IncorrectLoadBalancerStatus

|The current status of the load balancer "%s" does not support this action.

|The error message returned because the operation is not supported while the SLB instance is in the current state. |
|400

|IncorrectLoadBalancerHealthCheck

|The current health check type of the load balancer "%s" does not support this action.

|The error message returned because health check is not enabled for the specified SLB instance. |
|400

|InvalidLoadBalancerId.VPCMismatch

|The specified virtual switch and the instance in the load balancer "%s" are not in the same VPC.

|The error message returned because the SLB instance and the scaling group are not in the same VPC. |
|400

|QuotaExceeded.BackendServer

|Backend server quota exceeded in the load balancer "%s".

|The error message returned because the maximum number of backend servers of the SLB instance has been reached. |
|404

|InvalidScalingConfigurationId.NotFound

|The specified scaling configuration does not exist.

|The error message returned because the specified scaling configuration that is enabled for the specified scaling group does not exist. |

