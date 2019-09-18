# ModifyScalingGroup {#doc_api_Ess_ModifyScalingGroup .reference}

You can call this operation to modify a scaling group.

## Description {#description .section}

-   The following parameters cannot be modified:
    -   RegionId
    -   LoadBalancerId

**Note:** If you want to attach or detach a Server Load Balancer \(SLB\) instance to or from the scaling group, call the [AttachLoadBalancers](~~85125~~) or [DetachLoadBalancers](~~85141~~) operation.

    -   DBInstanceId

**Note:** If you want to attach or detach an ApsaraDB for Relational Database Service \(RDS\) instance to or from the scaling group, call the [AttachDBInstances](~~85379~~) or [DetachDBInstances](~~85380~~) operation.

-   You can call this operation only when the scaling group is in the Active or Inactive state.
-   New scaling configurations do not affect running Elastic Compute Service \(ECS\) instances that are created based on the previous scaling configurations.
-   If you increase the value of the MaxSize parameter, and the number of ECS instances in the scaling group exceeds the new value, the scaling group automatically removes instances to ensure that the number of instances are within the modified range.
-   If you decrease the value of the MinSize parameter, and the number of ECS instances in the scaling group falls below the new value, the scaling group automatically adds instances to ensure that the number of instances are within the modified range.

## Debugging {#api_explorer .section}

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=Ess&api=ModifyScalingGroup&type=RPC&version=2014-08-28)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|ScalingGroupId|String|Yes|cqS5QbbhmvGLcJbWoDbW\*\*\*\*| The ID of the scaling group to be modified.

 |
|Action|String|No|ModifyScalingGroup| The operation that you want to perform. Set the value to ModifyScalingGroup.

 |
|ActiveScalingConfigurationId|String|No|bU5uZHcAgtzwcL4IeDea\*\*\*\*| The ID of the active scaling configuration in the scaling group.

 |
|DefaultCooldown|Integer|No|600| The cooldown period after a scaling activity \(adding or removing ECS instances\) is executed. Valid values: 0 to 86400. Unit: seconds.

 During the cooldown period calculated for a scaling activity, the scaling group does not execute any other scaling activities triggered by [CloudMonitor](~~35170~~) alarm tasks.

 |
|HealthCheckType|String|No|ECS| The health check mode of the scaling group. Valid values:

 -   NONE: The system performs no health check.
-   ECS: The system performs the health check on ECS instances in the scaling group.

 |
|LaunchTemplateId|String|No|lt-m5e3ofjr1zn1aw7\*\*\*\*| The ID of the instance launch template from which the scaling group obtains launch configurations.

 |
|LaunchTemplateVersion|String|No|Default| The version of the instance launch template. Valid values:

 -   A fixed template version.
-   Default: The default template version is always used.
-   Latest: The latest template version is always used.

 |
|MaxSize|Integer|No|99| The maximum number of ECS instances in the scaling group. Valid values: 0 to 1000. When the number of ECS instances in the scaling group exceeds the value of MaxSize, Auto Scaling removes the ECS instances from the scaling group until the number of instances is equal to the MaxSize value.

 |
|MinSize|Integer|No|1| The minimum number of ECS instances in the scaling group. Valid values: 0 to 1000. When the number of ECS instances in the scaling group is smaller than the value of MinSize, Auto Scaling automatically creates ECS instances until the number of instances is equal to the MinSize value.

 |
|OnDemandBaseCapacity|Integer|No|30| The minimum number of pay-as-you-go instances required in the scaling group. Valid values: 0 to 1000. When the number of pay-as-you-go instances is smaller than this value, the scaling group will attempt to create pay-as-you-go instances over other instances.

 |
|OnDemandPercentageAboveBaseCapacity|Integer|No|20| The percentage of pay-as-you-go instances to be created when instances are added to the scaling group. This parameter takes effect after the number of instances reaches the OnDemandBaseCapacity value. Valid values: 0 to 100.

 |
|RemovalPolicy.1|String|No|OldestScalingConfiguration| Specifies policy N for removing ECS instances from the scaling group. Valid values of N: 1 to 2. For more information, see [Removal policies](~~25910~~). Valid values:

 -   OldestInstance: removes the ECS instance that is added to the scaling group at the earliest point in time.
