# CreateScalingGroup

Creates a scaling group.

## Description

A scaling group is a group of Elastic Compute Service \(ECS\) instances that are dynamically scaled based on the configured scenario.

The number of scaling groups that can be created in a region depends on your usage of Auto Scaling. You can go to the [Quota Center](https://quotas.console.aliyun.com/products/ess/quotas) to check the quota corresponding to the **Total Scaling Groups**.

A scaling group does not immediately take effect after it is created. You must call the [EnableScalingGroup](~~25939~~) operation to enable the scaling group so that the scaling group can execute scaling rules to trigger scaling activities.

Each scaling group must be in the same region as the Server Load Balancer \(SLB\) instance and ApsaraDB RDS instance that are associated with the scaling group. For more information, see [Regions and zones](~~40654~~).

If you specify an SLB instance when you create a scaling group, Auto Scaling automatically adds ECS instances in the scaling group to the backend server group of the specified SLB instance. You can specify a server group to which to add the ECS instances. ECS instances can be added to the following types of server groups:

-   Default server group: The group of ECS instances that are used to receive requests. If the listener is not configured with a vServer group or a primary/secondary server group, requests are forwarded to the ECS instances in the default server group.
-   vServer group: If you want to distribute different requests to different backend servers or configure domain name- or URL-based routing methods, you can use vServer groups.

**Note:** If you specify the default server group and multiple vServer groups at the same time, ECS instances are added to all the specified server groups.


The default weight of an ECS instance added to the backend server group is 50. The specified SLB instance must meet the following requirements:

-   The SLB instance must be in the Active state. You can call the [DescribeLoadBalancers](~~27582~~) operation to query the status of the specified SLB instance.
-   Health check must be enabled on all listener ports configured for the SLB instance. Otherwise, the scaling group fails to be created.

If you specify an ApsaraDB RDS instance when you create a scaling group, Auto Scaling automatically adds the internal IP addresses of ECS instances in the scaling group to the whitelist of the specified ApsaraDB RDS instance. The specified ApsaraDB RDS instance must meet the following requirements:

-   The ApsaraDB RDS instance must be in the Running state. You can call the [DescribeDBInstances](~~26232~~) operation to query the status of the specified ApsaraDB RDS instance.
-   The number of IP addresses in the whitelist of the specified ApsaraDB RDS instance cannot exceed the upper limit. For more information, see [Configure a whitelist](~~43185~~).

If the MultiAZPolicy parameter of a scaling group is set to COST\_OPTIMIZED:

-   You can use the OnDemandBaseCapacity, OnDemandPercentageAboveBaseCapacity, and SpotInstancePools parameters to specify the percentages of pay-as-you-go instances and preemptible instances based on the cost optimized policy. This instance allocation method is prioritized during scaling.
-   When at least one of the OnDemandBaseCapacity, OnDemandPercentageAboveBaseCapacity, and SpotInstancePools parameters is not specified, the instance types available at the lowest cost are used to create instances based on the cost optimization policy.

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
|ScalingGroupName|String|No|scalinggroup\*\*\*\*|The name of the scaling group. The name of a scaling group must be unique in a region. The name must be 2 to 64 characters in length, and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a letter or digit.

The default value is the value of ScalingGroupId. |
|LaunchTemplateId|String|No|lt-m5e3ofjr1zn1aw7\*\*\*\*|The ID of the launch template that is used by Auto Scaling to create ECS instances. |
|LaunchTemplateVersion|String|No|Default|The version number of the launch template. Valid values:

-   A fixed template version number.
-   Default: The default template version is always used.
-   Latest: The latest template version is always used. |
|InstanceId|String|No|i-28wt4\*\*\*\*|The ID of the ECS instance from which Auto Scaling obtains configuration information. |
|DefaultCooldown|Integer|No|300|The cooldown time after a scale-in or scale-out event is executed. Valid values: 0 to 86400. Unit: seconds.

During the cooldown time, Auto Scaling executes only scaling activities that are triggered by CloudMonitor event-triggered tasks.

Default value: 300. |
|LoadBalancerIds|String|No|\["lb-bp1u7etiogg38yvwz\*\*\*\*", "lb-bp168cqrux9ai9l7f\*\*\*\*", "lb-bp1jv3m9zvj22ufxp\*\*\*\*"\]|The IDs of SLB instances. This value can be a JSON array that contains multiple SLB instance IDs. Separate multiple IDs with commas \(,\).

The number of SLB instances that can be associated with a scaling group depends on your usage of Auto Scaling. You can go to the [Quota Center](https://quotas.console.aliyun.com/products/ess/quotas) to check the quota corresponding to **SLB Instances That Can Be Associated with a Scaling Group**. |
|DBInstanceIds|String|No|\["rm-bp142f86de0t7\*\*\*\*", "rm-bp18l1z42ar4o\*\*\*\*", "rm-bp1lqr97h4aqk\*\*\*\*"\]|The IDs of ApsaraDB RDS instances. The value can be a JSON array that contains multiple ApsaraDB RDS IDs. Separate multiple IDs with commas \(,\).

The number of ApsaraDB RDS instances that can be associated with a scaling group depends on your usage of Auto Scaling. You can go to the [Quota Center](https://quotas.console.aliyun.com/products/ess/quotas) to check the quota corresponding to **RDS Instances That Can Be Associated with a Scaling Group**. |
|RemovalPolicy.1|String|No|OldestScalingConfiguration|Policy N for removing ECS instances from the scaling group. Valid values of N: 1 to 2. Valid values:

-   OldestInstance: removes ECS instances that are added to the scaling group at the earliest point in time.
-   NewestInstance: removes ECS instances that are most recently added to the scaling group.
-   OldestScalingConfiguration: removes ECS instances that are created based on the earliest scaling configuration.

Default value of RemovalPolicy.1: OldestScalingConfiguration.

Default value of RemovalPolicy.2: OldestInstance. |
|VSwitchId|String|No|vsw-bp14zolna43z266bq\*\*\*\*|The ID of the vSwitch. If VSwitchId is specified, the network type of the scaling group is VPC.

**Note:** If VSwitchId or VSwitchIds.N is not specified, the network type of the scaling group is classic network. |
|VSwitchIds.N|RepeatList|No|vsw-bp14zolna43z266bq\*\*\*\*|The ID of vSwitch N. Valid values of N: 1 to 5. If you use the VSwitchIds.N parameter, the VSwitchId parameter is ignored. If VSwitchIds.N is specified, the network type of the scaling group is VPC.

When you specify multiple vSwitches, take note of the following items:

-   The vSwitches must belong to the same VPC.
-   The vSwitches can belong to different zones.
-   vSwitches are sorted in ascending order. 1 indicates the highest priority. When an ECS instance cannot be created in the zone where the vSwitch with the highest priority resides, the system automatically uses the vSwitch with the next highest priority to create the ECS instance.

**Note:** If VSwitchId or VSwitchIds.N is not specified, the network type of the scaling group is classic network. |
|MultiAZPolicy|String|No|PRIORITY|The ECS instance scaling policy for a multi-zone scaling group. Valid values:

-   PRIORITY: ECS instances are scaled based on the VSwitchIds.N parameter. When an ECS instance cannot be created in the zone where the vSwitch with the highest priority resides, the system uses the vSwitch with the next highest priority to create the ECS instance.
-   COST\_OPTIMIZED: ECS instances are created based on the unit prices of vCPUs in ascending order. Preemptible instances are preferentially created when preemptible instance types are specified for the scaling configuration. You can set the CompensateWithOnDemand parameter to specify whether to automatically create pay-as-you-go instances when preemptible instances cannot be created due to insufficient resources.

**Note:** COST\_OPTIMIZED is valid only when multiple instance types are specified or at least one preemptible instance type is specified.

-   BALANCE: ECS instances are evenly distributed in multiple zones specified in the scaling group. If ECS instances are unevenly distributed among the zones due to issues such as insufficient ECS resources, you can reallocate instances to make them evenly distributed by calling the [RebalanceInstance](~~71516~~) operation.

Default value: PRIORITY. |
|HealthCheckType|String|No|ECS|The health check mode of the scaling group. Valid values:

-   NONE: The system performs no health check.
-   ECS: The system performs a health check on ECS instances in the scaling group.

Default value: ECS. |
|LifecycleHook.N.LifecycleHookName|String|No|lifecyclehook\*\*\*\*|The name of lifecycle hook N. After this parameter is specified, you cannot modify the name of the lifecycle hook. If this parameter is not specified, the name of the lifecycle hook is the same as the ID of the lifecycle hook. |
|LifecycleHook.N.LifecycleTransition|String|No|SCALE\_OUT|The type of scaling activities to which the lifecycle hook applies. Valid values:

-   SCALE\_OUT: scale-out events
-   SCALE\_IN: scale-in events

**Note:** If lifecycle hooks are specified for the scaling group, LifecycleHook.N.LifecycleTransition is required and other related parameters are optional. |
|LifecycleHook.N.DefaultResult|String|No|CONTINUE|The action that the scaling group takes when the lifecycle hook times out. Valid values:

-   CONTINUE: Auto Scaling continues to respond to a scale-in or scale-out event.
-   ABANDON: Auto Scaling releases the created ECS instances if the scaling activity type is scale-out or removes the ECS instances to be scaled in if the scaling activity type is scale-in.

If the scaling group has multiple lifecycle hooks and one of them is terminated when the DefaultResult parameter is set to ABANDON during a scale-in event, the remaining lifecycle hooks in the same scaling group are also terminated. Otherwise, the scaling activity proceeds normally after the lifecycle hook times out and continues with the action specified by the DefaultResult parameter.

Default value: CONTINUE. |
|LifecycleHook.N.HeartbeatTimeout|Integer|No|600|The wait period before the lifecycle hook times out. When the lifecycle hook times out, Auto Scaling performs the default action. Valid values: 30 to 21600. Unit: seconds.

You can prevent the lifecycle hook from timing out by calling the [RecordLifecycleActionHeartbeat](~~73846~~) operation. You can also call the [CompleteLifecycleAction](~~73847~~) operation to resume a suspended scaling activity before the corresponding lifecycle hook times out.

Default value: 600. |
|LifecycleHook.N.NotificationMetadata|String|No|Test|The fixed string to be included when Auto Scaling sends a notification about the wait state of a scaling activity. The parameter value cannot exceed 128 characters in length. Auto Scaling sends the specified NotificationMetadata parameter value along with the notification message so that you can categorize your notifications. The NotificationMetadata parameter is valid only after you specify the NotificationArn parameter. |
|LifecycleHook.N.NotificationArn|String|No|acs:ess:cn-hangzhou:1111111111:queue/queue2|The Alibaba Cloud Resource Name \(ARN\) of the notification object that Auto Scaling uses to notify you when an instance is in the transition state for the lifecycle hook. This object can be a Message Service \(MNS\) queue or an MNS topic. The parameter value is in the following format: acs:ess:\{region\}:\{account-id\}:\{resource-relative-id\}.

-   region: the region where the scaling group resides
-   account-id: the ID of the Alibaba Cloud account

The following code provides an example:

-   MNS queue: acs:ess:\{region\}:\{account-id\}:queue/\{queuename\}
-   MNS topic: acs:ess:\{region\}:\{account-id\}:topic/\{topicname\} |
|VServerGroup.N.LoadBalancerId|String|No|lb-bp1u7etiogg38yvwz\*\*\*\*|The ID of the SLB instance with which the vServer group is associated.

For more information, see [AttachVServerGroups](~~98983~~). |
|VServerGroup.N.VServerGroupAttribute.N.VServerGroupId|String|No|rsp-bp1443g77\*\*\*\*|The ID of vServer group N.

For more information, see [AttachVServerGroups](~~98983~~). |
|VServerGroup.N.VServerGroupAttribute.N.Port|Integer|No|22|The port number that is used by Auto Scaling to add the ECS instances to vServer group N. Valid values: 1 to 65535.

For more information, see [AttachVServerGroups](~~98983~~). |
|VServerGroup.N.VServerGroupAttribute.N.Weight|Integer|No|100|The weight set for the ECS instances that are added to vServer group N. Valid values: 0 to 100.

For more information, see [AttachVServerGroups](~~98983~~).

Default value: 50. |
|ScalingPolicy|String|No|recycle|Specifies the reclaim mode of the scaling group. Valid values:

-   recycle: The scaling group is set to Shutdown and Reclaim Mode.
-   release: The scaling group is set to Release Mode.

ScalingPolicy specifies the reclaim modes of scaling groups, but the policy that is used to remove ECS instances from scaling groups is determined by the RemovePolicy parameter of the RemoveInstances operation. For more information, see [RemoveInstances](~~25955~~) . |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to guarantee the idempotence of the request. You can use the client to generate the value, but you must make sure that the value is unique among different requests. The token can contain only ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |
|OnDemandBaseCapacity|Integer|No|30|The minimum number of pay-as-you-go instances required in the scaling group. Valid values: 0 to 1000. When the number of pay-as-you-go instances is less than this value, Auto Scaling preferentially creates pay-as-you-go instances. |
|OnDemandPercentageAboveBaseCapacity|Integer|No|20|The percentage of pay-as-you-go instances to be created when instances are added to the scaling group. This parameter is valid after the number of pay-as-you-go instances in the scaling group reaches the OnDemandBaseCapacity value. Valid values: 0 to 100. |
|SpotInstanceRemedy|Boolean|No|true|Specifies whether to supplement preemptible instances. When Auto Scaling receives a system message indicating that a preemptible instance is reclaimed, Auto Scaling creates a new instance to replace the instance to be reclaimed if this parameter is set to true. |
|CompensateWithOnDemand|Boolean|No|true|Specifies whether to automatically create pay-as-you-go instances to meet the required number of ECS instances when the expected capacity of preemptible instances cannot be fulfilled due to reasons such as cost or insufficient resources. This parameter takes effect when the MultiAZPolicy parameter is set to COST\_OPTIMIZED. Valid values:

-   true: Pay-as-you-go instances can be created.
-   false: Pay-as-you-go instances cannot be created.

Default value: true. |
|SpotInstancePools|Integer|No|5|The number of available instance types. Auto Scaling creates preemptible instances of multiple available instance types at the lowest cost. Valid values: 1 to 10. |
|DesiredCapacity|Integer|No|5|The expected number of ECS instances in the scaling group. Auto Scaling automatically maintains ECS instances at this number. The expected number must be between the value of MaxSize and the value of MinSize. |
|GroupDeletionProtection|Boolean|No|true|Specifies whether to enable deletion protection for the scaling group. Valid values:

-   true: enables deletion protection for the scaling group. In this case, you cannot delete the scaling group.
-   false: disables deletion protection for the scaling group.

Default value: false. |
|Tag.N.Key|String|No|Department|The key of tag N of the scaling group. |
|Tag.N.Value|String|No|Finance|The value of tag N of the scaling group. |
|LaunchTemplateOverride.N.InstanceType|String|No|ecs.c5.xlarge|If you want to scale the scaling group based on the capacity, you must specify both the LaunchTemplateOverride.N.InstanceType and LaunchTemplateOverride.N.WeightedCapacity parameters at the same time.

This parameter specifies instance type N to override the instance types specified in the launch template. You can specify N values for this parameter and N instance types for the extended configurations. Valid values of N: 1 to 10.

**Note:** This parameter is valid only when the LaunchTemplateId parameter is specified.

Valid values of InstanceType: For information about available ECS instance types, see [Instance families](~~25378~~). |
|LaunchTemplateOverride.N.WeightedCapacity|Integer|No|4|If you want to scale the scaling group based on the capacity, you must specify LaunchTemplateOverride.N.WeightedCapacity after LaunchTemplateOverride.N.InstanceType is specified. The two parameters have a one-to-one correspondence between them. The N value must be the same.

This parameter specifies the weight of the instance type, which indicates the capacity of a single instance of the specified instance type in the scaling group. A greater weight indicates that a less number of instances of the specified instance type is required to meet the expected capacity.

The performance metrics such as the number of vCPUs and the memory size of each instance type may vary. You can configure different weights for different instance types to meet your requirements.

The following code provides an example:

-   Current capacity: 0
-   Expected capacity: 6
-   Capacity of ecs.c5.xlarge: 4

To meet the expected capacity, Auto Scaling creates two ecs.c5.xlarge instances.

**Note:** The capacity of the scaling group cannot exceed the sum of the maximum capacity \(MaxSize\) and the maximum weight of the instance type.

Valid values: 1 to 500. |

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

|The error message returned because the vSwitch is unavailable and ECS instances cannot be created. |
|400

|InvalidDBInstanceId. RegionMismatch

|DB instance "XXX" and the specified scaling group are not in the same Region.

|The error message returned because the specified ApsaraDB RDS instance and the specified scaling group are not in the same region. |
|400

|InvalidLoadBalancerId.IncorrectAddressType

|The current address type of specified load balancer does not support this action.

|The error message returned because the network type of the specified SLB instance does not match the network type of the vSwitch. |
|400

|InvalidLoadBalancerId.IncorrectInstanceNetworkType

|The network type of the instance in specified Load Balancer does not support this action.

|The error message returned because the network type of the ECS instance added to the backend server group of the specified SLB instance is different from that of the scaling group. |
|400

|InvalidLoadBalancerId.RegionMismatch

|The specified Load Balancer and the specified scaling group are not in the same Region.

|The error message returned because the specified SLB instance and the specified scaling group are not in the same region. |
|400

|InvalidLoadBalancerId.VPCMismatch

|The specified virtual switch and the instance in specified Load Balancer are not in the same VPC.

|The error message returned because the vSwitch and the ECS instance added to the backend server group of the SLB instance associated with the scaling group are not in the same VPC. |
|400

|InvalidParameter

|The specified value of parameter "ScalingPolicy" is not valid.

|The error message returned because the specified ScalingPolicy parameter is invalid. |
|400

|InvalidParameter.Conflict

|The value of parameter &lt;parameter name&gt; and parameter &lt;parameter name&gt; are conflict.

|The error message returned because the specified MinSize value is greater than the MaxSize value. |
|400

|InvalidScalingGroupName.Duplicate

|The specified value of parameter &lt;parameter name&gt; is duplicated.

|The error message returned because the specified ScalingGroupName parameter already exists. |
|400

|QuotaExceeded.DBInstanceSecurityIP

|Security IP quota exceeded in DB instance “XXX”.

|The error message returned because the maximum number of IP addresses in the whitelist of the specified ApsaraDB RDS instance has been reached. |
|400

|QuotaExceeded.PrivateIpAddress

|Private IP address quota exceeded in the specified virtual switch.

|The error message returned because no idle private IP addresses are available in the CIDR block of the vSwitch. |
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

|The error message returned because the specified vSwitch does not exist. |
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

|The error message returned because the fixed version number specified for the LaunchTemplateVersion parameter of the launch template contains non-digit characters. |

