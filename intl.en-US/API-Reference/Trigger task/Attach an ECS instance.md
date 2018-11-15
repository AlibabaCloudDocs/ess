# Attach an ECS instance {#concept_25954_zh .concept}

Attaches an ECS instance to a specified scaling group.

## Description {#section_odd_l1l_sfb .section}

-   Restrictions on the attached ECS instance:
    -   The attached ECS instance and the scaling group must be in the same region.
    -   The attached ECS instance must in the Running status.
    -   The attached ECS instance has not been attached to other scaling groups.
    -   The attached ECS instance supports Subscription and Pay-As-You-Go payment methods.
    -   If the VswitchID is specified for a scaling group, you cannot attach Classic ECS instances or ECS instances on other VPCs to the scaling group.
    -   If the VswitchID is not specified for the scaling group, ECS instances of the VPC type cannot be attached to the scaling group.
-   The interface can be called only when the scaling group is active.
-   The interface can be called only when the scaling group has no scaling activity in progress.
-   When the scaling group has no scaling activity in progress, the interface can be directly executed without cooldown.
-   Successfully calling this interface only means that the Auto Scaling service has accepted the call request, and the scaling activity can be executed, but does not necessarily mean that the scaling activity can be successfully executed. You can use the returned ScalingActivityId to check the status of the scaling activity.
-   The call attempt may fail when the total capacity of instances specified by this interface plus the instances of the scaling group is greater than MaxSize.
-   The manually attached ECS instance is not associated with the active scaling configurations of the scaling group.

## Request parameters {#section_wjq_m1l_sfb .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|Operation interface name, required parameter. Value: AttachInstances.|
|ScalingGroupId|String|Yes|Scaling group ID.|
|InstanceId.N|String|Yes|ECS instance ID. You can input up to 20 IDs.|

## Response parameter {#section_hnz_n1l_sfb .section}

|Name|Type|Description|
|:---|:---|:----------|
|ScalingActivityId|String|Scaling activity ID|

## Error codes {#section_pp4_p1l_sfb .section}

For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|Error message|Error code|Description|HTTP status code|
|:------------|:---------|:----------|:---------------|
|The specified scaling group does not exist in this account.|Invalidscalinggroupid. NotFound|The specified scaling group does not exist.|404|
|The user has not granted Open API authorization to Auto Scaling|API is not fully authorized to the Auto Scaling service.|A required authorization for the specified action is not supplied.|403|
|The specified scaling group is not active.|IncorrectScalingGroupStatus|The current status of the specified scaling group does not support this action.|400|
|The specified ECS instance does not exist in this account.|InvalidInstanceId.NotFound|Instance “XXX” does not exist.|404|
|The specified ECS instance and the scaling group are not in the same region.|InvalidInstanceId. RegionMismatch|Instance “XXX” and the specified scaling group are not in the same Region.|400|
|The specified ECS instance and the instance with valid scaling configurations do not match.|InvalidInstanceId.InstanceTypeMismatch|Instance “XXX” and existing active scaling configurations have different instance types.|400|
|The specified ECS instance is not in the Running status.|IncorrectInstanceStatus|The current status of instance “XXX” does not support this action.|400|
|The network types of the specified ECS instance and the scaling group do not match.|InvalidInstanceId. NetworkTypeMismatch|The network type of instance “XXX” does not support this action.|400|
|The specified scaling group and the attached ECS instance are not in the same VPC.|InvalidInstanceId.VPCMismatch|Instance “XXX” and the specified scaling group are not in the same VPC.|400|
|The specified ECS instance has been attached to another scaling group.|InvalidInstanceId.InUse|Instance “XXX” is already attached to another scaling group.|400|
|The specified scaling group has an in-progress scaling activity.|ScalingActivityInProgress|You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress for the specified scaling group.|400|
|The load balancing instance for the specified scaling group is not active|The Server Load Balancer instance of the specified scaling group is not in the Active status.|The current status of the specified Server Load Balancer does not support this action.|400|
|Health check is not enabled for the Server Load Balancer of the specified scaling group.|IncorrectLoadBalancerHealthCheck|The current health check type of specified load balancer does not support this action.|400|
|The network type of the ECS instance contained in the specified Server Load Balancer is different from the network type of the scaling group.|InvalidLoadBalancerId.IncorrectInstanceNetworkType|The network type of the instance in specified Server Load Balancer does not support this action.|400|
|The ECS instance contained in the specified Server Load Balancer and VSwitchId are not in the same VPC.|InvalidLoadBalancerId.VPCMismatch|The specified virtual switch and the instance in specified load balancer are not in the same VPC.|400|
|The RDS instance in the specified scaling group is not in the Running status.|IncorrectDBInstanceStatus|The current status of DB instance “XXX” does not support this action.|400|
|The number of IP addresses in the whitelist that can access the RDS instance in the scaling group has exceeded the upper limit.|QuotaExceeded.DBInstanceSecurityIP|Security IP quota exceeded in DB instance “XXX”.|400|
|The number of ECS instances attached to the specified security group exceeds the upper limit.|QuotaExceeded.SecurityGroupInstance|Instance quota exceeded in the specified security group.|400|
|Total Capacity after the ECS instance is attached is greater than MaxSize.|IncorrectCapacity.MaxSize|To attach the instances, the total capacity will be greater than the MaxSize.|400|

## Request example {#section_ah2_t1l_sfb .section}

```
http://ess.aliyuncs.com/?Action=AttachInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&InstanceId. 1=i-28wt48iaa
&<Public Request Parameters>
```

## Response example { .section}

XML format:

```
<AttachInstancesResponse>
    <ScalingActivityId>bybj9OcaOT4ucPMbFhcqHfA3</ScalingActivityId>
    <RequestId>DD0309B7-2613-4792-9B86-275906695253</RequestId>
</AttachInstancesResponse>
```

JSON format:

```
"RequestId": "6469DCD0-13AC-487E-85A0-CE4922908FDE",
"ScalingActivityId": "ebta5WbUzC8gcwUWvfchyT4U"
```

