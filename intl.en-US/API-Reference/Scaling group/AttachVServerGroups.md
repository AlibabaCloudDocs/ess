# AttachVServerGroups {#doc_api_Ess_AttachVServerGroups .reference}

You can call this operation to add one or more VServer groups to an SLB instance.

## Description {#description .section}

Due to the [limits](~~32459~~) on SLB, the following conditions must be met when you add a VServer group to a scaling group:

-   The SLB instance and the scaling group must belong to the same account.
-   The SLB instance and the scaling group must be in the same region.
-   The SLB instance must be in the**Running**state.
-   The SLB instance must have at least one listener with health check enabled.
-   The SLB instance and the scaling group must be in the same VPC if both of them are of the VPC network type.
-   If the network type of the scaling group is VPC, the network type of the SLB instance is classic network, and the VServer group contains a VPC instance, the VPC instance and the scaling group must be in the same VPC.
-   The VServer group that you want to add to the scaling group must be associated with the SLB instance.
-   Currently, up to five VServer groups can be added to a scaling group.

    **Note:** A VServer group is uniquely identified by the combination of the SLB instance ID \(LoadBalancerId\),

    -   VServer group ID \(VServerGroupId\),
    -   and port number of the VServer group \(Port\). If you have added a VServer group to a scaling group by using different port numbers, Auto Scaling considers that multiple VServer groups are added to the scaling group. If multiple VServer groups that have the same group ID and port number are specified in the request parameters,
    -   only the first VServer group is used. The other VServer groups are ignored.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=AttachVServerGroups) simplifies API usage. You can use OpenAPI Explorer to perform operations such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the scaling group was created, such as cn-hangzhou or cn-shanghai. For more information, see [Regions and zones](~~40654~~).

 |
|ScalingGroupId|String|Yes|asg-\*\*\*\*| The ID of the scaling group.

 |
|Action|String|No|AttachVServerGroups| The operation that you want to perform. Set the value to AttachVServerGroups.

 |
|ForceAttach|Boolean|No|false| Indicates whether the ECS instances that belong to the scaling group are to be added to the newly attached VServer group.

 -   true: Add the ECS instances to the VServer group.
-   false: Do not add the ECS instances to the VServer group.

 Default value: false.

 |
|VServerGroup.N.LoadBalancerId|String|No|lb-\*\*\*\*| The ID of the SLB instance with which the VServer group is associated. N represents the SLB instance number. Valid values of N: 1 to 5.

 |
|VServerGroup.N.VServerGroupAttribute.N.Port|Integer|No|22| The port number used by Auto Scaling to add the ECS instances to the VServer group. Valid values: 1 to 65,535.

 N represents the SLB instance number. Valid values of N: 1 to 5. M represents the VServer group number that is associated with the SLB instance. Valid values of M: 1 to 5.

 |
|VServerGroup.N.VServerGroupAttribute.N.VServerGroupId|String|No|rsp-\*\*\*\*| The ID of the VServer group. N represents the SLB instance number. Valid values of N: 1 to 5. M represents the VServer group number that is associated with the SLB instance. Valid values of M: 1 to 5.

 |
|VServerGroup.N.VServerGroupAttribute.N.Weight|Integer|No|100| The weight set for the ECS instances that are added to the VServer group. Valid values: 0 to 100.

 Default value: 50.

 N represents the SLB instance number. Valid values of N: 1 to 5. M represents the VServer group number that is associated with the SLB instance. Valid values of M: 1 to 5.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=AttachVServerGroups
&ScalingGroupId=asg-****
&RegionId=cn-hangzhou 
&VServerGroup. 1.LoadBalancerId=lb-****
&VServerGroup. 1.VServerGroupAttribute. 1.VServerGroupId=rsp-****
&VServerGroup. 1.VServerGroupAttribute. 1.Port=22
&VServerGroup. 1.VServerGroupAttribute. 1.Weight=100
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<AttachVServerGroupsResponse> 
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</AttachVServerGroupsResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"requestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes {#section_1gv_bbp_14l .section}

[View error codes](https://error-center.aliyun.com/status/product/Ess)

| HTTP status code

 | Error code

 | Error message

 | Description

 |
|--------------------|--------------|-----------------|---------------|
| 403

 | Forbidden.Unauthorized

 | A required authorization for the specified action is not supplied.

 | The error message returned when Auto Scaling is not authorized to call the specified operation.

 |
| 404

 | InvalidScalingGroupId.NotFound

 | The specified scaling group does not exist.

 | The error message returned when the specified scaling group does not exist in the current account.

 |
| 404

 | InvalidLoadBalancerId.NotFound

 | The load balancer "%s" does not exist.

 | The error message returned when the specified SLB instance does not exist in the current account.

 |
| 400

 | InvalidLoadBalancerId.RegionMismatch

 | The load balancer "%s" and the specified scaling group are not in the same Region.

 | The error message returned when the SLB instance and the scaling group are not in the same region.

 |
| 400

 | IncorrectLoadBalancerStatus

 | The current status of the load balancer "%s" does not support this action.

 | The error message returned when the SLB instance is in a state that does not support the current operation.

 |
| 400

 | IncorrectLoadBalancerHealthCheck

 | The current health check type of the load balancer "%s" does not support this action.

 | The error message returned when health check is not enabled for the specified SLB instance.

 |
| 400

 | InvalidLoadBalancerId.VPCMismatch

 | The specified virtual switch and the instance in the load balancer "%s" are not in the same VPC.

 | The error message returned when the SLB instance and the scaling group are not in the same VPC.

 |
| 400

 | InvalidVServerGroupId.ForLoadBalancer

 | Invalid VServerGroupId For LoadBalancer "%s".

 | The error message returned when the VServer group that is specified by the VServerGroupId parameter is not associated with the specified SLB instance.

 |
| 400

 | QuotaExceeded.VServerGroup

 | VServerGroup quota exceeded in the specified scaling group.

 | The error message returned when the maximum number of VServer groups that can be attached to the scaling group has been reached.

 |

