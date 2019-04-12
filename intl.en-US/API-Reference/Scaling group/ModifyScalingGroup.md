# ModifyScalingGroup {#concept_25937_zh .concept}

This topic introduces how to modify a scaling group using the API.

## Description {#section_ld1_pv2_sfb .section}

-   Modifies the attributes of a scaling group. However, the following attributes cannot be modified:
    -   RegionId
    -   LoadBalancerId
    -   DBInstanceId
-   The interface can be called only when the scaling group is active or inactive.
-   When the scaling configuration specified for the scaling group needs to be modified, the instance type attribute of the modified scaling configuration must be consistent with that of the active scaling configuration.

    After a new scaling configuration is added to the scaling group, the running ECS instances which are created based on the previous scaling configuration remain unchanged.

-   When the number \(total capacity\) of ECS instances in the scaling group does not meet the modified MaxSize or MinSize specification, the Auto Scaling service automatically attaches or removes ECS instances to/from the group to make odds even.

## Request parameters { .section}

|Name|Type|Required|Description|
|----|----|--------|-----------|
|Action|String|Yes|Operation interface name, required parameter. Value: ModifyScalingGroup|
|ScalingGroupId|String|Yes|Scaling group ID|
|ScalingGroupName|String|No|Name shown for the scaling group, which must contain 2-40 characters \(English or Chinese\). The name must begin with a number, an upper/lower-case letter or a Chinese character and may contain numbers, “\_”, “-“ or “.”. The account name is unique in the same region.|
|ActiveScalingConfigurationId|String|No|ID of the active scaling configuration in the scaling group.|
|MinSize|Integer|No|Minimum number of ECS instances in the scaling group. Value range: \[0, 100\].|
|MaxSize|Integer|No|Maximum number of ECS instances in the scaling group. Value range: \[0, 100\].|
|DefaultCooldown|Integer|No|Default cool-down time \(in seconds\) of the scaling group. Value range: \[0, 86400\].|
|RemovalPolicy.N|String|No|Policy for removing ECS instances from the scaling group. Optional values: -   OldestInstance: removes the first ECS instance attached to the scaling group.
-   NewestInstance: removes the first ECS instance attached to the scaling group.
-   OldestScalingConfiguration: removes the ECS instance with the oldest scaling configuration.

 You can enter up to two removal policies.

 |
|LaunchTemplateId|String|No|ID of the launch template. For the specified scaling group to obtain startup configuration information from the launch template.|
|LaunchTemplateVersion|String|No|Version of the launch template. Optional values: -   Fixed template version number
-   Default: The default template version is always used.
-   Latest: The latest template version is always used.

 |
|VSwitchIds.N|String|No| -   VSwitchIds.N takes effect only when the network type of scaling group is VPC.
-   VSwitchIds.N can be used for specifying VSwitchs from multiple zones, and the value range of N is \[1, 5\]. When modifying the scaling group, you can specify up to 5 VSwitchs in the same VPC.
-   The VSwitchs and scaling group must belong to the same VPC.
-   The priorities of VSwitchs are determined by their numbers, and 1 has the highest priority.
-   When an instance cannot be created in the zone where the VSwitch with higher priority belong, the VSwitch with the lower priority will be selected.

 |

## Response parameters { .section}

Public parameters.

## Error codes { .section}

For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|Error message|Error code|Description|HTTP status code|
|:------------|:---------|:----------|:---------------|
|The specified scaling group does not exist in this account.|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|404|
|The scaling group name already exists.|InvalidScalingGroupName.Duplicate|The specified value of parameter `<parameter name>` is duplicated.|400|
|The specified scaling configuration does not exist in the scaling group.|InvalidScalingConfigurationId.NotFound|The specified scaling configuration does not exist.|404|
|The instance types of the specified scaling configuration and the active scaling configuration do not match.|InvalidScalingConfigurationId.InstanceTypeMismatch|The specified scaling configuration and existing active scaling configuration have different instance type.|400|
|The specified MinSize is greater than MaxSize.|InvalidParameter.Conflict|The value of parameter `<parameter name>` and parameter `<parameter name>` are confilict.|400|
|The specified launch template version does not exist.|LaunchTemplateVersionSet.NotFound|The specific version of launch template does not exist.|400|
|The specified lauch template does not exist.|LaunchTemplateSet.NotFound|The specified launch template set is not found.|400|
|The required parameter ImageId is not supplied.|TemplateMissingParameter.ImageId|The input parameter "ImageId" that is mandatory for processing this request is not supplied.|400|
|The required parameter InstanceTypes is not supplied.|TemplateMissingParameter.InstanceTypes|The input parameter "InstanceTypes" that is mandatory for processing this request is not supplied.|400|
|The required parameter SecurityGroup is not supplied.|TemplateMissingParameter.SecurityGroup|The input parameter "SecurityGroup" that is mandatory for processing this request is not supplied.|400|
|The input parameter LaunchTemplateVersion must be a number.|TemplateVersion.NotNumber|The input parameter "LaunchTemplateVersion" is supposed to be a string representing the version number.|400|

## Request example { .section}

```
http://ess.aliyuncs.com/?Action=ModifyScalingGroup
&ScalingGroupId=cqS5QbbhmvGLcJbWoDbWLj2V
&ScalingGroupName=ScalingGroup
&<Public Request Parameters>
```

## Response example { .section}

XML format:

```
< ModifyScalingGroupResponse>
    <RequestId>6469DCD0-13AC-487E-85A0-CE4922908FDE</RequestId>
</ ModifyScalingGroupResponse>
```

JSON format:

```
"RequestId": "6469DCD0-13AC-487E-85A0-CE4922908FDE"
```