-   NewestInstance: removes the ECS instance that is added to the scaling group at the latest point in time.
-   OldestScalingConfiguration: removes the ECS instance that is created based on the earliest scaling configuration.

 |
|ScalingGroupName|String|No|Scaling\*\*\*\*| The name of the scaling group. The name of a scaling group must be unique in a region. The name must be 2 to 40 characters in length and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a letter or digit.

 |
|SpotInstancePools|Integer|No|5| The number of available instance types. The scaling group will create preemptible instances of multiple instance types available at the lowest cost. Valid values: 0 to 10.

 |
|SpotInstanceRemedy|Boolean|No|true| Specifies whether to supplement preemptible instances when the target capacity of preemptible instances is not fulfilled. When receiving a system message that a preemptible instance will be reclaimed, the scaling group will create a new instance to replace the instance to be reclaimed if this parameter is set to true.

 |
|VSwitchIds.N|RepeatList|No|vsw-\*\*\*\*| The IDs of one or more VSwitches. Valid values of N: 1 to 5.

 This parameter is only valid when the network type of the scaling group is VPC. The specified VSwitch and the scaling group must be in the same VPC.

 VSwitches can be from multiple zones. VSwitches are sorted in ascending order based on the value of N. Value 1 indicates the highest priority. When an ECS instance cannot be created in the zone where the VSwitch with the highest priority resides, the system automatically uses the VSwitch with the next highest priority to create the ECS instance.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}

http://ess.aliyuncs.com/?Action=ModifyScalingGroup
&ScalingGroupId=cqS5QbbhmvGLcJbWoDbW****
&ScalingGroupName=Scaling****
&<Common request parameters>

```

Sample success response

`XML` format

``` {#xml_return_success_demo}
<ModifyScalingGroupResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyScalingGroupResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes {#section_s1x_s9p_igw .section}

| HTTP status code

 | Error code

 | Error message

 | Description

 |
|--------------------|--------------|-----------------|---------------|
| 404

 | InvalidScalingGroupId.NotFound

 | The specified scaling group does not exist.

 | The error message returned because the specified scaling group does not exist in the current account.

 |
| 400

 | InvalidScalingGroupName.Duplicate

 | The specified value of parameter <parameter name\> is duplicated.

 | The error message returned because the specified scaling group name already exists.

 |
| 404

 | InvalidScalingConfigurationId.NotFound

 | The specified scaling configuration does not exist.

 | The error message returned because the specified scaling configuration does not exist in the scaling group.

 |
| 400

 | InvalidScalingConfigurationId.InstanceTypeMismatch

 | The specified scaling configuration and existing active scaling configuration have different instance type.

 | The error message returned because the instance type in the specified scaling configuration is different from that in the active scaling configuration.

 |
| 400

 | InvalidParameter.Conflict

 | The value of parameter <parameter name\> and parameter <parameter name\> are conflict.

 | The error message returned because the specified MinSize value is greater than the MaxSize value.

 |
| 400

 | LaunchTemplateVersionSet.NotFound

 | The specific version of launch template does not exist.

 | The error message returned because the specified instance launch template version does not exist.

 |
| 400

 | LaunchTemplateSet.NotFound

 | The specified launch template set is not found.

 | The error message returned because the specified instance launch template does not exist.

 |
| 400

 | TemplateMissingParameter.ImageId

 | The input parameter "ImageId" that is mandatory for processing this request is not supplied.

 | The error message returned because the ImageId parameter required for the specified instance launch template is not specified.

 |
| 400

 | TemplateMissingParameter.InstanceTypes

 | The input parameter "InstanceTypes" that is mandatory for processing this request is not supplied.

 | The error message returned because the InstanceTypes parameter required for the specified instance launch template is not specified.

 |
| 400

 | TemplateMissingParameter.SecurityGroup

 | The input parameter "SecurityGroup" that is mandatory for processing this request is not supplied.

 | The error message returned because the SecurityGroup parameter required for the specified instance launch template is not specified.

 |
| 400

 | TemplateVersion.NotNumber

 | The input parameter "LaunchTemplateVersion" is supposed to be a string representing the version number.

 | The error message returned because the specified LaunchTemplateVersion parameter of the specified instance launch template is not in digits.

 |

