# ModifyScalingGroup

You can call this operation to modify a scaling group.

## Description

-   The following parameters cannot be modified:
    -   RegionId
    -   LoadBalancerId

**Note:** If you want to add a Server Load Balancer \(SLB\) instance to a scaling group, call the [AttachLoadBalancers](~~85125~~) operation. If you want to remove a SLB instance from a scaling group, call the [DetachLoadBalancers](~~85141~~) operation.

    -   DBInstanceId

**Note:** If you want to add an ApsaraDB RDS instance to a scaling group, call the [AttachDBInstances](~~85379~~) operation. If you want to remove an ApsaraDB RDS instance from a scaling group, call the [DetachDBInstances](~~85380~~) operation.

-   You can call this operation only when a scaling group is in the Active or Inactive state.
-   New scaling configurations do not affect running Elastic Compute Service \(ECS\) instances that are created based on the previous scaling configurations.
-   If you modify the MaxSize parameter to a value that is less than the number of existing ECS instances in the scaling group, Auto Scaling automatically removes instances from the scaling group to ensure that the number of instances are within the modified range.
-   If you modify the MinSize parameter to a value that is greater than the number of existing ECS instances in the scaling group, Auto Scaling automatically adds instances to the scaling group to ensure that the number of instances are within the modified range.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=ModifyScalingGroup&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyScalingGroup|The operation that you want to perform. Set the value to ModifyScalingGroup. |
|ScalingGroupId|String|Yes|asg-bp1ffogfdauy0jw0\*\*\*\*|The ID of the scaling group to be modified. |
|ScalingGroupName|String|No|scalinggroup\*\*\*\*|The name of the scaling group. The name of a scaling group must be unique in a region. The name must be 2 to 64 characters in length and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a letter or a digit. |
|MinSize|Integer|No|1|The minimum number of ECS instances in the scaling group. When the number of ECS instances in the scaling group is less than the value of MinSize, Auto Scaling automatically creates ECS instances until the number of instances is equal to the value of MinSize.

 **Note:** The value of MinSize must be less than or equal to that of MaxSize. |
