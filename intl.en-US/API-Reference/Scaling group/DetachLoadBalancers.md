# DetachLoadBalancers {#doc_api_1163784 .reference}

You can call this operation to remove one or more SLB instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=DetachLoadBalancers) simplifies API usage. You can use OpenAPI Explorer to perform operations such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description |
|---------|----|--------|-------|------------|
|LoadBalancer.N|RepeatList|Yes|lb-2zeur05gfs\*\*\*\*|The IDs of SLB instances. Up to five SLB instances can be removed at a time.

 |
|ScalingGroupId|String|Yes|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|The ID of the scaling group.

 |
|Action|String|No|DetachLoadBalancers|The operation that you want to perform. Set the value to DetachLoadBalancers.

 |
|ForceDetach|Boolean|No|false|Indicates whether to remove instances in the current scaling group from the back-end servers of the SLB instance:

 -   true: Remove the instances.
-   false: Do not remove the instances.

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

http://ess.aliyuncs.com/?Action=DetachLoadBalancers
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&LoadBalancer. 1=lb-2zeur05gfs****
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DetachLoadBalancersResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E
</RequestId>
</DetachLoadBalancersResponse>

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
|404

|InvalidLoadBalancerId.NotFound

|The Load Balancer "%s" does not exist.

|The error message returned when the specified SLB instance does not exist in the scaling group.

|

