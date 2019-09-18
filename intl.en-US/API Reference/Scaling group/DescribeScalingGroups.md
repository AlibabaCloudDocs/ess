# DescribeScalingGroups {#doc_api_Ess_DescribeScalingGroups .reference}

You can call this operation to query scaling groups.

## Debugging {#api_explorer .section}

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=Ess&api=DescribeScalingGroups&type=RPC&version=2014-08-28)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|RegionId|String|Yes|cn-qingdao|The ID of the region where a scaling group resides.

 |
|Action|String|No|DescribeScalingGroups|The operation that you want to perform. Set the value to DescribeScalingGroups.

 |
|PageNumber|Integer|No|1|The page number of the scaling group list to return. Pages start from page 1.

 Default value: 1.

 |
|PageSize|Integer|No|10|The number of entries to return on each page. Maximum value: 50.

 Default value: 10.

 |
|ScalingGroupId.1|String|No|dyrSuvBOtO1dEdIlIbp\*\*\*\*|The ID of scaling group N to be queried. Valid values of N: 1 to 20. The IDs of inactive scaling groups will not be displayed in the query result and no errors will be returned.

 |
|ScalingGroupName.1|String|No|dyrSuvBOtO1dEdIlIbp\*\*\*\*|The name of scaling group N to be queried. Valid values of N: 1 to 20. The names of inactive scaling groups will not be displayed in the query result and no errors will be returned.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The current page number.

 |
|PageSize|Integer|50|The number of entries returned on each page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request.

 |
|ScalingGroups| | |The set of scaling groups.

 |
|ActiveCapacity|Integer|1|The number of Elastic Compute Service \(ECS\) instances that have been added to the scaling group and are running properly.

 |
|ActiveScalingConfigurationId|String|dyo713cNYIB4ddEVlKbc\*\*\*\*|The ID of the active scaling configuration in the scaling group.

 |
|CreationTime|String|2014-08-14T10:58Z|The time when the scaling group was created.

 |
|DBInstanceIds| |rdszzzyyuny\*\*\*\*|The IDs of ApsaraDB for Relational Database Service \(RDS\) instances associated with the scaling group.

 |
|DefaultCooldown|Integer|60|The default cooldown period of the scaling group. During the cooldown period calculated for a scaling activity, the scaling group does not execute any other scaling activities triggered by [CloudMonitor](~~35170~~) alarm tasks.

 |
|HealthCheckType|String|ECS|The health check mode of the scaling group. Valid values:

 -   NONE: The system performs no health check.
-   ECS: The system performs the health check on ECS instances in the scaling group.

 |
|LaunchTemplateId|String|lt-m5e3ofjr1zn1aw7\*\*\*\*|The ID of the instance launch template used by the scaling group.

 |
|LaunchTemplateVersion|String|true|The version of the instance launch template used by the scaling group.

 |
|LifecycleState|String|Active|The status of the scaling group. Valid values:

 -   Active: Active scaling groups can receive requests to execute scaling rules and trigger scaling activities.
-   Inactive: Inactive scaling groups cannot receive any requests to execute scaling rules.
-   Deleting: Scaling groups that are being deleted cannot receive any requests to execute scaling rules and their parameters cannot be modified.

 |
|LoadBalancerIds| |147b46d767c-cn-qingdao-cm5\*\*\*\*|The IDs of Server Load Balancer \(SLB\) instances associated with the scaling group.

 |
|MaxSize|Integer|2|The maximum number of ECS instances in the scaling group.

 |
|MinSize|Integer|1|The minimum number of ECS instances in the scaling group.

 |
|ModificationTime|String|2014-08-14T10:58Z|The time when the scaling group was modified.

 |
|MultiAZPolicy|String|PRIORITY|The ECS instance scaling policy for a multi-zone scaling group. Valid values:

 -   PRIORITY: ECS instances are scaled based on the VSwitchIds.N parameter. When an ECS instance cannot be created in the zone where the VSwitch with the highest priority resides, the system automatically uses the VSwitch with the next highest priority to create the ECS instance.
