# EnableScalingGroup

You can call this operation to enable a scaling group.

## Description

You can call this operation on a scaling group only when the scaling group is in the Enabled state.

When you enable a scaling group, you obtain one or more of the following results:

-   After a scaling group is enabled, the ECS instances that you specified by using the InstanceId.N parameter are added to the scaling group.
-   If the number of existing ECS instances in a scaling group is less than the MinSize value after the specified ECS instances are added to the scaling group, additional ECS instances are automatically created to maintain the MinSize value. For example, a scaling group is created with the MinSize parameter set to 5. Two existing ECS instances are specified in the InstanceId.N parameter when the scaling group is enabled. Then, three additional ECS instances are automatically created after the two ECS instances are added by Auto Scaling to the scaling group.
-   If the sum of the number of instances to be added specified for this operation and the number of existing ECS instances in the scaling group is greater than the MaxSize value, the call fails.

If the scaling group has no active scaling configuration, you must specify a scaling configuration when you enable the scaling group. This operation must meet the following requirements:

-   A single scaling group can have only one active scaling configuration.
-   If an active scaling configuration exists and you specify a new active scaling configuration when you call this operation, the original scaling configuration becomes inactive.

The ECS instances to be added to the scaling group must meet the following requirements:

-   The instances are located in the same region as the scaling group.
-   The instances have the same instance type as that of the active scaling configuration.
-   The instances are in the Running state.
-   The instances are not added to other scaling groups.
-   The instances use the subscription or pay-as-you-go billing method or are preemptible instances.
-   If the VSwitchId parameter is specified for a scaling group, ECS instances in the classic network or not in the same VPC as the specified vSwitch cannot be added to the scaling group.
-   If the VSwitchId parameter is not specified for a scaling group, VPC-type ECS instances cannot be added to the scaling group.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=EnableScalingGroup&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|EnableScalingGroup|The operation that you want to perform. Set the value to EnableScalingGroup. |
|ScalingGroupId|String|Yes|asg-bp14wlu85wrpchm0\*\*\*\*|The ID of the scaling group. |
|ActiveScalingConfigurationId|String|No|asc-bp1ffogfdauy0nu5\*\*\*\*|The ID of the scaling configuration to be enabled in the scaling group. |
|InstanceId.N|RepeatList|No|i-283vv\*\*\*\*|The ID of ECS instance N to be added to the scaling group. Valid values of N: 1 to 20. |
|LoadBalancerWeight.N|RepeatList|No|50|The weight of ECS instance N that acts as a backend server of the associated SLB instance. Valid values of N: 1 to 20. Valid values of this parameter: 1 to 100.

Default value: 50. |
|LaunchTemplateId|String|No|lt-m5e3ofjr1zn1aw7\*\*\*\*|The ID of the launch template that is used by Auto Scaling to create ECS instances. |
|LaunchTemplateVersion|String|No|Default|The version number of the launch template. Valid values:

-   A fixed template version number.
-   Default: The default template version is always used.
-   Latest: The latest template version is always used. |
|LaunchTemplateOverride.N.InstanceType|String|No|ecs.c5.xlarge|If you want to scale the scaling group based on the capacity, you must specify both the LaunchTemplateOverride.N.InstanceType and LaunchTemplateOverride.N.WeightedCapacity parameters at the same time.

This parameter specifies instance type N to override the instance types specified in the launch template. You can specify N values for this parameter and N instance types for the extended configurations. Valid values of N: 1 to 10.

**Note:** This parameter takes effect only when the LaunchTemplateId parameter is specified.

Valid values of InstanceType: For information about available ECS instance types, see [Instance families](~~25378~~). |
|LaunchTemplateOverride.N.WeightedCapacity|Integer|No|4|If you want to scale the scaling group based on the capacity, you must specify LaunchTemplateOverride.N.WeightedCapacity after LaunchTemplateOverride.N.InstanceType is specified. The two parameters have a one-to-one correspondence between them. The N value must be the same.

