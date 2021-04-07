# DescribeScalingGroups

You can call this operation to query scaling groups.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeScalingGroups&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeScalingGroups|The operation that you want to perform. Set the value to DescribeScalingGroups. |
|RegionId|String|Yes|cn-qingdao|The region ID of the scaling group. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

 Default value: 1 |
|PageSize|Integer|No|10|The number of entries to return on each page. Maximum value: 50.

 Default value: 10 |
|ScalingGroupId.N|RepeatList|No|asg-bp14wlu85wrpchm0\*\*\*\*|The ID of scaling group N to be queried. Valid values of N: 1 to 20. The IDs of inactive scaling groups are not displayed in the query result, and no errors are returned. |
|ScalingGroupName.1|String|No|scalinggroup\*\*\*\*|The name of scaling group N to be queried. Valid values of N: 1 to 20. The names of inactive scaling groups are not displayed in the query result, and no errors are returned. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|ScalingGroups|Array of ScalingGroup| |Details about the scaling groups. |
|ScalingGroup| | | |
|ActiveCapacity|Integer|1|The number of ECS instances that have been added to the scaling group and are running normally. |
|ActiveScalingConfigurationId|String|asc-bp1et2qekq3ojr33\*\*\*\*|The ID of the active scaling configuration in the scaling group. |
|CompensateWithOnDemand|Boolean|true|Indicates whether to automatically create pay-as-you-go instances to meet the required number of ECS instances when the expected capacity of preemptible instances cannot be fulfilled due to reasons such as cost or insufficient resources. This parameter takes effect when the MultiAZPolicy parameter is set to COST\_OPTIMIZED. Valid values:

 -   true: Pay-as -you-go instances can be created.
-   false: Pay-as -you-go instances cannot be created. |
|CreationTime|String|2014-08-14T10:58Z|The time when the scaling group was created. |
|DBInstanceIds|List|rm-bp15556qzebg1\*\*\*\*|The IDs of the ApsaraDB RDS instances that are associated with the scaling group. |
|DefaultCooldown|Integer|60|The default cooldown time of the scaling group. Unit: seconds. During the cooldown time, Auto Scaling executes only scaling activities that are triggered by [Cloud Monitor](~~35170~~) event-triggered tasks. |
|DesiredCapacity|Integer|5|The expected number of ECS instances in the scaling group. Auto Scaling automatically keeps the ECS instances at this number. |
|GroupDeletionProtection|Boolean|true|Indicates whether deletion protection is enabled for the scaling group. Valid values:

 -   true: Deletion protection is enabled for the scaling group. You cannot delete the scaling group.
-   false: Deletion protection is disabled for the scaling group. |
|HealthCheckType|String|ECS|The health check mode of the scaling group. Valid values:

 -   NONE: The system performs no health check.
-   ECS: The system performs health checks on ECS instances in the scaling group. |
|LaunchTemplateId|String|lt-m5e3ofjr1zn1aw7\*\*\*\*|The ID of the launch template used by the scaling group. |
|LaunchTemplateOverrides|Array of LaunchTemplateOverride| |Details about the instance type of the extended configurations. |
|LaunchTemplateOverride| | | |
|InstanceType|String|ecs.c5.xlarge|The instance type. The specified instance type overrides the instance type in the launch template. |
|WeightedCapacity|Integer|4|The weight of the instance type. This parameter indicates the capacity of a single instance of this instance type in the scaling group. A greater weight indicates that a less number of instances of the specified instance type is required to meet the expected capacity. |
|LaunchTemplateVersion|String|Default|The version of the launch template used by the scaling group. |
|LifecycleState|String|Active|The lifecycle status of the scaling group. Valid values:

 -   Active: The scaling group is active. Active scaling groups can receive requests to execute scaling rules and trigger scaling activities.
-   Inactive: The scaling group is inactive. Inactive scaling groups cannot receive requests to execute scaling rules.
-   Deleting: The scaling group is being deleted. Scaling groups that are being deleted cannot receive requests to execute scaling rules and their parameters cannot be modified. |
|LoadBalancerIds|List|lb-bp19byhscefk3x0li\*\*\*\*|The IDs of the SLB instances that are associated with the scaling group. |
|MaxSize|Integer|2|The maximum number of ECS instances in the scaling group. |
|MinSize|Integer|1|The minimum number of ECS instances in the scaling group. |
|ModificationTime|String|2014-08-14T10:58Z|The time when the scaling group was modified. |
|MultiAZPolicy|String|PRIORITY|The ECS instance scaling policy for a multi-zone scaling group. Valid values:

 -   PRIORITY: ECS instances are scaled based on the VSwitchIds.N parameter. When an ECS instance cannot be created in the zone where the VSwitch with the highest priority resides, the system uses the VSwitch with the next highest priority to create the ECS instance.
