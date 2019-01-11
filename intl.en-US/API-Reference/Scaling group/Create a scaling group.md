# Create a scaling group {#concept_25936_zh .concept}

Creates a scaling group \(CreateScalingGroup\). A scaling group is a collection of ECS instances with the same application scenarios. It defines the maximum and minimum numbers of ECS instances in the group, and their associated Server Load Balancer instances, RDS instances, and other attributes.

-   The scaling group, Server Load Balancer instance, and RDS instance must be in the same region. For more information, see [regions and zones](../../../../../reseller.en-US/General Reference/Regions and zones.md#).

-   You can create up to 20 scaling groups.

-   The scaling group does not take effect immediately after being created. It must be enabled \(`EnableScalingGroup`\) to support scaling rule trigger and perform scaling activities.

-   If a Server Load Balancer instance is specified in the scaling group, notice that:

    -   The Server Load Balancer instance must be in the **Active** \(**active**\) status.
    -   The scaling group automatically attaches its ECS instances to the Server Load Balancer instance.
    -   Health check must be enabled for all listener ports configured for the Server Load Balancer instance; otherwise, creation fails.
    -   The default weight of an ECS instance attached to the Server Load Balancer instance is 50.
-   If an RDS instance is specified in the scaling group, notice that:

    -   The specified RDS instance must be in the **Running** \(**running**\) status.
    -   the scaling group automatically attaches the intranet IP addresses of its ECS instances to the RDS access whitelist.
    -   The number of IPs in the RDS instance whitelist cannot exceed the upper limit. For more information, see [whitelist](../../../../../reseller.en-US/User Guide/Security/Set a whitelist.md#) in *RDS*.

## Request parameters {#section_lt4_vd2_sfb .section}

|Name|Type|Required|Description|
|----|----|--------|-----------|
|Action|String|Yes|Operation interface name, required parameter. Value: CreateScalingGroup|
|RegionId|String|Yes|ID of the region where a scaling group is located. For more information, see [regions and zones](../../../../../reseller.en-US/General Reference/Regions and zones.md#).|
|MaxSize|Integer|Yes|Maximum number of ECS instances in the scaling group. Value range: \[0, 100\]. If the number ECS instances in the scaling group exceeds the MaxSize, Auto Scaling automatically removes the ECS instances.|
|MinSize|Integer|Yes|Minimum number of ECS instances in the scaling group. Value range: \[0, 100\]. If the number ECS instances in the scaling group is less than the MinSize, Auto Scaling automatically creates ECS instances.|
|Scalinggroupname|String|No| Name shown for the scaling group, which must contain 2-40 characters \(English or Chinese\). The name must begin with a number, an upper/lower-case letter or a Chinese character and may contain numbers, “\_“, “-“ or “.”. The account name is unique in the same region.

 If this parameter is not specified, the default value is ScalingGroupId.

 |
|DefaultCooldown|Integer|No| Default cool-down time \(in seconds\) of the scaling group. Value range: \[0, 86400\].

 The default value is 300s.

 During the cool-down time, this scaling group cannot perform any new scaling activities. Currently, this only applies to scaling activities triggered by [CloudMonitor](../../../../../reseller.en-US/Product Introduction/What is CloudMonitor.md#) alarm tasks.

 |
|RemovalPolicy.N|String|No| Policy for removing ECS instances from the scaling group. For more information, see [removal policy](../../../../../reseller.en-US/User Guide/Scaling groups/Realize Auto Scaling/Removal policies.md#). Value range of N: \[1,2\] Optional values:

 -   OldestInstance: removes the first ECS instance attached to the scaling group.
-   NewestInstance: removes the first ECS instance attached to the scaling group.
-   OldestScalingConfiguration: removes the ECS instance with the oldest scaling configuration.

 Default values: OldestScalingConfiguration and OldestInstance. You can enter up to two removal policies.

 |
|LoadBalancerIds|String|No|ID list of Server Load Balancer instances. A Json Array with format: \[ “lb-id0”, “lb-id1”, … “lb-idz” \], support up to 5 Load Balancer instance.|
|VServerGroup.N.LoadBalancerId|String|No|The ID of Server Load Balancer instance that a VServer Group belongs to.|
|VServerGroup.N.VServerGroupAttribute.M.VServerGroupId|String|No|The ID of VServer Group.|
|VServerGroup.N.VServerGroupAttribute.M.Port|Integer|No|The port number used to attach an ECS instance to the VServer Group. Value range: 1-65535.|
|VServerGroup.N.VServerGroupAttribute.M.Weight|Integer|No|The weight of an ECS instance that is attached to the VServer Group. Value range: 0-100.Default value: 50.

|
|DBInstanceIds|String|No|ID list of an RDS instance. A Json Array with format: \[ “rm-id0”, “rm-id1”, … “rm-idz” \], support up to 8 RDS instance.|
|VSwitchId|String|No|If you create a VPC scaling group, you must specify the ID of a VSwitch.|
|VSwitchIds.N|String|No| Parameter VSwitchIds.N is used to create instance in multiple zones. Parameter VSwitchIds.N has a priority over parameter VSwitchId. The valid range of N is \[1, 5\], and you can specify at most 5 VSwitches in a VPC. If you use the VSwitchIds.N parameter, the parameter VSwitchId is ignored.

 -   VSwitches can be from multiple zones.
-   The priority of VSwitches descends from 1 to 5, and 1 indicates the highest priority. When the VSwitch with the highest priority cannot create an ECS instance in its zone, the system automatically uses the VSwitch with the next highest priority to create the ECS instance.

 |
|ScalingPolicy|String|No|Specify the reclaim mode of scaling group. Optional values:-   recycle: Shutdown and Reclaim mode
-   release: Release mode

For more information about instance status, see [RemoveInstances](reseller.en-US/API-Reference/Trigger task/Remove an ECS instance.md#).

|
|MultiAZPolicy|String|No| The ECS instance scale up/down policy for a multi-zone scaling group. Optional values:

 -   PRIORITY: Scale up/down according to the user-defined VSwitches \(VSwitchIds.N\). When the VSwitch with the highest priority cannot create an ECS instance in its zone, the system automatically uses the VSwitch with the next highest priority to create the ECS instance.
-   BALANCE: ECS instances are allocated evenly to the multiple zones specified in the scaling group. If instances are not balanced among the zones due to an inventory shortage or other cause, you can re-balance the resources by calling the RebalanceInstance API.

 Default value: PRIORITY

 |
|LaunchTemplateId|String|No|ID of the launch template. For the specified scaling group to obtain the startup configuration information from the template.|
|LaunchTemplateVersion|String|No|Version of the launch template. Optional values:-   Fixed template version number
-   Default: The default template version is always used.
-   Latest: The latest template version is always used.

|

## Response parameters {#section_zt4_vd2_sfb .section}

|Name|Type|Description|
|----|----|-----------|
|ScalingGroupId|String|ID of a scaling group, generated by the system and globally unique.|

## Examples {#section_b54_vd2_sfb .section}

**Request example**

```language-shell
http://ess.aliyuncs.com/?Action=CreateScalingGroup
&RegionId=cn-qingdao
&MaxSize=20
&MinSize=2
&LoadBalancerId=147b46d767c-cn-qingdao-cm5-a01
&DBInstanceId. 1=rdszzzyyunybaeu
&DBInstanceId. 2=rdsia3u3yia3u3y
&<Public Request Parameters>

```

**Response example**

XML format:

```language-xml
<CreateScalingGroupResponse>
    <ScalingGroupId>dP8VqSd9ENXPc0ciVmbcrBT1</ScalingGroupId>
    <RequestId>536E9CAD-DB30-4647-AC87-AA5CC38C5382</RequestId>
</CreateScalingGroupResponse>

```

JSON format:

```language-json
{
	"RequestId": "536E9CAD-DB30-4647-AC87-AA5CC38C5382",
	"ScalingGroupId": "dP8VqSd9ENXPc0ciVmbcrBT1"
}


```

## Error codes {#section_f54_vd2_sfb .section}

Error codes specific to the CreateScalingGroup API are as follows. For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

 

|Error code|Error message|HTTP status code|Description|
|----------|-------------|----------------|-----------|
|IncorrectDBInstanceStatus|The current status of DB instance “XXX” does not support this action.|400|The specified RDS instance is not in the **Running** status.|
|IncorrectLoadBalancerHealthCheck|The current health check type of specified load balancer does not support this action.|400|Health check is not enabled for the specified Server Load Balancer instance.|
|IncorrectLoadBalancerStatus|The current status of the specified load balancer does not support this action.|400|The specified Server Load Balancer instance is not active.|
|IncorrectVSwitchStatus|The current status of virtual switch does not support this operation.|400|The VSwitch is unavailable and instances cannot be created.|
|InvalidDBInstanceId. RegionMismatch|DB instance “XXX” and the specified scaling group are not in the same Region.|400|The specified RDS instance must be in the same region as the scaling group.|
|InvalidLoadBalancerId.IncorrectAddressType|The current address type of specified load balancer does not support this action.|400|The Server Load Balancer instance is a private network instance, but a VSwitch has been specified. For more information, see [Server Load Balancer instances](../../../../../reseller.en-US/Product Introduction/What is Server Load Balancer?.md#).|
|InvalidLoadBalancerId.IncorrectInstanceNetworkType|The network type of the instance in specified Load Balancer does not support this action.|400|The network type of the ECS instance contained in the specified Server Load Balancer is different from the network type of the scaling group.|
|InvalidLoadBalancerId.RegionMismatch|The specified Load Balancer and the specified scaling group are not in the same Region.|400|The specified RDS instance and scaling group are not in the same region.|
|InvalidLoadBalancerId.VPCMismatch|The specified virtual switch and the instance in specified Load Balancer are not in the same VPC.|400|The ECS instance contained in the specified Server Load Balancer and VSwitchId are not in the same VPC.|
|InvalidParameter|The specified value of parameter "ScalingPolicy" is not valid.|400|The specified reclaim mode does not exist.|
|InvalidParameter.Conflict|The value of parameter <parameter name" and parameter <parameter name" are conflict.|400|The specified MinSize is greater than MaxSize.|
|InvalidScalingGroupName.Duplicate|The specified value of parameter <parameter name" is duplicated.|400|The scaling group name already exists.|
|QuotaExceeded.DBInstanceSecurityIP|Security IP quota exceeded in DB instance “XXX”.|400|The number of IP addresses in the access whitelist of the specified RDS instance exceeds the upper limit.|
|QuotaExceeded.PrivateIpAddress|Private IP address quota exceeded in the specified virtual switch.|400|The private IP address quota of the VSwitch is exceeded.|
|QuotaExceeded.ScalingGroup|Scaling group quota exceeded.|400|The scaling group quota is exceeded.|
|QuotaExceeded.VPCInstance|Instance quota exceeded in the specified VPC.|400|The instance quota of the VPC is exceeded.|
|InvalidDBInstanceId.NotFound|DB instance “XXX” does not exist.|404|The specified RDS instance does not exist.|
|InvalidLoadBalancerId.NotFound|The specified Load Balancer does not exist.|404|The specified Server Load Balancer instance does not exist.|
|InvalidRegionId.NotFound|The specified region does not exist.|404|The specified RegionId does not exist.|
|InvalidVSwitchId.NotFound|The specified virtual switch does not exist.|404|The specified VSwitch does not exist.|
|LaunchTemplateVersionSet.NotFound|The specific version of launch template is not exist.|400|The specified version of the launch template does not exist.|
|LaunchTemplateSet.NotFound|The specified launch template set is not found.|400|The specified launch template does not exist.|
|TemplateMissingParameter.ImageId|The input parameter "ImageId" that is mandatory for processing this request is not supplied.|400|The required parameter ImageId is not supplied.|
|TemplateMissingParameter.InstanceTypes|The input parameter "InstanceTypes" that is mandatory for processing this request is not supplied.|400|The required parameter InstanceType is not supplied.|
|TemplateMissingParameter.SecurityGroup|The input parameter "SecurityGroup" that is mandatory for processing this request is not supplied.|400|The required parameter SecurityGroup is not supplied.|
|TemplateVersion.NotNumber|The input parameter "LaunchTemplateVersion" is supposed to be a string representing the version number.|400|The fixed version number of the specified launch template must be numbers.|

