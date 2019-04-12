# EnableScalingGroup {#concept_25939_zh .concept}

This topic introduces how to enable a scaling group using the API.

## Description {#section_gxd_1x2_sfb .section}

-   Enables the specified scaling group.
    -   After the scaling group is successfully enabled \(the group is active\), the ECS instances specified by the interface are attached to the group.
    -   If the current number of ECS instances in the scaling group is still smaller than MinSize after the ECS instances specified by the interface are attached, the Auto Scaling service automatically creates ECS instances in Pay-As-You-Go mode to make odds even. For example, a scaling group is created with MinSize = 5. Two existing ECS instances are specified by the InstanceId.N parameter when the scaling group is enabled. Three additional ECS instances are automatically created after the two ECS instances are attached by the Auto Scaling service to the scaling group.
-   The interface can be called only when the scaling group is inactive.
-   If the scaling group has no active scaling configurations, you need to input scaling configurations when enabling the scaling group.
    -   A single scaling group can have only one active scaling configuration at a time.
    -   If an active scaling configuration has been created before the scaling group is enabled, input of a new active scaling configuration through the interface makes the previous scaling configuration inactive.
-   Restrictions on attaching ECS instances:
    -   The attached ECS instance and the scaling group must be in the same region.
    -   The attached ECS instance and the instance with active scaling configurations must be of the same type.
    -   The attached ECS instance must in the **Running** state.
    -   The attached ECS instance has not been attached to other scaling groups.
    -   The attached ECS instance supports Subscription and Pay-As-You-Go payment methods.
    -   If the VswitchID is specified for a scaling group, you cannot attach Classic ECS instances or ECS instances on other VPCs to the scaling group.
    -   If the VswitchID is not specified for the scaling group, ECS instances of the VPC type cannot be attached to the scaling group.
-   The call fails if the number \(total capacity\) of instances specified by the interface plus instances in the scaling group is greater than MaxSize.

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|Operation interface name, required parameter; value: EnableScalingGroup|
|ScalingGroupId|String|Yes|Scaling group ID.|
|ActiveScalingConfigurationId|String|No|ID of the scaling configuration to be activated in a scaling group.|
|InstanceId.N|String|No|ID of the ECS instance to be attached to the scaling group after it is enabled. You can input up to 20 IDs.|
|LaunchTemplateId|String|No|ID of the launch template. For the specified scaling group to obtain the startup configuration information from the template.|
|LaunchTemplateVersion|String|No|Version of the launch template. Optional values:-   Fixed template version number
-   Default: The default template version is always used.
-   Latest: The latest template version is always used.

|

## Response parameters { .section}

Public parameters.

## Error codes { .section}

For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|Error message|Error code|Description|HTTP status code|
|:------------|:---------|:----------|:---------------|
|The specified scaling group does not exist in this account.|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|404|
|API is not fully authorized to the Auto Scaling service.|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|403|
|The specified scaling group is in the deleting state.|IncorrectScalingGroupStatus|The current status of the specified scaling group does not support this action.|400|
|The specified scaling configuration does not exist in the scaling group.|InvalidScalingConfigurationId.NotFound|The specified scaling configuration does not exist.|404|
|The instance types of the specified scaling configuration and the active scaling configuration do not match.|InvalidScalingConfigurationId.InstanceTypeMismatch|The specified scaling configuration and existing active scaling configuration have different instance type.|400|
|No active scaling configuration is specified for the scaling group.|MissingActiveScalingConfiguration|An active scaling configuration for the specified scaling group is not supplied.|400|
|The specified ECS instance does not exist in this account.|InvalidInstanceId.NotFound|Instance “XXX” does not exist.|404|
|The specified ECS instance and the scaling group are not in the same region.|InvalidInstanceId. RegionMismatch|Instance “XXX” and the specified scaling group are not in the same Region.|400|
|The instance types of the specified ECS instance and the scaling configuration do not match.|InvalidInstanceId. InstanceTypeMismatch|Instance “XXX” and existing active scaling configuration have different instance type.|400|
|The specified ECS instance is not in the Running status.|IncorrectInstanceStatus|The current status of instance “XXX” does not support this action.|400|
|The network types of the specified ECS instance and the scaling configuration do not match.|InvalidInstanceId. NetworkTypeMismatch|The network type of instance “XXX” does not support this action.|400|
|The specified scaling group and the attached ECS instance are not in the same VPC.|InvalidInstanceId.VPCMismatch|Instance “XXX” and the specified scaling group are not in the same VPC.|400|
|The specified ECS instance has been attached to another scaling group.|InvalidInstanceId.InUse|Instance "XXX" is already attached to another scaling group.|400|
|The specified Server Load Balancer instance is not active.|IncorrectLoadBalancerStatus|The current status of the specified load balancer does not support this action.|400|
|Health check is not enabled for the specified Server Load Balancer instance.|IncorrectLoadBalancerHealthCheck|The current health check type of specified load balancer does not support this action.|400|
|The network type of the ECS instance contained in the specified Server Load Balancer is different from the network type of the scaling group.|InvalidLoadBalancerId.IncorrectInstanceNetworkType|The network type of the instance in specified Load Balancer does not support this action.|400|
|The ECS instance contained in the specified Server Load Balancer and VSwitchId are not in the same VPC.|InvalidLoadBalancerId.VPCMismatch|The specified virtual switch and the instance in specified Load Balancer are not in the same VPC.|400|
|The specified RDS instance is not running.|IncorrectDBInstanceStatus|The current status of DB instance “XXX” does not support this action.|400|
|Total Capacity after the ECS instance is attached is greater than MaxSize.|IncorrectCapacity.MaxSize|To attach the instances, the total capacity will be greater than the max size.|400|
|The specified version of the launch template does not exist.|LaunchTemplateVersionSet.NotFound|The specific version of launch template does not exist.|400|
|The specified launch template does not exist.|LaunchTemplateSet.NotFound|The specified launch template set is not found.|400|
|The required parameter ImageId is not supplied.|TemplateMissingParameter.ImageId|The input parameter "ImageId" that is mandatory for processing this request is not supplied.|400|
|The required parameter InstanceTypes is not supplied.|TemplateMissingParameter.InstanceTypes|The input parameter "InstanceTypes" that is mandatory for processing this request is not supplied.|400|
|The required parameter SecurityGroup is not supplied.|TemplateMissingParameter.SecurityGroup|The input parameter "SecurityGroup" that is mandatory for processing this request is not supplied.|400|
|The fixed version number of the specified launch template must be numbers.|TemplateVersion.NotNumber|The input parameter "LaunchTemplateVersion" is supposed to be a string representing the version number.|400|

## Request example { .section}

```
http://ess.aliyuncs.com/?Action=EnableScalingGroup 
&ScalingGroupId=dmIDKNcyWfzncX9MWX1bwFV
&InstanceId. 1=i-283vvyytn
&<Public Request Parameters>
```

## Response example { .section}

XML format:

```
< EnableScalingGroupResponse>
    <RequestId>6469DCD0-13AC-487E-85A0-CE4922908FDE</RequestId>
</ EnableScalingGroupResponse>
```

JSON format:

```
{
    "RequestId": "6469DCD0-13AC-487E-85A0-CE4922908FDE"
}
```