-   COST\_OPTIMIZED: ECS instances are created based on the unit price of vCPU, from low to high. Preemptible instances are created first when preemptible instance types are specified for the scaling configuration. Pay-as-you-go instances are created automatically when all types of preemptible instances are unavailable due to issues such as insufficient ECS resources.

**Note:** COST\_OPTIMIZED takes effect only when multiple instance types are specified or at least one preemptible instance type is specified.

-   BALANCE: ECS instances are distributed evenly in multiple zones specified in the scaling group. If ECS instances are unevenly distributed among the zones due to certain issues such as insufficient ECS resources, you can reallocate instances to make them evenly distributed by calling the [RebalanceInstance](~~71516~~) operation.

 |
|OnDemandBaseCapacity|Integer|30|The minimum number of pay-as-you-go instances required in the scaling group. Valid values: 0 to 1000. When the number of pay-as-you-go instances is smaller than this value, the scaling group will attempt to create pay-as-you-go instances over other instances.

 |
|OnDemandPercentageAboveBaseCapacity|Integer|20|The percentage of pay-as-you-go instances to be created when instances are added to the scaling group. This parameter takes effect after the number of instances reaches the OnDemandBaseCapacity value. Valid values: 0 to 100.

 |
|PendingCapacity|Integer|0|The number of ECS instances that are being added to the scaling group, but are still being configured.

 |
|PendingWaitCapacity|Integer|1|The number of ECS instances that are in the pending state in the scaling group.

 |
|ProtectedCapacity|Integer|1|The number of ECS instances that are in the protected state in the scaling group.

 |
|RegionId|String|cn-qingdao|The ID of the region where the scaling group resides.

 |
|RemovalPolicies| |OldestScalingConfiguration|The set of policies for removing ECS instances from the scaling group.

 |
|RemovingCapacity|Integer|0|The number of ECS instances that are currently being removed from the scaling group.

 |
|RemovingWaitCapacity|Integer|1|The number of ECS instances that are pending to be removed from the scaling group.

 |
|ScalingGroupId|String|dyrSuvBOtO1dEdIlIbp\*\*\*\*|The ID of the scaling group.

 |
|ScalingGroupName|String|dyrSuvBOtO1dEdIlIbp\*\*\*\*|The name of the scaling group.

 |
|ScalingPolicy|String|recycle|The reclaim policy of the scaling group. Valid values:

 -   recycle: The scaling group is set to the Shutdown and Reclaim Mode, which stops ECS instances and reclaims resources.
-   release: The scaling group is set to the Release Mode, which removes or adds ECS instances.

 For more information, see [RemoveInstances](~~25955~~).

 |
|SpotInstancePools|Integer|5|The number of available instance types. The scaling group will create preemptible instances of multiple instance types available at the lowest cost. Valid values: 0 to 10.

 |
|SpotInstanceRemedy|Boolean|true|Indicates whether supplementing preemptible instances was enabled when the target capacity of preemptible instances is not fulfilled. When receiving a system message that a preemptible instance will be reclaimed, the scaling group will create a new instance to replace the instance to be reclaimed if this parameter is set to true.

 |
|StandbyCapacity|Integer|1|The number of instances that are in the standby state in the scaling group.

 |
|StoppedCapacity|Integer|1|The number of instances that are in the stopped state in the scaling group.

 |
|TotalCapacity|Integer|1|The total number of ECS instances in the scaling group.

 |
|VServerGroups| | |The list of VServer groups.

 |
|LoadBalancerId|String|147b46d767c-cn-qingdao-cm5\*\*\*\*|The ID of the SLB instance with which the VServer group is associated.

 |
|VServerGroupAttributes| | |The attributes of the VServer group.

 |
|Port|Integer|22|The number of the port that is used by the SLB instance to provide public-facing services.

 |
|VServerGroupId|String|rsp-bp12bjrny\*\*\*\*|The ID of the VServer group.

 |
|Weight|Integer|1|The weight of the VServer group.

 |
