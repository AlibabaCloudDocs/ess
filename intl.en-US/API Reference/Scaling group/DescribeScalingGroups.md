# DescribeScalingGroups

You can call this operation to query scaling groups.

****

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
|ScalingGroupId.1|String|No|asg-bp14wlu85wrpchm0\*\*\*\*|The ID of scaling group N to be queried. Valid values of N: 1 to 20. The IDs of inactive scaling groups will not be displayed in the query result and no errors will be returned. |
|ScalingGroupName.1|String|No|scalinggroup\*\*\*\*|The name of scaling group N to be queried. Valid values of N: 1 to 20. The names of inactive scaling groups will not be displayed in the query result and no errors will be returned. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|ScalingGroups|Array of ScalingGroup| |Details about the scaling groups. |
|ScalingGroup| | | |
|ActiveCapacity|Integer|1|The number of ECS instances that have been added to the scaling group and are running properly. |
|ActiveScalingConfigurationId|String|asc-bp1et2qekq3ojr33\*\*\*\*|The ID of the active scaling configuration in the scaling group. |
|CompensateWithOnDemand|Boolean|true|Specifies whether to automatically create pay-as-you-go instances to meet the requirement for the number of ECS instances in the scaling group when the number of preemptible instances cannot be reached due to reasons such as cost or insufficient resources. This parameter takes effect when the MultiAZPolicy parameter is set to COST\_OPTIMIZED. Valid values:

-   true: Pay-as -you-go instances can be created.
-   false: Pay-as -you-go instances cannot be created. |
|CreationTime|String|2014-08-14T10:58Z|The time when the scaling group was created. |
|DBInstanceIds|List|rm-bp15556qzebg1\*\*\*\*|The IDs of the ApsaraDB RDS instances that are associated with the scaling group. |
|DefaultCooldown|Integer|60|The default cooldown period of the scaling group. Unit: seconds. During the cooldown period, Auto Scaling executes only scaling activities that are triggered by [Cloud Monitor](~~35170~~) event-triggered tasks. |
|DesiredCapacity|Integer|5|The expected number of ECS instances in the scaling group. Auto Scaling automatically keeps the ECS instances at this number. |
|GroupDeletionProtection|Boolean|true|Indicates whether scaling group deletion protection is enabled. Valid values:

-   true: Scaling group deletion protection is enabled. You cannot delete the scaling group.
-   false: Scaling group deletion protection is disabled. |
|HealthCheckType|String|ECS|The health check mode of the scaling group. Valid values:

-   NONE: The system performs no health check.
-   ECS: The system performs a health check on ECS instances in the scaling group. |
|LaunchTemplateId|String|lt-m5e3ofjr1zn1aw7\*\*\*\*|The ID of the launch template used by the scaling group. |
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

-   BALANCE: ECS instances are distributed evenly in multiple zones specified in the scaling group. If ECS instances are unevenly distributed among the zones due to certain issues such as insufficient ECS resources, you can reallocate instances to make them evenly distributed by calling the [RebalanceInstance](~~71516~~) operation. |
|OnDemandBaseCapacity|Integer|30|The minimum number of pay-as-you-go instances required in the scaling group. Valid values: 0 to 1000. When the number of pay-as-you-go instances is less than this value, Auto Scaling will preferentially create pay-as-you-go instances. |
|OnDemandPercentageAboveBaseCapacity|Integer|20|The percentage of pay-as-you-go instances to be created when instances are added to the scaling group. This parameter takes effect after the number of pay-as-you-go instances in the scaling group reaches the value of OnDemandBaseCapacity. Valid values: 0 to 100. |
|PendingCapacity|Integer|0|The number of ECS instances that are being added to the scaling group, but are still being configured. |
|PendingWaitCapacity|Integer|1|The number of ECS instances that are in the pending state to be added in the scaling group. |
|ProtectedCapacity|Integer|1|The number of ECS instances that are in the protected state in the scaling group. |
|RegionId|String|cn-qingdao|The region ID of the scaling group. |
|RemovalPolicies|List|OldestScalingConfiguration|Details about policies for removing ECS instances from the scaling group. Valid values:

-   OldestInstance: removes the ECS instance that was created at the earliest point in time.
-   NewestInstance: removes the ECS instance that was created at the latest point in time.
-   OldestScalingConfiguration: removes the ECS instance that was created based on the earliest scaling configuration. |
|RemovingCapacity|Integer|0|The number of ECS instances that are being removed from the scaling group. |
|RemovingWaitCapacity|Integer|1|The number of ECS instances that are in the pending state to be removed from the scaling group. |
|ScalingGroupId|String|asg-bp14wlu85wrpchm0\*\*\*\*|The ID of the scaling group. |
|ScalingGroupName|String|dyrSuvBOtO1dEdIlIbp\*\*\*\*|The name of the scaling group. |
|ScalingPolicy|String|recycle|Specifies the reclaim policy of the scaling group. Valid values:

-   recycle: The scaling group is set to Shutdown and Reclaim Mode.
-   release: The scaling group is set to Release Mode.

For more information, see [RemoveInstances](~~25955~~). |
|SpotInstancePools|Integer|5|The number of available instance types. Auto Scaling will create preemptible instances of multiple instance types available at the lowest cost. Valid values: 0 to 10. |
|SpotInstanceRemedy|Boolean|true|Specifies whether to supplement preemptible instances when the target capacity of preemptible instances is not fulfilled. When Auto Scaling receives a system message that a preemptible instance will be reclaimed, Auto Scaling will create a new instance to replace the instance to be reclaimed if this parameter is set to true. |
|StandbyCapacity|Integer|1|The number of instances that are in the standby state in the scaling group. |
|StoppedCapacity|Integer|1|The number of instances that are in the stopped state in the scaling group. |
|SuspendedProcesses|List|ScaleIn|The scaling activity that is suspended. If no scaling activity is suspended, the returned value is null. Valid values:

-   ScaleIn: removes ECS instances.
-   ScaleOut: adds ECS instances.
-   HealthCheck: performs health check.
-   AlarmNotification: sends alarm notifications.
-   ScheduledAction: triggers scheduled tasks. |
|TotalCapacity|Integer|1|The total number of ECS instances in the scaling group. |
|VServerGroups|Array of VServerGroup| |Details about backend server groups. |
|VServerGroup| | | |
|LoadBalancerId|String|147b46d767c-cn-qingdao-cm5\*\*\*\*|The ID of the SLB instance with which the backend server group is associated. |
|VServerGroupAttributes|Array of VServerGroupAttribute| |The attributes of the backend server group. |
|VServerGroupAttribute| | | |
|Port|Integer|22|The number of the port that is used by the SLB instance to provide external services. |
|VServerGroupId|String|rsp-bp12bjrny\*\*\*\*|The ID of the backend server group. |
|Weight|Integer|1|The weight of the backend server group. |
|VSwitchId|String|vsw-bp1whw2u46cn8zubm\*\*\*\*|The ID of the VSwitch that is associated with the scaling group. |
|VSwitchIds|List|vsw-bp1whw2u46cn8zubm\*\*\*\*|A collection of IDs of the VSwitches that are associated with the scaling group. If you use the VSwitchIds parameter, the VSwitchId parameter is ignored. |
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