-   COST\_OPTIMIZED: ECS instances are created based on the unit prices of vCPUs in ascending order. Preemptible instances are preferentially created when preemptible instance types are specified for the scaling configuration. You can set the CompensateWithOnDemand parameter to specify whether to automatically create pay-as-you-go instances when preemptible instances cannot be created due to insufficient resources.

**Note:** COST\_OPTIMIZED takes effect only when multiple instance types are specified or at least one preemptible instance type is specified.

-   BALANCE: ECS instances are evenly distributed in multiple zones specified in the scaling group. If ECS instances are unevenly distributed among the zones due to issues such as insufficient ECS resources, you can call the [RebalanceInstance](~~71516~~) operation to reallocate instances to make them evenly distributed. |
|OnDemandBaseCapacity|Integer|30|The minimum number of pay-as-you-go instances required in the scaling group. Valid values: 0 to 1000. When the number of pay-as-you-go instances is less than this value, Auto Scaling preferentially creates pay-as-you-go instances. |
|OnDemandPercentageAboveBaseCapacity|Integer|20|The percentage of pay-as-you-go instances to create when instances are added to the scaling group.This parameter takes effect when the number of instances reaches the OnDemandBaseCapacity value. Valid values: 0 to 100. |
|PendingCapacity|Integer|0|The number of ECS instances that are being added to the scaling group but are still being configured. |
|PendingWaitCapacity|Integer|1|The number of ECS instances that are in the pending state to be added in the scaling group. |
|ProtectedCapacity|Integer|1|The number of ECS instances that are in the protected state in the scaling group. |
|RegionId|String|cn-qingdao|The region ID of the scaling group. |
|RemovalPolicies|List|OldestScalingConfiguration|Details about policies for removing ECS instances from the scaling group. Valid values:

 -   OldestInstance: removes ECS instances that were created at the earliest point in time.
-   NewestInstance: removes ECS instances that were most recently created.
-   OldestScalingConfiguration: removes ECS instances that were created based on the earliest scaling configuration. |
|RemovingCapacity|Integer|0|The number of ECS instances that are being removed from the scaling group. |
|RemovingWaitCapacity|Integer|1|The number of ECS instances that are in the pending state to be removed from the scaling group. |
|ScalingGroupId|String|asg-bp14wlu85wrpchm0\*\*\*\*|The ID of the scaling group. |
|ScalingGroupName|String|dyrSuvBOtO1dEdIlIbp\*\*\*\*|The name of the scaling group. |
|ScalingPolicy|String|recycle|Indicates the reclaim mode of the scaling group. Valid values:

 -   recycle: The reclaim mode of the scaling group is set to Shutdown and Reclaim Mode.
-   release: The reclaim mode of the scaling group is set to Release Mode.

 For more information, see [RemoveInstances](~~25955~~). |
|SpotInstancePools|Integer|5|The number of available instance types. Auto Scaling creates preemptible instances of multiple instance types available at the lowest cost. Valid values: 0 to 10. |
|SpotInstanceRemedy|Boolean|true|Indicates whether to supplement preemptible instances when the specified capacity of preemptible instances is not fulfilled. When Auto Scaling receives a system message that a preemptible instance is to be reclaimed, Auto Scaling attempts to create a new instance to replace the instance to be reclaimed if this parameter is set to true. |
|StandbyCapacity|Integer|1|The number of instances that are in the standby state in the scaling group. |
|StoppedCapacity|Integer|1|The number of instances that are in the stopped state in the scaling group. |
|SuspendedProcesses|List|ScaleIn|The scaling activity that is suspended. If no scaling activity is suspended, the returned value is empty. Valid values:

 -   ScaleIn: removes instances.