|VSwitchId|String|vpc-25j4g\*\*\*\*|The ID of the VSwitch associated with the scaling group.

 |
|VSwitchIds| |vpc-25j4g\*\*\*\*|The set of IDs of the VSwitches associated with the scaling group. If you use the VSwitchIds parameter, the VSwitchId parameter is ignored.

 |
|VpcId|String|vpc-\*\*\*\*|The ID of the VPC to which the scaling group belongs.

 |
|TotalCount|Integer|1|The total number of scaling groups.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DescribeScalingGroups
&RegionId=cn-qingdao
&PageSize=50
&<Common request parameters>

```

Sample success response

`XML` format

``` {#xml_return_success_demo}
<DescribeScalingGroupsResponse>
      <RequestId>6393C3A8-B611-42F2-AFA6-F080FC45D5D0</RequestId>
      <TotalCount>1</TotalCount>
      <PageNumber>1</PageNumber>
      <PageSize>10</PageSize>
      <ScalingGroups> 
            <ScalingGroup>
                  <ActiveCapacity>1</ActiveCapacity>
                  <ActiveScalingConfigurationId>dyo713cNYIB4ddEVlKbc****</ActiveScalingConfigurationId>
                  <DBInstanceIds>
                        <DBInstanceId>rdszzzyyuny****</DBInstanceId>
                  </DBInstanceIds>
                  <VSwitchId>vpc-25j4g****</VSwitchId>
                  <DefaultCooldown>20</DefaultCooldown>
                  <LifecycleState>Active</LifecycleState>
                  <LoadBalancerIds>
                        <LoadBalancerId>147b46d767c-cn-qingdao-cm5****</LoadBalancerId>
                  </LoadBalancerIds>
                  <MaxSize>1</MaxSize>
                  <MinSize>0</MinSize>
                  <PendingCapacity>0</PendingCapacity>
                  <RegionId>cn-qingdao</RegionId>
                  <RemovingCapacity>0</RemovingCapacity>
                  <ScalingGroupId>dyrSuvBOtO1dEdIlIbp****</ScalingGroupId>
                  <ScalingGroupName>dyrSuvBOtO1dEdIlIbp****</ScalingGroupName>
                  <RemovalPolicies>
                        <RemovalPolicy>OldestScalingConfiguration</RemovalPolicy>
                        <RemovalPolicy>OldestInstance</RemovalPolicy>
                  </RemovalPolicies>
                  <TotalCapacity>1</TotalCapacity>
                  <CreationTime>2014-08-14T10:58Z</CreationTime>
            </ScalingGroup>
      </ScalingGroups>
</DescribeScalingGroupsResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":10,
	"RequestId":"68386699-8B9E-4D5B-BC4C-75A28F6C2A00",
	"ScalingGroups":{
		"ScalingGroup":[
			{
				"DefaultCooldown":300,
				"MaxSize":2,
				"RemovalPolicies":{
					"RemovalPolicy":[
						"OldestScalingConfiguration",
						"OldestInstance"
					]
				},
				"PendingCapacity":0,
				"RemovingCapacity":0,
				"VSwitchId":"vpc-25j4g****",
				"ScalingGroupName":"b8pYCVbIV5k9cz4PWpbe****",
				"CreationTime":"2014-08-14T10:58Z",
				"ActiveCapacity":0,
				"ActiveScalingConfigurationId":" dyo713cNYIB4ddEVlKbc****",
				"ScalingGroupId":"b8pYCVbIV5k9cz4PWpbe****",
				"RegionId":"cn-qingdao",
				"TotalCapacity":0,
				"DBInstanceIds":{
					"DBInstanceId":[
						"rdsia3u3yia****",
						"rdszzzyyuny****"
					]
				},
				"LoadBalancerIds":{
					"LoadBalancerId":[
						"147b46d767c-cn-qingdao-cm5****"
					]
				},
				"MinSize":1,
				"LifecycleState":"Inactive"
			}
		]
	}
}
```

## Error codes { .section}

