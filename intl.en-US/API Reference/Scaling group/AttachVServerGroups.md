# AttachVServerGroups

You can call this operation to add one or more VServer groups of an SLB instance to a scaling group.

## Description

Before you add a VServer group to a scaling group, make sure that the following requirements are met:

-   The SLB instance and the scaling group must be in the same account.
-   The SLB instance and the scaling group must be in the same region.
-   The SLB instance must be in the Running state.
-   The SLB instance must be configured with at least one listener. Health check is enabled for the SLB instance.
-   The SLB instance and the scaling group must be in the same VPC if the network type of both of them is VPC.
-   If the network type of the scaling group is VPC, the network type of the SLB instance is classic network, and the VServer group contains VPC-type instances, the instance and the scaling group must be in the same VPC.
-   The VServer group to be added to the scaling group must be associated with the SLB instance.
-   The number of VServer groups cannot exceed the quota for VServer groups in the scaling group. For more information about the quota, see [Limits](~~25863~~).

You must set the following parameters to specify the VServer groups to be added:

-   VServerGroup.N.LoadBalancerId: the ID of the SLB instance
-   VServerGroup.N.VServerGroupAttribute.N.VServerGroupId: the ID of the VServer group
-   VServerGroup.N.VServerGroupAttribute.N.Port: the port number of the VServer group

If you use different ports to add a VServer group to a scaling group, Auto Scaling considers that multiple VServer groups are added to the scaling group. If multiple VServer groups with the same group ID and port number are specified in the request parameters, only the first VServer group is used. The other VServer groups are ignored.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=AttachVServerGroups&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AttachVServerGroups|The operation that you want to perform. Set the value to AttachVServerGroups. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the scaling group. Example: cn-hangzhou or cn-shanghai. For more information, see [Regions and zones](~~40654~~). |
|ScalingGroupId|String|Yes|asg-bp18p2yfxow2dloq\*\*\*\*|The ID of the scaling group. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25965~~). |
|VServerGroup.N.LoadBalancerId|String|No|lb-bp1u7etiogg38yvwz\*\*\*\*|The ID of SLB instance N with which the VServer group is associated. N specifies the number of the SLB instance. Valid values of N: 1 to 5. |
|VServerGroup.N.VServerGroupAttribute.N.VServerGroupId|String|No|rsp-bp1jp1rge\*\*\*\*|The ID of VServer group M. N specifies the number of the SLB instance. Valid values of N: 1 to 5.

M specifies the number of the VServer group that is associated with SLB instance N. Valid values of M: 1 to 5. |
|VServerGroup.N.VServerGroupAttribute.N.Port|Integer|No|22|The port number that is used by Auto Scaling to add the ECS instances to VServer group M. Valid values: 1 to 65535.

N specifies the number of the SLB instance. Valid values of N: 1 to 5.

M specifies the number of the VServer group that is associated with SLB instance N. Valid values of M: 1 to 5. |
|VServerGroup.N.VServerGroupAttribute.N.Weight|Integer|No|100|The weight set for the ECS instances that are added to VServer group M. Valid values: 0 to 100.

N specifies the number of the SLB instance. Valid values of N: 1 to 5.

M specifies the number of the VServer group that is associated with SLB instance N. Valid values of M: 1 to 5.

Default value: 50. |
|ForceAttach|Boolean|No|false|Specifies whether to add the ECS instances in the specified scaling group to the new VServer group.

-   true: adds the ECS instances to the VServer group.
-   false: does not add the ECS instances to the VServer group.

Default value: false. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=AttachVServerGroups
&ScalingGroupId=asg-****
&RegionId=cn-hangzhou
&VServerGroup.1.LoadBalancerId=lb-bp1u7etiogg38yvwz****
&VServerGroup.1.VServerGroupAttribute.1.VServerGroupId=rsp-bp1jp1rge****
&VServerGroup.1.VServerGroupAttribute.1.Port=22
&VServerGroup.1.VServerGroupAttribute.1.Weight=100
&<Common request parameters>
```

Sample success responses

`XML` format

```
<AttachVServerGroupsResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</AttachVServerGroupsResponse>
```

`JSON` format

```
{
    "requestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
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

|The load balancer "%s" does not exist.

|The error message returned because the specified SLB instance does not exist in the current account. |
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

|InvalidVServerGroupId.ForLoadBalancer

|Invalid VServerGroupId For LoadBalancer "%s".

|The error message returned because the VServer group that is specified by the VServerGroup.N.VServerGroupAttribute.N.VServerGroupId parameter does not belong to the specified SLB instance. |
|400

|QuotaExceeded.VServerGroup

|VServerGroup quota exceeded in the specified scaling group.

|The error message returned because the maximum number of VServer groups that can be added to the scaling group has been reached. |