-   ScaleOut: creates instances.
-   HealthCheck: performs health checks.
-   AlarmNotification: sends alert notifications.
-   ScheduledAction: triggers scheduled tasks. |
|TotalCapacity|Integer|1|The total weighted capacity of all ECS instances in the scaling group if the instance type weight is specified for the scaling group. If the instance type weight is not specified, this parameter indicates the total number of ECS instances in the scaling group. |
|TotalInstanceCount|Integer|1|The total number of ECS instances in the scaling group. |
|VServerGroups|Array of VServerGroup| |Details about backend server groups. |
|VServerGroup| | | |
|LoadBalancerId|String|147b46d767c-cn-qingdao-cm5\*\*\*\*|The ID of the SLB instance with which the backend server group is associated. |
|VServerGroupAttributes|Array of VServerGroupAttribute| |The attributes of the backend server group. |
|VServerGroupAttribute| | | |
|Port|Integer|22|The number of the port that is used by the SLB instance to provide external services. |
|VServerGroupId|String|rsp-bp12bjrny\*\*\*\*|The ID of the backend server group. |
|Weight|Integer|1|The weight of the backend server group. |
|VSwitchId|String|vsw-bp1whw2u46cn8zubm\*\*\*\*|The ID of the vSwitch that is associated with the scaling group. |
|VSwitchIds|List|vsw-bp1whw2u46cn8zubm\*\*\*\*|The IDs of the vSwitches that are associated with the scaling group. If you use the VSwitchIds parameter, the VSwitchId parameter is ignored. |
|VpcId|String|vpc-bp1vwnn14rqpyiczj\*\*\*\*|The ID of the VPC to which the scaling group belongs. |
|TotalCount|Integer|1|The total number of scaling groups. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DescribeScalingGroups
&RegionId=cn-qingdao
&PageSize=10
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeScalingGroupsResponse>
      <RequestId>68386699-8B9E-4D5B-BC4C-75A28F6C2A00</RequestId>
      <TotalCount>1</TotalCount>
      <PageSize>10</PageSize>
      <PageNumber>1</PageNumber>
      <ScalingGroups>
            <ScalingGroup>
                  <ScalingGroupId>asg-bp14wlu85wrpchm0****</ScalingGroupId>
                  <ScalingGroupName>scalinggroup****</ScalingGroupName>
                  <RegionId>cn-qingdao</RegionId>
                  <RemovingCapacity>0</RemovingCapacity>
                  <DefaultCooldown>300</DefaultCooldown>
                  <MinSize>1</MinSize>
                  <MaxSize>2</MaxSize>
                  <LifecycleState>Inactive</LifecycleState>
                  <TotalInstanceCount>0</TotalInstanceCount>
                  <ActiveScalingConfigurationId>asc-bp1et2qekq3ojr33****</ActiveScalingConfigurationId>
                  <LoadBalancerIds>
                        <LoadBalancerId>lb-bp19byhscefk3x0li****</LoadBalancerId>
                  </LoadBalancerIds>
                  <PendingCapacity>0</PendingCapacity>
                  <TotalCapacity>0</TotalCapacity>
                  <ActiveCapacity>0</ActiveCapacity>
                  <CreationTime>2014-08-14T10:58Z</CreationTime>
                  <DBInstanceIds>
                        <DBInstanceId>rm-bp15556qzebg1****</DBInstanceId>
                        <DBInstanceId>rm-bp52316qzhbg6****</DBInstanceId>
                  </DBInstanceIds>
                  <VSwitchId>vsw-bp1whw2u46cn8zubm****</VSwitchId>
                  <RemovalPolicies>
                        <RemovalPolicy>OldestScalingConfiguration</RemovalPolicy>
                        <RemovalPolicy>OldestInstance</RemovalPolicy>
                  </RemovalPolicies>
            </ScalingGroup>
      </ScalingGroups>
</DescribeScalingGroupsResponse>
```

`JSON` format

```
{
    "RequestId": "68386699-8B9E-4D5B-BC4C-75A28F6C2A00",
    "TotalCount": 1,
    "PageSize": 10,
    "PageNumber": 1,
    "ScalingGroups": {
        "ScalingGroup": [
            {
                "ScalingGroupId": "asg-bp14wlu85wrpchm0****",
                "ScalingGroupName": "scalinggroup****",
                "RegionId": "cn-qingdao",
                "RemovingCapacity": 0,
                "DefaultCooldown": 300,
                "MinSize": 1,
                "MaxSize": 2,
                "LifecycleState": "Inactive",
                "TotalInstanceCount": 0,
                "ActiveScalingConfigurationId": "asc-bp1et2qekq3ojr33****",
                "LoadBalancerIds": {
                    "LoadBalancerId": [
                        "lb-bp19byhscefk3x0li****"
                    ]
                },
                "PendingCapacity": 0,
                "TotalCapacity": 0,
                "ActiveCapacity": 0,
                "CreationTime": "2014-08-14T10:58Z",
                "DBInstanceIds": {
                    "DBInstanceId": [
                        "rm-bp15556qzebg1****",
                        "rm-bp52316qzhbg6****"
                    ]
                },
                "VSwitchId": "vsw-bp1whw2u46cn8zubm****",
                "RemovalPolicies": {
                    "RemovalPolicy": [
                        "OldestScalingConfiguration",
                        "OldestInstance"
                    ]
                }
            }
        ]
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

