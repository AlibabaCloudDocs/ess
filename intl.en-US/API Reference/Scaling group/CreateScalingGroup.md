# CreateScalingGroup

You can call this operation to create a scaling group.

## Description

A scaling group is a group of ECS instances that are dynamically scaled based on the configured scenario.

The number of scaling groups that can be created in a region depends on your usage of Auto Scaling. You can go to the [Quota Center](https://quotas.console.aliyun.com/products/ess/quotas) to check the quota corresponding to the **Total Scaling Groups**.

A scaling group does not take effect immediately after it is created. You must call the [EnableScalingGroup](~~25939~~) operation so that the scaling group can execute scaling rules to trigger scaling activities.

Each scaling group must be in the same region as the Server Load Balancer \(SLB\) instance and ApsaraDB RDS instance that are associated with the scaling group. For more information, see [Regions and zones](~~40654~~).

If you specify an SLB instance when you create a scaling group, Auto Scaling automatically adds ECS instances in the scaling group to the backend server group of the specified SLB instance. The default weight of an ECS instance added to the backend server group is 50. The specified SLB instance must meet the following requirements:

-   The SLB instance must be in the Active state. You can call the [DescribeLoadBalancers](~~27582~~) operation to query the status of the specified SLB instance.
-   Health check must be enabled on all listener ports configured for the SLB instance. Otherwise, the scaling group fails to be created.

If you specify an ApsaraDB RDS instance when you create a scaling group, Auto Scaling automatically adds the internal IP addresses of ECS instances in the scaling group to the whitelist of the specified ApsaraDB RDS instance. The specified ApsaraDB RDS instance must meet the following requirements:

-   The ApsaraDB RDS instance must be in the Running state. You can call the [DescribeDBInstances](~~26232~~) operation to query the status of the specified ApsaraDB RDS instance.
-   The number of IP addresses in the ApsaraDB RDS instance whitelist cannot exceed the upper limit. For more information, see [Configure a whitelist](~~43185~~).

If the MultiAZPolicy parameter of a scaling group is set to COST\_OPTIMIZED \(cost optimization policy\):

-   You can use the OnDemandBaseCapacity, OnDemandPercentageAboveBaseCapacity, and SpotInstancePools parameters to specify the percentages of pay-as-you-go instances and preemptible instances based on the cost optimized policy. This instance allocation method is prioritized during scaling.
-   When at least one of the OnDemandBaseCapacity, OnDemandPercentageAboveBaseCapacity, and SpotInstancePools parameters is not specified, the instance types available at the lowest cost are selected to create instances based on the cost optimization policy.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=CreateScalingGroup&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateScalingGroup|The operation that you want to perform. Set the value to CreateScalingGroup. |
|MaxSize|Integer|Yes|20|The maximum number of ECS instances in the scaling group. When the number of ECS instances in the scaling group is greater than the value of MaxSize, Auto Scaling automatically removes ECS instances until the number of instances is equal to the value of MaxSize.

The value range of MaxSize depends on your usage of Auto Scaling. You can go to the [Quota Center](https://quotas.console.aliyun.com/products/ess/quotas) to check the quota corresponding to **Instances That Can Be Configured for a Scaling Group**.

For example, if the quota corresponding to **Instances That Can Be Configured for a Scaling Group** is 2000, the value range of MaxSize is 0 to 2000. |
|MinSize|Integer|Yes|2|The minimum number of ECS instances in the scaling group. When the number of ECS instances in the scaling group is less than the value of MinSize, Auto Scaling automatically creates ECS instances until the number of instances is equal to the value of MinSize.

**Note:** The value of MinSize must be less than or equal to that of MaxSize. |
|RegionId|String|Yes|cn-qingdao|The region ID of the scaling group. For more information, see [Regions and zones](~~40654~~). |
|ScalingGroupName|String|No|scalinggroup\*\*\*\*|The name of the scaling group. The name of a scaling group must be unique in a region. The name must be 2 to 64 characters in length and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a letter or digit.

The default value is the value of ScalingGroupId. |
|LaunchTemplateId|String|No|lt-m5e3ofjr1zn1aw7\*\*\*\*|The ID of the launch template, from which Auto Scaling can obtain launch configurations. |
|LaunchTemplateVersion|String|No|Default|The version number of the launch template. Valid values:

-   A fixed template version number.
-   Default: The default template version is always used.
-   Latest: The latest template version is always used. |
|InstanceId|String|No|i-28wt4\*\*\*\*|The ID of the ECS instance from which Auto Scaling obtains configuration information of the specified instance. |
|DefaultCooldown|Integer|No|300|The cooldown period after a scaling activity is executed. Scaling activities include addition and remove of ECS instances. Valid values: 0 to 86400. Unit: seconds.

During the cooldown period, Auto Scaling executes only scaling activities that are triggered by Cloud Monitor event-triggered tasks.

Default value: 300. |
|LoadBalancerIds|String|No|\["lb-bp1u7etiogg38yvwz\*\*\*\*", "lb-bp168cqrux9ai9l7f\*\*\*\*", "lb-bp1jv3m9zvj22ufxp\*\*\*\*"\]|The IDs of SLB instances. This value can be a JSON array that contains multiple SLB instance IDs. Separate multiple IDs with commas \(,\).

The number of SLB instances that can be associated with a scaling group depends on your usage of Auto Scaling. You can go to the [Quota Center](https://quotas.console.aliyun.com/products/ess/quotas) to Check the quota corresponding to **SLB Instances That Can Be Associated with a Scaling Group**. |
|DBInstanceIds|String|No|\["rm-bp142f86de0t7\*\*\*\*", "rm-bp18l1z42ar4o\*\*\*\*", "rm-bp1lqr97h4aqk\*\*\*\*"\]|The IDs of ApsaraDB RDS instances. The value can be a JSON array that contains multiple ApsaraDB RDS IDs. Separate multiple IDs with commas \(,\).

The number of ApsaraDB RDS instances that can be associated with a scaling group depends on your usage of Auto Scaling. You can go to the [Quota Center](https://quotas.console.aliyun.com/products/ess/quotas) to check the quota corresponding to **RDS Instances That Can Be Associated with a Scaling Group**. |
|RemovalPolicy.1|String|No|OldestScalingConfiguration|Policy N for removing ECS instances from the scaling group. Valid values of N: 1 to 2. Valid values:

-   OldestInstance: removes the ECS instances that are added to the scaling group at the earliest point in time.
-   NewestInstance: removes the ECS instances that are added to the scaling group at the latest point in time.
-   OldestScalingConfiguration: removes the ECS instances that are created based on the earliest scaling configuration.

Default value of RemovalPolicy.1: OldestScalingConfiguration.

Default value of RemovalPolicy.2: OldestInstance. |
|VSwitchId|String|No|vsw-bp14zolna43z266bq\*\*\*\*|The ID of the VSwitch. This parameter is used to create a VPC-type scaling group. |
|VSwitchIds.N|RepeatList|No|vsw-bp14zolna43z266bq\*\*\*\*|The ID of VSwitch N. Valid values of N: 1 to 5. If you use the VSwitchIds.N parameter, the VSwitchId parameter is ignored.

This parameter is valid only when the network type of the scaling group is VPC. The specified VSwitches and the scaling group must be in the same VPC.

The VSwitches can reside in different zones. VSwitches are prioritized based on the value of N. Value 1 indicates the highest priority. When an ECS instance cannot be created in the zone where the VSwitch with the highest priority resides, the system uses the VSwitch with the next highest priority to create the ECS instance. |
|MultiAZPolicy|String|No|PRIORITY|The ECS instance scaling policy for a multi-zone scaling group. Valid values:

-   PRIORITY: ECS instances are scaled based on the VSwitchIds.N parameter. When an ECS instance cannot be created in the zone where the VSwitch with the highest priority resides, the system uses the VSwitch with the next highest priority to create the ECS instance.
-   COST\_OPTIMIZED: ECS instances are created based on the unit prices of vCPUs in ascending order. Preemptible instances are preferentially created when preemptible instance types are specified for the scaling configuration. You can set the CompensateWithOnDemand parameter to specify whether to automatically create pay-as-you-go instances when preemptible instances cannot be created due to insufficient resources.

**Note:** COST\_OPTIMIZED takes effect only when multiple instance types are specified or at least one preemptible instance type is specified.

-   BALANCE: ECS instances are distributed evenly in multiple zones specified in the scaling group. If ECS instances are unevenly distributed among the zones due to certain issues such as insufficient ECS resources, you can reallocate instances to make them evenly distributed by calling the [RebalanceInstance](~~71516~~) operation.

Default value: PRIORITY. |
|HealthCheckType|String|No|ECS|The health check mode of the scaling group. Valid values:

-   NONE: The system performs no health check.
-   ECS: The system performs a health check on ECS instances in the scaling group.

Default value: ECS. |
|LifecycleHook.N.LifecycleHookName|String|No|lifecyclehook\*\*\*\*|The name of the lifecycle hook. The name is used to specify a lifecycle hook and cannot be modified if it is set. |
|LifecycleHook.N.LifecycleTransition|String|No|SCALE\_OUT|The type of scaling activities to which the lifecycle hook applies. Valid values:

-   SCALE\_OUT: scale-out events of the scaling group
-   SCALE\_IN: scale-in events of the scaling group |
|LifecycleHook.N.DefaultResult|String|No|CONTINUE|The action that the scaling group takes when the lifecycle hook times out. Valid values:

-   CONTINUE: The scaling group continues to respond to a scale-in or scale-out event.
-   ABANDON: The scaling group releases the created ECS instances if the scaling activity type is scale-out or removes the ECS instances to be scaled in if the scaling activity type is scale-in.

If the scaling group has multiple lifecycle hooks and one of them is terminated when the DefaultResult parameter is set to ABANDON during a scale-in activity, the remaining lifecycle hooks in the same scaling group are also terminated. Otherwise, the scaling activity will proceed normally after the lifecycle hook times out and continue with the action specified by the DefaultResult parameter.

Default value: CONTINUE. |
|LifecycleHook.N.HeartbeatTimeout|Integer|No|600|The wait period before the lifecycle hook times out. When the lifecycle hook times out, the scaling group performs the default action. Valid values: 30 to 21600. Unit: seconds.

You can prevent the lifecycle hook from timing out by calling the [RecordLifecycleActionHeartbeat](~~73846~~) operation. You can also call the [CompleteLifecycleAction](~~73847~~) operation to resume a suspended scaling activity before the corresponding lifecycle hook times out.

Default value: 600. |
|LifecycleHook.N.NotificationMetadata|String|No|Test|The fixed string to be included when Auto Scaling sends a notification about the wait state of a scaling activity. The parameter value cannot exceed 128 characters in length. Auto Scaling sends the specified NotificationMetadata parameter value along with the notification message so that you can categorize your notifications. The NotificationMetadata parameter is valid only after you set the NotificationArn parameter. |
|LifecycleHook.N.NotificationArn|String|No|acs:ess:cn-hangzhou:1111111111:queue/queue2|The Alibaba Cloud Resource Name \(ARN\) of the notification object that Auto Scaling uses to notify you when an instance is in the transition state for the lifecycle hook. This object can be either an MNS queue or an MNS topic. The format of the parameter value is acs:ess:\{region\}:\{account-id\}:\{resource-relative-id\}.

-   region: the region in which to deploy the scaling group.
-   account-id: the ID of the Alibaba Cloud account.

Examples:

-   MNS queue: acs:ess:\{region\}:\{account-id\}:queue/\{queuename\}
-   MNS topic: acs:ess:\{region\}:\{account-id\}:topic/\{topicname\} |
|VServerGroup.N.LoadBalancerId|String|No|lb-bp1u7etiogg38yvwz\*\*\*\*|The ID of the SLB instance with which the VServer group is associated.

For more information, see [AttachVServerGroups](~~98983~~). |
|VServerGroup.N.VServerGroupAttribute.N.VServerGroupId|String|No|rsp-bp1443g77\*\*\*\*|The ID of the VServer group.

For more information, see [AttachVServerGroups](~~98983~~). |
|VServerGroup.N.VServerGroupAttribute.N.Port|Integer|No|22|The port number that is used by Auto Scaling to add the ECS instances to VServer group N. Valid values: 1 to 65535.

For more information, see [AttachVServerGroups](~~98983~~). |
|VServerGroup.N.VServerGroupAttribute.N.Weight|Integer|No|100|The weight set for the ECS instances that are added to VServer group N. Valid values: 0 to 100.

For more information, see [AttachVServerGroups](~~98983~~).

Default value: 50. |
|ScalingPolicy|String|No|recycle|Specifies the reclaim mode of the scaling group. Valid values:

-   recycle: The scaling group is set to Shutdown and Reclaim Mode.
-   release: The scaling group is set to Release Mode.

ScalingPolicy specifies the reclaim modes of scaling groups, but the policy that is used to remove ECS instances from scaling groups is determined by the RemovePolicy parameter of the RemoveInstances operation. For more information, see[RemoveInstances](~~25955~~). |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |
|OnDemandBaseCapacity|Integer|No|30|The minimum number of pay-as-you-go instances required in the scaling group. Valid values: 0 to 1000. When the number of pay-as-you-go instances is less than this value, the scaling group will preferentially create pay-as-you-go instances. |
|OnDemandPercentageAboveBaseCapacity|Integer|No|20|The percentage of pay-as-you-go instances to be created when instances are added to the scaling group.This parameter takes effect after the number of pay-as-you-go instances in the scaling group reaches the OnDemandBaseCapacity value. Valid values: 0 to 100. |
|SpotInstanceRemedy|Boolean|No|true|Specifies whether to supplement preemptible instances when the target capacity of preemptible instances is not fulfilled. When Auto Scaling receives a system message indicating that a preemptible instance will be reclaimed, Auto Scaling will create a new instance to replace the instance to be reclaimed if this parameter is set to true. |
|CompensateWithOnDemand|Boolean|No|true|Specifies whether to automatically create pay-as-you-go instances to meet the required number of ECS instances when the expected capacity of preemptible instances cannot be fulfilled due to reasons such as cost or insufficient resources. This parameter takes effect when the MultiAZPolicy parameter is set to COST\_OPTIMIZED. Valid values:

-   true: Pay-as -you-go instances can be created.
-   false: Pay-as -you-go instances cannot be created.

Default value: true. |
|SpotInstancePools|Integer|No|5|The number of available instance types. Auto Scaling will create preemptible instances of multiple instance types available at the lowest cost. Valid values: 1 to 10. |
|DesiredCapacity|Integer|No|5|The expected number of ECS instances in the scaling group. Auto Scaling automatically maintains the ECS instances at this number. The expected number must be between the value of MaxSize and the value of MinSize. |
|GroupDeletionProtection|Boolean|No|true|Specifies whether to enable scaling group deletion protection. Valid values:

-   true: Scaling group deletion protection is enabled. You cannot delete the scaling group.
-   false: Scaling group deletion protection is disabled.

Default value: false. |
|Tag.N.Key|String|No|Department|The key of tag N of the scaling group. |
|Tag.N.Value|String|No|Finance|The value of tag N of the scaling group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ScalingGroupId|String|asg-bp14wlu85wrpchm0\*\*\*\*|The ID of the scaling group. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=CreateScalingGroup
&RegionId=cn-qingdao
&MaxSize=20
&MinSize=2
&LoadBalancerIds=["lb-bp1u7etiogg38yvwz****", "lb-bp168cqrux9ai9l7f****", "lb-bp1jv3m9zvj22ufxp****"]
&DBInstanceIds=["rm-bp142f86de0t7****", "rm-bp18l1z42ar4o****", "rm-bp1lqr97h4aqk****"]
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateScalingGroupResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <ScalingGroupId>asg-bp14wlu85wrpchm0****</ScalingGroupId>
</CreateScalingGroupResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "ScalingGroupId": "asg-bp14wlu85wrpchm0****"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|400

|IncorrectDBInstanceStatus

|The current status of DB instance “XXX” does not support this action.

|The error message returned because the specified ApsaraDB RDS instance is not in the Running state. |
|400

|IncorrectLoadBalancerHealthCheck

|The current health check type of specified load balancer does not support this action.

|The error message returned because health check is not enabled for the specified SLB instance. |
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|The error message returned because the specified SLB instance is not in the Active state. |
|400

|IncorrectVSwitchStatus

|The current status of virtual switch does not support this operation.

|The error message returned because the VSwitch is unavailable and ECS instances cannot be created. |
|400

|InvalidDBInstanceId. RegionMismatch

|DB instance "XXX" and the specified scaling group are not in the same Region.

|The error message returned because the specified ApsaraDB RDS instance and the specified scaling group are not in the same region. |
|400

|InvalidLoadBalancerId.IncorrectAddressType

|The current address type of specified load balancer does not support this action.

|The error message returned because the network type of the specified SLB instance does not match the network type of the VSwitch. |
|400

|InvalidLoadBalancerId.IncorrectInstanceNetworkType

|The network type of the instance in specified Load Balancer does not support this action.

|The error message returned because the network type of the ECS instance attached to the specified SLB instance is different from that of the scaling group. |
|400

|InvalidLoadBalancerId.RegionMismatch

|The specified Load Balancer and the specified scaling group are not in the same Region.

|The error message returned because the specified SLB instance and the scaling group are not in the same region. |
|400

|InvalidLoadBalancerId.VPCMismatch

|The specified virtual switch and the instance in specified Load Balancer are not in the same VPC.

|The error message returned because the VSwitch and the ECS instance attached to the SLB instance of the scaling group are not in the same VPC. |
|400

|InvalidParameter

|The specified value of parameter "ScalingPolicy" is not valid.

|The error message returned because the specified ScalingPolicy parameter is invalid. |
|400

|InvalidParameter.Conflict

|The value of parameter &lt;parameter name&gt; and parameter &lt;parameter name&gt; are conflict.

|The error message returned because the specified MinSize parameter is greater than the MaxSize parameter. |
|400

|InvalidScalingGroupName.Duplicate

|The specified value of parameter &lt;parameter name&gt; is duplicated.

|The error message returned because the specified scaling group name already exists. |
|400

|QuotaExceeded.DBInstanceSecurityIP

|Security IP quota exceeded in DB instance “XXX”.

|The error message returned because the maximum number of IP addresses in the specified ApsaraDB RDS instance whitelist has been reached. |
|400

|QuotaExceeded.PrivateIpAddress

|Private IP address quota exceeded in the specified virtual switch.

|The error message returned because no idle private IP addresses are available in the CIDR block of the VSwitch. |
|400

|QuotaExceeded.ScalingGroup

|Scaling group quota exceeded.

|The error message returned because the maximum number of scaling groups has been reached. |
|400

|QuotaExceeded.VPCInstance

|Instance quota exceeded in the specified VPC.

|The error message returned because the maximum number of instances in the VPC has been reached. |
|404

|InvalidDBInstanceId.NotFound

|DB instance "XXX" does not exist.

|The error message returned because the specified ApsaraDB RDS instance does not exist. |
|404

|InvalidLoadBalancerId.NotFound

|The specified Load Balancer does not exist.

|The error message returned because the specified SLB instance does not exist. |
|404

|InvalidRegionId.NotFound

|The specified region does not exist.

|The error message returned because the specified region does not exist. |
|404

|InvalidVSwitchId.NotFound

|The specified virtual switch does not exist.

|The error message returned because the specified VSwitch does not exist. |
|400

|LaunchTemplateVersionSet.NotFound

|The specific version of launch template is not exist.

|The error message returned because the specified version of the launch template does not exist. |
|400

|LaunchTemplateSet.NotFound

|The specified launch template set is not found.

|The error message returned because the specified launch template does not exist. |
|400

|TemplateMissingParameter.ImageId

|The input parameter "ImageId" that is mandatory for processing this request is not supplied.

|The error message returned because the ImageId parameter required for the specified launch template is not specified. |
|400

|TemplateMissingParameter.InstanceTypes

|The input parameter "InstanceTypes" that is mandatory for processing this request is not supplied.

|The error message returned because the InstanceTypes parameter required for the specified launch template is not specified. |
|400

|TemplateMissingParameter.SecurityGroup

|The input parameter "SecurityGroup" that is mandatory for processing this request is not supplied.

|The error message returned because the SecurityGroup parameter required for the specified launch template is not specified. |
|400

|TemplateVersion.NotNumber

|The input parameter "LaunchTemplateVersion" is supposed to be a string representing the version number.

|The error message returned because the specified fixed version number specified by the LaunchTemplateVersion parameter for the launch template is not numerical. |