|MaxSize|Integer|No|99|The maximum number of ECS instances in the scaling group. When the number of ECS instances in the scaling group is greater than the value of MaxSize, Auto Scaling automatically removes ECS instances until the number of instances is equal to the value of MaxSize.

 The value range of MaxSize is based on your usage of Auto Scaling. For more information, check the quota value that corresponds to **Instances That Can Be Configured for a Scaling Group** in [Quota Center](https://quotas.console.aliyun.com/products/ess/quotas).

 For example, if the quota value that corresponds to **Instances That Can Be Configured for a Scaling Group** is 2000, the value range of MaxSize is 0 to 2000. |
|VSwitchIds.N|RepeatList|No|vsw-bp1oo2a7isyrb8igf\*\*\*\*|The ID of VSwitch N. Valid values of N: 1 to 5.

 This parameter is valid only when the network type of the scaling group is VPC. The specified VSwitch and the scaling group must be in the same VPC.

 VSwitches can reside in different zones. VSwitches are sorted in ascending order based on the value of N. A value of 1 indicates the highest priority. When an ECS instance cannot be created in the zone where the VSwitch with the highest priority resides, the system uses the VSwitch with the next highest priority to create the ECS instance. |
|DefaultCooldown|Integer|No|600|The cooldown period after a scaling activity is executed. Scaling activities include addition and removal of ECS instances. Valid values: 0 to 86400. Unit: seconds.

 During the cooldown period, Auto Scaling executes only scaling activities that are triggered by Cloud Monitor event-triggered tasks. |
|RemovalPolicy.1|String|No|OldestScalingConfiguration|Policy N for removing ECS instances from the scaling group. Valid values of N: 1 to 2. Valid values:

 -   OldestInstance: removes the ECS instance that is added to the scaling group at the earliest point in time.
-   NewestInstance: removes the ECS instance that is added to the scaling group at the latest point in time.
-   OldestScalingConfiguration: removes the ECS instances that are created based on the earliest scaling configuration. |
|ActiveScalingConfigurationId|String|No|asc-bp17pelvl720x5ub\*\*\*\*|The ID of the active scaling configuration in the scaling group. |
|HealthCheckType|String|No|ECS|The health check mode of the scaling group. Valid values:

 -   NONE: The system performs no health check.
-   ECS: The system performs a health check on ECS instances in the scaling group. |
|LaunchTemplateId|String|No|lt-m5e3ofjr1zn1aw7\*\*\*\*|The ID of the launch template, from which Auto Scaling can obtain launch configurations. |
|LaunchTemplateVersion|String|No|Default|The version number of the launch template. Valid values:

 -   A fixed template version number.
-   Default: The default template version is always used.
-   Latest: The latest template version is always used. |
|OnDemandBaseCapacity|Integer|No|30|The minimum number of pay-as-you-go instances required in the scaling group. Valid values: 0 to 1000. When the number of pay-as-you-go instances is less than this value, Auto Scaling will preferentially create pay-as-you-go instances. |
|OnDemandPercentageAboveBaseCapacity|Integer|No|20|The percentage of pay-as-you-go instances to be created when instances are added to the scaling group. This parameter takes effect after the number of pay-as-you-go instances in the scaling group reaches the value of OnDemandBaseCapacity. Valid values: 0 to 100. |
|SpotInstanceRemedy|Boolean|No|true|Specifies whether to supplement preemptible instances when the target capacity of preemptible instances is not fulfilled. When Auto Scaling receives a system message that a preemptible instance will be reclaimed, Auto Scaling will create a new instance to replace the instance to be reclaimed if this parameter is set to true. |
|CompensateWithOnDemand|Boolean|No|true|Specifies whether to automatically create pay-as-you-go instances to meet the requirement for the number of ECS instances in the scaling group when the number of preemptible instances cannot be reached due to reasons such as cost or insufficient resources. This parameter takes effect when the MultiAZPolicy parameter of the CreateScalingGroup operation is set to COST\_OPTIMIZED. Valid values:

 -   true: Pay-as -you-go instances can be created.
-   false: Pay-as -you-go instances cannot be created. |
|SpotInstancePools|Integer|No|5|The number of available instance types. Auto Scaling will create preemptible instances of multiple instance types available at the lowest cost. Valid values: 0 to 10. |
|DesiredCapacity|Integer|No|5|The expected number of ECS instances in the scaling group. Auto Scaling automatically keeps the ECS instances at this number. The expected number must be between the value of MaxSize and the value of MinSize. |
|GroupDeletionProtection|Boolean|No|true|Specifies whether to enable scaling group deletion protection. Valid values:

 -   true: Scaling group deletion protection is enabled. You cannot delete the scaling group.
-   false: Scaling group deletion protection is disabled. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=ModifyScalingGroup
&ScalingGroupId=asg-bp1ffogfdauy0jw0****
&ScalingGroupName=Scaling****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyScalingGroupResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyScalingGroupResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HttpCode

|Error code

|Error message

|Description |
|----------|------------|---------------|-------------|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist in the current account. |
|400

|InvalidScalingGroupName.Duplicate

|The specified value of parameter &lt;parameter name&gt; is duplicated.

|The error message returned because the specified scaling group name already exists. |
|404

|InvalidScalingConfigurationId.NotFound

|The specified scaling configuration does not exist.

|The error message returned because the specified scaling configuration does not exist in the scaling group. |
|400

|InvalidScalingConfigurationId.InstanceTypeMismatch

|The specified scaling configuration and existing active scaling configuration have different instance type.

|The error message returned because the instance type in the specified scaling configuration is different from that in the active scaling configuration. |
|400

|InvalidParameter.Conflict

|The value of parameter &lt;parameter name&gt; and parameter &lt;parameter name&gt; are confilict.

|The error message returned because the specified MinSize value is greater than the MaxSize value. |
|400

|LaunchTemplateVersionSet.NotFound

|The specific version of launch template is not exist.

|The error message returned because the specified launch template version does not exist. |
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

|The error message returned because the specified LaunchTemplateVersion parameter of the specified launch template contains non-digit characters. |