This parameter specifies the weight of the instance type, which indicates the capacity of a single instance of the specified instance type in the scaling group. A greater weight indicates that a less number of instances of the specified instance type is required to meet the expected capacity.

The performance metrics such as the number of vCPUs and the memory size of each instance type may vary. You can configure different weights for different instance types to meet your requirements.

Example:

-   Current capacity: 0
-   Expected capacity: 6
-   Capacity of ecs.c5.xlarge: 4

To meet the expected capacity, Auto Scaling creates two ecs.c5.xlarge instances.

**Note:** The capacity of the scaling group cannot exceed the sum of the maximum capacity \(MaxSize\) and the maximum weight of the instance type.

Valid values: 1 to 500. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=EnableScalingGroup
&ScalingGroupId=asg-bp1ffogfdauy0jw0****
&InstanceId.1=i-283vv****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<EnableScalingGroupResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</EnableScalingGroupResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist in the current account. |
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned because Auto Scaling is not authorized to call the specified operation. |
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|The error message returned because the specified scaling group is being deleted. |
|404

|InvalidScalingConfigurationId.NotFound

|The specified scaling configuration does not exist.

|The error message returned because the specified scaling configuration does not exist in the specified scaling group. |
|400

|InvalidScalingConfigurationId.InstanceTypeMismatch

|The specified scaling configuration and existing active scaling configuration have different instance type.

|The error message returned because the instance type of the specified scaling configuration is different from that of the active scaling configuration. |
|400

|MissingActiveScalingConfiguration

|An active scaling configuration for the specified scaling group is not supplied.

|The error message returned because no active scaling configuration is specified for the scaling group. |
|404

|InvalidInstanceId.NotFound

|Instance “XXX” does not exist.

|The error message returned because the specified ECS instance does not exist in the current account. |
|400

|InvalidInstanceId. RegionMismatch

|Instance “XXX” and the specified scaling group are not in the same Region.

|The error message returned because the specified ECS instance and the scaling group are not in the same region. |
|400

|InvalidInstanceId. InstanceTypeMismatch

|Instance "XXX" and existing active scaling configuration have different instance type.

|The error message returned because the instance type of the specified ECS instance is different from that of the active scaling configuration. |
|400

|IncorrectInstanceStatus

|The current status of instance "XXX" does not support this action.

|The error message returned because the specified ECS instance is not in the Running state. |
|400

|InvalidInstanceId. NetworkTypeMismatch

|The network type of instance “XXX” does not support this action.

|The error message returned because the network type of the specified ECS instance is different from that of the scaling group. |
|400

|InvalidInstanceId.VPCMismatch

|Instance "XXX" and the specified scaling group are not in the same VPC.

|The error message returned because the added ECS instance and the specified scaling group are not in the same VPC. |
|400

|InvalidInstanceId.InUse

|Instance "XXX" is already attached to another scaling group.

|The error message returned because the specified ECS instance is already added to another scaling group. |
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|The error message returned because the specified SLB instance is not in the Active state. |
|400

|IncorrectLoadBalancerHealthCheck

|The current health check type of specified load balancer does not support this action.

|The error message returned because health check is not enabled for the specified SLB instance. |
|400

|InvalidLoadBalancerId.IncorrectInstanceNetworkType

|The network type of the instance in specified Load Balancer does not support this action.

|The error message returned because the network type of the ECS instance added to the specified SLB instance is different from that of the scaling group. |
|400

|InvalidLoadBalancerId.VPCMismatch

|The specified virtual switch and the instance in specified Load Balancer are not in the same VPC.

|The error message returned because the ECS instance added to the specified SLB instance is not in the same VPC as the vSwitch specified by VSwitchID. |
|400

|IncorrectDBInstanceStatus

|The current status of DB instance “XXX” does not support this action.

|The error message returned because the specified ApsaraDB RDS instance is not in the Running state. |
|400

|IncorrectCapacity.MaxSize

|To attach the instances, the total capacity will be greater than the max size.

|The error message returned because the total number of ECS instances \(Total Capacity\) exceeds the specified value of MaxSize after instances are added to the specified scaling group. |
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

