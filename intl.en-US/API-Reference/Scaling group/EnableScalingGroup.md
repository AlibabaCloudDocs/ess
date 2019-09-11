# EnableScalingGroup {#doc_api_Ess_EnableScalingGroup .reference}

You can call this operation to enable a scaling group.

## Description {#description .section}

You can call this operation to enable a specified scaling group.

-   If the operation is successful, the scaling group becomes active and the specified ECS instances are added to the scaling group.
-   If the number of ECS instances in the scaling group is smaller than the MinSize value after the ECS instances are added, additional ECS instances are automatically created to achieve the MinSize value. For example, a scaling group is created with the MinSize parameter set to 5. Two existing ECS instances are specified in the InstanceId.N parameter when the scaling group is enabled. Then, three additional ECS instances are automatically created after the two ECS instances are added by Auto Scaling to the scaling group.

    The operation can only be called when the scaling group is inactive.


If the scaling group has no active scaling configuration, you must specify a scaling configuration when enabling the scaling group.

-   A single scaling group can only have one active scaling configuration at a time.
-   If an active scaling configuration has been created before the scaling group is enabled, this configuration will become inactive after you specify a new active scaling configuration by calling the operation.

    The restrictions on ECS instances to be manually added are as follows:

-   The ECS instances and the scaling group must be in the same region.
-   The ECS instances must have the same instance type as the active scaling configuration.
-   The ECS instances must be running.
-   The ECS instances have not been added to any scaling group.
-   The ECS instances support subscription and pay-as-you-go billing methods.
-   If the VSwitchId parameter is specified for a scaling group, ECS instances that belong to a classic network or in different VPCs cannot be added to the scaling group.
-   If the VSwitchId parameter is not specified for a scaling group, ECS instances that belong to a VPC cannot be added to the scaling group.

    If the sum of the number of instances to be added specified by this operation and the number of ECS instances currently in the scaling group is greater than the MaxSize value, the call fails.


## Debugging {#api_explorer .section}

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=EnableScalingGroup&type=RPC&version=2014-08-28)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|ScalingGroupId|String|Yes|dmIDKNcyWfzncX9MWX1\*\*\*\*|The ID of the scaling group.

 |
|Action|String|No|EnableScalingGroup|The operation that you want to perform. Set the value to EnableScalingGroup.

 |
|ActiveScalingConfigurationId|String|No|cGsGHrdMBa3DcDrrBVcc\*\*\*\*|The ID of the scaling configuration to be activated in the scaling group.

 |
|InstanceId.1|String|No|i-283vv\*\*\*\*|The ID of enabled ECS instance N to be added to the scaling group. Valid values of N: 1 to 20.

 |
|LaunchTemplateId|String|No|lt-m5e3ofjr1zn1aw7\*\*\*\*|The ID of the instance launch template, from which the specified scaling group can obtain launch configurations.

 |
|LaunchTemplateVersion|String|No|Default|The version number of the instance launch template. Valid values:

 -   A fixed template version number.
-   Default: always uses the default template version.
-   Latest: always uses the latest template version.

 |
|LoadBalancerWeight.1|Integer|No|50|The weight of ECS backend server N. Valid values of N: 1 to 20. Valid values for this parameter: 0 to 100.

 Default value: 50.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=EnableScalingGroup
&ScalingGroupId=dmIDKNcyWfzncX9MWX1****
&InstanceId.1=i-283vv****
&<Common request parameters>

