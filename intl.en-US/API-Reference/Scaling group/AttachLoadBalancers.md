# AttachLoadBalancers {#doc_api_1163783 .reference}

You can call this operation to add one or more SLB instances.

## Description {#description .section}

Due to [limits](~~32459~~), the following conditions must be met when you add an SLB instance to a scaling group:

-   The SLB instance and the scaling group must be in the same account.
-   The SLB instance and the scaling group must be in the same region.
-   The SLB instance must be in the Running state.
-   The SLB instance must have at least one listener with health check enabled.
-   The SLB instance and the scaling group must be in the same VPC if the network type of both of them is VPC.
-   If the network type of the scaling group is VPC, the network type of the SLB instance is classic network, and the SLB back-end server contains a VPC instance, the VPC instance and the scaling group must be in the same VPC.
-   The number of added SLB instances must be less than the quota of instances in the scaling group.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=AttachLoadBalancers) simplifies API usage. You can use OpenAPI Explorer to perform operations such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|LoadBalancer.N|RepeatList|Yes|lb-2zeur05gfs\*\*\*\*|The IDs of SLB instances. Up to five SLB instances can be added at a time.

 |
|ScalingGroupId|String|Yes|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|The ID of the scaling group.

 |
|Action|String|No|AttachLoadBalancers|The operation that you want to perform. Set the value to AttachLoadBalancers.

 |
|ForceAttach|Boolean|No|false|Indicates whether to add all instances in the current scaling group to the SLB back-end server:

 -   true: Add all instances to the back-end server.
-   false: Do not add any instance to the back-end server.

 Default value: false.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description |
|---------|----|-------|------------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=AttachLoadBalancers
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&LoadBalancer. 1=lb-2zeur05gfs****
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<AttachLoadBalancersResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</AttachLoadBalancersResponse>

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

|The error message returned when Auto Scaling is not authorized to call the specified operation.

|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned when the specified scaling group does not exist in the current account.

|
|400

|QuotaExceeded.LoadBalancer

|LoadBalancer quota exceeded in the scaling group "%s".

|The error message returned when the number of SLB instances in the scaling group exceeds the quota.

|
|404

|InvalidLoadBalancerId.NotFound

|The load balancer "%s" does not exist.

|The error message returned when the specified SLB instance does not exist.

|
|400

|InvalidLoadBalancerId.RegionMismatch

|The load balancer "%s" and the specified scaling group are not in the same Region.

|The error message returned when the SLB instance and the scaling group are not in the same region.

|
|400

|IncorrectLoadBalancerStatus

|The current status of the load balancer "%s" does not support this action.

|The error message returned when the SLB instance is in a state that does not support the current operation.

|
|400

|IncorrectLoadBalancerHealthCheck

|The current health check type of the load balancer "%s" does not support this action.

|The error message returned when health check is not enabled for the specified SLB instance.

|
|400

|InvalidLoadBalancerId.VPCMismatch

|The specified virtual switch and the instance in the load balancer "%s" are not in the same VPC.

|The error message returned when the SLB instance and the scaling group are not in the same VPC.

|
|400

|QuotaExceeded.BackendServer

|Backend server quota exceeded in the load balancer "%s".

|The error message returned when the number of back-end servers of the SLB instance exceeds the quota.

|
|404

|InvalidScalingConfigurationId.NotFound

|The specified scaling configuration does not exist.

|The error message returned when the specified scaling configuration that is enabled for the current scaling group does not exist.

|