```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
< EnableScalingGroupResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ EnableScalingGroupResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes { .section}

|HTTP status code

|Error code

|Error message

|Description

|
|------------------|------------|---------------|-------------|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist in the current account.

|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned because Auto Scaling is not authorized to call the specified operation.

|
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|The error message returned because the specified scaling group is currently being deleted.

|
|404

|InvalidScalingConfigurationId.NotFound

|The specified scaling configuration does not exist.

|The error message returned because the specified scaling configuration does not exist in the specified scaling group.

|
|400

|InvalidScalingConfigurationId.InstanceTypeMismatch

|The specified scaling configuration and existing active scaling configuration have different instance type.

|The error message returned because the instance type of the specified scaling configuration is different from that of the active scaling configuration.

|
|400

|MissingActiveScalingConfiguration

|An active scaling configuration for the specified scaling group is not supplied.

|The error message returned because no active scaling configuration is specified for the scaling group.

|
|404

|InvalidInstanceId.NotFound

|Instance "XXX" does not exist.

|The error message returned because the specified ECS instance does not exist in the current account.

|
|400

|InvalidInstanceId. RegionMismatch

|Instance "XXX" and the specified scaling group are not in the same Region.

|The error message returned because the specified ECS instance and the scaling group are not in the same region.

|
|400

|InvalidInstanceId. InstanceTypeMismatch

|Instance "XXX" and existing active scaling configuration have different instance type.

|The error message returned because the type of the specified ECS instance is different from that of the active scaling configuration.

|
|400

|IncorrectInstanceStatus

|The current status of instance "XXX" does not support this action.

|The error message returned because the specified ECS instance is not running.

|
|400

|InvalidInstanceId. NetworkTypeMismatch

|The network type of instance "XXX" does not support this action.

|The error message returned because the network type of the specified ECS instance is different from that of the scaling group.

|
|400

|InvalidInstanceId.VPCMismatch

|Instance "XXX" and the specified scaling group are not in the same VPC.

|The error message returned because the added ECS instance and the specified scaling group are not in the same VPC.

|
|400

|InvalidInstanceId.InUse

|Instance "XXX" is already attached to another scaling group.

|The error message returned because the specified ECS instance is already added to another scaling group.

|
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|The error message returned because the specified SLB instance is not active.

|
|400

|IncorrectLoadBalancerHealthCheck

|The current health check type of specified load balancer does not support this action.

|The error message returned because health check is not enabled for the specified SLB instance.

|
|400

|InvalidLoadBalancerId.IncorrectInstanceNetworkType

|The network type of the instance in specified load balancer does not support this action.

|The error message returned because the network type of the ECS instance attached to the specified SLB instance is different from that of the scaling group.

|
|400

|InvalidLoadBalancerId.VPCMismatch

|The specified virtual switch and the instance in specified Load Balancer are not in the same VPC.

|The error message returned because the ECS instance attached to the specified SLB instance is not in the same VPC as the VSwitch specified by VSwitchID.

|
|400

|IncorrectDBInstanceStatus

|The current status of DB instance "XXX" does not support this action.

|The error message returned because the specified RDS instance is not running.

|
|400

|IncorrectCapacity.MaxSize

|To attach the instances, the total capacity will be greater than the max size.

|The error message returned because the total number of ECS instances \(Total Capacity\) exceeds the specified value of MaxSize after instances are added to the specified scaling group.

|
|400

|LaunchTemplateVersionSet.NotFound

|The specific version of launch template is not exist.

|The error message returned because the specified version of the instance launch template does not exist.

|
|400

|LaunchTemplateSet.NotFound

|The specified launch template set is not found.

|The error message returned because the specified instance launch template does not exist.

|
|400

|TemplateMissingParameter.ImageId

|The input parameter "ImageId" that is mandatory for processing this request is not supplied.

|The error message returned because the ImageId parameter required for the specified instance launch template is not specified.

|
|400

|TemplateMissingParameter.InstanceTypes

|The input parameter "InstanceTypes" that is mandatory for processing this request is not supplied.

|The error message returned because the InstanceTypes parameter required for the specified instance launch template is not specified.

|
|400

|TemplateMissingParameter.SecurityGroup

|The input parameter "SecurityGroup" that is mandatory for processing this request is not supplied.

|The error message returned because the SecurityGroup parameter required for the specified instance launch template is not specified.

|
|400

|TemplateVersion.NotNumber

|The input parameter "LaunchTemplateVersion" is supposed to be a string representing the version number.

|The error message returned because the specified LaunchTemplateVersion parameter of the specified launch template is not in digits.

|

