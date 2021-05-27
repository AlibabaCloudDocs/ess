# ModifyScalingConfiguration

Modifies a scaling configuration.

## Description

If you are modifying the name of a scaling configuration in a scaling group, make sure that the new name is unique within the scaling group.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=ModifyScalingConfiguration&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyScalingConfiguration|The operation that you want to perform. Set the value to ModifyScalingConfiguration. |
|ScalingConfigurationId|String|Yes|asc-bp16har3jpj6fjbx\*\*\*\*|The ID of the scaling configuration that you want to modify. |
|IoOptimized|String|No|none|Specifies whether the instance to be created is I/O optimized. Valid values:

-   none: The instance to be created is non-I/O optimized.
-   optimized: The instance to be created is I/O optimized. |
|DataDisk.N.Size|Integer|No|100|The size of data disk N. Unit: GiB. Valid values of N: 1 to 16. Valid values:

-   Valid values when DataDisk.N.Category is set to cloud: 5 to 2000
-   Valid values when DataDisk.N.Category is set to cloud\_efficiency: 20 to 32768
-   Valid values when DataDisk.N.Category is set to cloud\_ssd: 20 to 32768
-   Valid values when DataDisk.N.Category is set to cloud\_essd: 20 to 32768
-   Valid values when DataDisk.N.Category is set to ephemeral\_ssd: 5 to 800

If this parameter is specified, the size of the data disk must be greater than or equal to that of the snapshot specified by SnapshotId. |
|DataDisk.N.SnapshotId|String|No|s-snapshot\*\*\*\*|The ID of the snapshot used to create data disk N. Valid values of N: 1 to 16. When this parameter is specified, the DataDisk.N.Size parameter is ignored. The size of the disk is the same as that of the specified snapshot.

If you specify a snapshot that was created on or before July 15, 2013, the operation fails and the system returns InvalidSnapshot.TooOld. |
|DataDisk.N.Category|String|No|cloud\_ssd|The category of data disk N. Valid values of N: 1 to 16. Valid values:

-   cloud: basic disk. The DeleteWithInstance attribute of a basic disk created together with the instance is true.
-   cloud\_efficiency: ultra disk.
-   cloud\_ssd: standard SSD.
-   cloud\_essd: enhanced SSD \(ESSD\).
-   ephemeral\_ssd: local SSD. |
|DataDisk.N.Device|String|No|/dev/xvdb|The mount point of data disk N. Valid values of N: 1 to 16. If this parameter is not specified, the system allocates a mount point to created ECS instances. The name of the mount point ranges from /dev/xvdb to /dev/xvdz in alphabetical order. |
|DataDisk.N.DeleteWithInstance|Boolean|No|true|Specifies whether to release data disk N when the instance to which the data disk is attached is released. Valid values of N: 1 to 16. Valid values:

-   true: releases data disk N when the instance to which the data disk is attached is released.
-   false: retains data disk N when the instance to which the data disk is attached is released.

This parameter is valid only for independently created disks, whose DataDisk.N.Category parameter is set to cloud, cloud\_efficiency, cloud\_ssd, or cloud\_essd. An error is returned if you set this parameter for other disks. |
|DataDisk.N.Encrypted|String|No|false|Specifies whether to encrypt data disk N. Valid values of N: 1 to 16. Valid values:

-   true: encrypts data disk N.
-   false: does not encrypt data disk N. |
|DataDisk.N.KMSKeyId|String|No|0e478b7a-4262-4802-b8cb-00d3fb40\*\*\*\*|The ID of the KMS key corresponding to data disk N. Valid values of N: 1 to 16. |
|DataDisk.N.DiskName|String|No|cloud\_ssdData|The name of data disk N. Valid values of N: 1 to 16. The name must be 2 to 128 characters in length, and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://. |
|DataDisk.N.Description|String|No|Test data disk.|The description of data disk N. Valid values of N: 1 to 16. The description must be 2 to 256 characters in length. It cannot start with http:// or https://. |
|DataDisk.N.AutoSnapshotPolicyId|String|No|sp-bp19nq9enxqkomib\*\*\*\*|The ID of the automatic snapshot policy that is applied to data disk N. Valid values of N: 1 to 16. |
|DataDisk.N.PerformanceLevel|String|No|PL1|Specifies the performance level of the system disk that is an ESSD. The N value must be the same as that in DataDisk.N.Category when DataDisk.N.Category is set to cloud\_essd. Valid values:

-   PL0: A single ESSD can deliver up to 10,000 random read/write IOPS.
-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS.

Default value: PL1.

**Note:** For more information about how to choose ESSD performance levels, see [ESSD](~~122389~~). |
|SpotStrategy|String|No|NoSpot|The preemption strategy to be applied to pay-as-you-go instances and preemptible instances. Valid values:

-   NoSpot: applies to regular pay-as-you-go instances.
-   SpotWithPriceLimit: applies to preemptible instances with maximum hourly prices.
-   SpotAsPriceGo: applies to pay-as-you-go instances that are of the market price at the time of purchase. |
|SpotPriceLimit.N.InstanceType|String|No|ecs.g6.large|The instance type of preemptible instance N. Valid values of N: 1 to 10. This parameter is valid only when the SpotStrategy parameter is set to SpotWithPriceLimit. |
|SpotPriceLimit.N.PriceLimit|Float|No|0.125|The price limit of preemptible instance N. Valid values of N: 1 to 10. This parameter is valid only when the SpotStrategy parameter is set to SpotWithPriceLimit. |
|ScalingConfigurationName|String|No|test-modify|The name of the scaling configuration. The name must be 2 to 64 characters in length, and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a letter or a digit.

The name of the scaling configuration must be unique within a scaling group in a region. If this parameter is not specified, the value of ScalingConfigurationId is used. |
|InstanceName|String|No|inst\*\*\*\*|The name of the instance to be automatically created based on the scaling configuration. |
|HostName|String|No|hos\*\*\*\*|The hostname of the instance to be created. The name cannot start or end with a period \(.\) or hyphen \(-\).It cannot contain consecutive periods \(.\)or hyphens \(-\). Naming conventions:

-   Windows instances: The name must be 2 to 15 characters in length, and can contain letters, digits, and hyphens \(-\). It cannot contain periods \(.\) or contain only digits.
-   Other instances such as Linux instances: The name must be 2 to 64 characters in length. It can be segments separated by periods \(.\).Each segment can contain letters, digits, and hyphens \(-\). |
|ImageId|String|No|centos6u5\_64\_20G\_aliaegis\_2014\*\*\*\*.vhd|The ID of the image that you specified when you create the instance.

**Note:** If the image specified in the scaling configuration contains a system disk and data disks, data stored in the data disks is cleared after you modify this image. |
|ImageName|String|No|suse11sp3\_64\_20G\_aliaegis\_20150428.vhd|The name of the image. Image names must be unique within a region. This parameter is ignored if ImageId is specified.

Alibaba Cloud Marketplace images cannot be specified by using the ImageName parameter. |
|InstanceTypes.N|RepeatList|No|ecs.g6.large|Instance type N from which ECS instances can be created. If you specify this parameter, InstanceType is ignored. You can specify a maximum of 10 instance types for a scaling configuration. Valid values of N: 1 to 10.

N represents the priority of an instance type in the scaling configuration. A lower value of N indicates a higher priority. Auto Scaling creates instances based on the priority of instance types. If Auto Scaling cannot create instances based on the instance type of the highest priority, the instance type of the next highest priority is used. |
|InstanceTypeOverride.N.InstanceType|String|No|ecs.c5.xlarge|If you want to specify the capacity of instance types in the scaling configuration, you must specify both the InstanceTypeOverride.N.InstanceType and InstanceTypeOverride.N.WeightedCapacity parameters.

This parameter is used to specify the instance type. You can specify N values for this parameter. You can customize the weights of multiple instance types in combination with the InstanceTypeOverride.N.WeightedCapacity parameter. Valid values of N: 1 to 10.

**Note:** When you specify InstanceTypeOverride.N.InstanceType, InstanceTypes cannot be specified.

Valid values of InstanceType: For information about available ECS instance types, see [Instance families](~~25378~~). |
|InstanceTypeOverride.N.WeightedCapacity|Integer|No|4|If you want to specify the capacity of instance types in the scaling configuration, you must specify InstanceTypeOverride.N.WeightedCapacity after InstanceTypeOverride.N.InstanceType is specified. The two parameters have a one-to-one correspondence between them. The N value must be the same.

This parameter specifies the weight of the instance type, which indicates the capacity of a single instance of the specified instance type in the scaling group. A greater weight indicates that a less number of instances of the specified instance type is required to meet the expected capacity.

The performance metrics such as the number of vCPUs and the memory size of each instance type may vary. You can configure different weights for different instance types to meet your requirements.

Example:

-   Current capacity: 0
-   Expected capacity: 6
-   Capacity of ecs.c5.xlarge: 4

To meet the expected capacity, Auto Scaling creates two ecs.c5.xlarge instances.

**Note:** The capacity of the scaling group cannot exceed the sum of the maximum capacity \(MaxSize\) and the maximum weight of the instance type.

Valid values: 1 to 500. |
|Cpu|Integer|No|2|The number of vCPUs.

You can specify the number of vCPUs and the amount of memory to define the range of instance types. For example, you can set Cpu to 2 and Memory to 16 to specify instance types that have 2 vCPUs and 16 GiB of memory. Auto Scaling uses factors such as I/O optimization and zone to determine a set of available instance types. Then, Auto Scaling creates instances based on the unit prices of instance types in ascending order.

**Note:** This instance type range is valid only when cost optimization is enabled and the scaling configuration does not have a specified instance type. |
|Memory|Integer|No|16|The amount of memory.

You can specify the number of vCPUs and the amount of memory to define the range of instance types. For example, to specify instance types that have 2 vCPUs and 16 GiB memory, set the value of Cpu to 2 and the value of Memory to 16. Auto Scaling uses factors such as I/O optimization and zone to determine a set of available instance types. Then, Auto Scaling creates instances based on the unit prices of instance types in ascending order.

**Note:** This instance type range is valid only when cost optimization is enabled and the scaling configuration does not have a specified instance type. |
|InternetChargeType|String|No|PayByBandwidth|The billing method for network usage. Valid values:

-   PayByBandwidth: You pay for the maximum available bandwidth specified by the InternetMaxBandwidthOut parameter.
-   PayByTraffic: You pay for the actual traffic used. The InternetMaxBandwidthOut parameter specifies only the upper limit of available bandwidth when this parameter is specified. |
|InternetMaxBandwidthOut|Integer|No|50|The maximum outbound public bandwidth. Unit: Mbit/s. Valid values: 0 to 100.

-   If InternetChargeType is set to PayByBandwidth and this parameter is not specified, this parameter is automatically set to 0.
-   If InternetChargeType is set to PayByTraffic and this parameter is not specified, an error is returned. |
|SystemDisk.Category|String|No|cloud\_efficiency|The category of the system disk. Valid values:

-   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: ESSD
-   ephemeral\_ssd: local SSD |
|SystemDisk.Size|Integer|No|50|The size of the system disk. Unit: GiB. Valid values:

-   Valid values when SystemDisk.Category is set to cloud: 20 to 500
-   Valid values when SystemDisk.Category is set to cloud\_efficiency: 20 to 500
-   Valid values when SystemDisk.Category is set to cloud\_ssd: 20 to 500
-   Valid values when SystemDisk.Category is set to cloud\_essd: 20 to 500
-   Valid values when SystemDisk.Category is set to ephemeral\_ssd: 20 to 500

The specified value must be greater than or equal to max\{20, ImageSize\}. |
|SystemDisk.DiskName|String|No|cloud\_ssdSystem|The name of the system disk. The name must be 2 to 128 characters in length, and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://. |
|SystemDisk.Description|String|No|Test system disk.|The description of the system disk. The description must be 2 to 256 characters in length. It cannot start with http:// or https://. |
|SystemDisk.AutoSnapshotPolicyId|String|No|sp-bp12m37ccmxvbmi5\*\*\*\*|The ID of the automatic snapshot policy that is applied to the system disk. |
|SystemDisk.PerformanceLevel|String|No|PL0|Specifies the performance level of the system disk that is an ESSD. Valid values:

-   PL0: A single ESSD can deliver up to 10,000 random read/write IOPS.
-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS.

Default value: PL0.

**Note:** For more information about how to choose ESSD performance levels, see [ESSD](~~122389~~). |
|LoadBalancerWeight|Integer|No|50|The weight of the ECS instance as a backend server. Valid values: 1 to 100. |
|UserData|String|No|echo hello ecs!|The user data of the ECS instance. It must be encoded in Base64. The maximum size of the raw data is 16 KB. |
|KeyPairName|String|No|KeyPair\_Name|The name of the key pair used to log on to the ECS instance.

-   This parameter is ignored if you are creating a Windows instance. This parameter is empty by default.
-   By default, the username and password authentication method is disabled for Linux instances. |
|RamRoleName|String|No|RamRoleTest|The name of the RAM role associated with the ECS instance. This name is provided and maintained by RAM. You can call the [ListRoles](~~28713~~) operation to query available RAM roles. For more information about how to create a RAM role, see [CreateRole](~~28710~~). |
|PasswordInherit|Boolean|No|false|Specifies whether to use the password predefined in the image. To use this parameter, make sure that a password is configured for the specified image. |
|Tags|String|No|“key1”:”value1”|The tags of the ECS instance. Tags must be specified as key-value pairs. A maximum of 20 tags can be specified. The following limits apply to tag keys and values:

-   A tag key can be up to 64 characters in length and cannot start with acs: or aliyun. It cannot contain http:// or https://. You cannot specify an empty string as a tag key.
-   A tag value can be up to 128 characters in length and cannot start with acs: or aliyun. It cannot contain http:// or https://. You can specify an empty string as a tag value. |
|DeploymentSetId|String|No|ds-bp13v7bjnj9gis\*\*\*\*|The ID of the deployment set to which the ECS instance belongs. |
|SecurityGroupId|String|No|sg-F876F\*\*\*\*|The ID of the security group to which the ECS instance belongs. ECS instances in the same security group can access each other. |
|Override|Boolean|No|true|Specifies whether to overwrite the existing data. Valid values:

-   true: overwrites the existing data.
-   false: does not overwrite the existing data. |
|ResourceGroupId|String|No|abcd1234abcd\*\*\*\*|The ID of the resource group to which an ECS instance belongs. |
|SecurityGroupIds.N|RepeatList|No|sg-bp18kz60mefs\*\*\*\*|The ID of security group N to which the ECS instance is added. The valid values of N depend on the maximum number of security groups to which an instance can be added. For more information, see the "Security group limits" section in [Limits](~~25412~~).

**Note:** You cannot specify both SecurityGroupId and SecurityGroupIds.N at the same time. |
|HpcClusterId|String|No|hpc-clusterid|The ID of the E-HPC cluster to which the ECS instance belongs. |
|InstanceDescription|String|No|Test instance.|The description of the ECS instance. The description must be 2 to 256 characters in length. It cannot start with http:// or https://. |
|Ipv6AddressCount|Integer|No|1|The number of randomly generated IPv6 addresses to be assigned to the elastic network interface \(ENI\). |
|CreditSpecification|String|No|Standard|The performance mode of the burstable instance. Valid values:

-   Standard: the standard mode. For more information, see the "Standard mode" section in [Burstable instances](~~59977~~).
-   Unlimited: the unlimited mode. For more information, see the "Unlimited mode" section in [Burstable instances](~~59977~~). |
|ImageFamily|String|No|hangzhou-daily-update|The name of the image family. You can set this parameter to obtain the latest available custom images within the specified image family. The images are used to create ECS instances. If you have set the ImageId parameter, you cannot set the ImageFamily parameter. |
|ZoneId|String|No|cn-hangzhou-g|The zone ID of the instance. |
|DedicatedHostId|String|No|dh-bp67acfmxazb4p\*\*\*\*|The ID of the dedicated host on which to create instances. If the DedicatedHostId parameter is specified, the SpotStrategy and SpotPriceLimit parameters are ignored. This is because preemptible instances cannot be created on dedicated hosts.

You can call the [DescribeDedicatedHosts](~~134242~~) operation to query the dedicated host list. |
|Affinity|String|No|default|Specifies whether to associate the instance on a dedicated host with the dedicated host. Valid values: 0 to 100.

-   default: does not associate the instance with the dedicated host. When an instance that is in the No Fees for Stopped Instances \(VPC-Connected\) state is restarted, the instance is automatically deployed to another dedicated host in the automatic deployment resource pool if resources of the original dedicated host are insufficient.
-   host: associates the instance with the dedicated host. When an instance that is in the No Fees for Stopped Instances \(VPC-Connected\) state is restarted, the instance still resides on the original dedicated host. If resources of the original dedicated host are insufficient, the instance fails to be restarted. |
|Tenancy|String|No|default|Specifies whether to create the instance on a dedicated host. Valid values:

-   default: creates the instance on a non-dedicated host.
-   host: creates the instance on a dedicated host. If you do not specify the DedicatedHostId parameter, Alibaba Cloud automatically selects a dedicated host for the instance. |
|PrivatePoolOptions.MatchCriteria|String|No|Open|The type of the private pool. After an elasticity assurance or a capacity reservation takes effect, a private pool is generated. You can select a private pool when you start an instance. Valid values:

-   Open: the open mode. In this mode, the system selects a matching private pool of the open type to start the instance. If no matching private pools exist, the instance takes up the capacity of public pool resources. If the parameter is set to Open, the PrivatePoolOptions.Id parameter can be empty.
-   Target: the specified mode. The instance takes up the capacity of a specific private pool to start up. If the specified private pool is unavailable, the instance fails to start up. If this parameter is set to Target, the PrivatePoolOptions.Id parameter must be specified.
-   None: the none mode. In this mode, no private pools are used to start the instance.

**Note:** This parameter is in invitational preview. For more information, submit a ticket. |
|PrivatePoolOptions.Id|String|No|eap-bp67acfmxazb4\*\*\*\*|The ID of the private pool. The ID of the private pool is that of the elasticity assurance or capacity reservation that generates the private pool.

**Note:** This parameter is in invitational preview. For more information, submit a ticket. |
|SpotDuration|Integer|No|1|The protection period of the preemptible instance. Unit: hours. Valid values: 0 to 6.

-   Protection periods of 2, 3, 4, 5, and 6 hours are in invitational preview. If you want to set the protection period value to one of these values, submit a ticket.
-   If this parameter is set to 0, no protection period is configured for the preemptible instance.

Default value: 1. |
|SpotInterruptionBehavior|String|No|Terminate|The interruption mode of the preemptible instance. Set the value to Terminate, which specifies to release the instance. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=ModifyScalingConfiguration
&ScalingConfigurationId=asc-bp16har3jpj6fjbx****
&InstanceName=instan****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyScalingConfigurationResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyScalingConfigurationResponse>
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
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned because you are not authorized to perform the specified operation. |
|404

|InvalidDataDiskSnapshotId.NotFound

|Snapshot “XXX” does not exist.

|The error message returned because the specified snapshot does not exist. |
|400

|InvalidDataDiskSnapshotId.SizeNotSupported

|The capacity of snapshot “XXX” exceeds the size limit of the specified disk category.

|The error message returned because the size of the specified snapshot exceeds the maximum size allowed for the specified disk category. |
|404

|InvalidImageId.NotFound

|The specified image does not exist.

|The error message returned because the specified image does not exist. |
|400

|InvalidKeyPairName.NotFound

|The specified KeyPairName does not exist in our records.

|The error message returned because the specified KeyPairName parameter does not exist. |
|400

|InvalidNetworkType.ForRAMRole

|RAMRole can’t be used For classic instance.

|The error message returned because the instance is a classic network-type instance that does not support the RamRoleName parameter. |
|400

|InvalidParamter

|The specified value of parameter is not valid.

|The error message returned because a specified parameter is invalid. |
|400

|InvalidScalingConfigurationName.Duplicate

|The specified value of parameter is duplicated.

|The error message returned because the specified scaling configuration name already exists. |
|400

|InvalidSecurityGroupId.IncorrectNetworkType

|The network type of specified Security Group does not support this action.

|The error message returned because the network types of the specified security group and the scaling group are different. |
|400

|InvalidSecurityGroupId.VPCMismatch

|The specified security group and the specified virtual switch are not in the same VPC.

|The error message returned because the specified security group and the vSwitch are not in the same VPC. |
|400

|InvalidTags.KeyValue

|The specified tags key/value cannot be empty.

|The error message returned because the Tags parameter is not specified. |
|400

|InvalidTags.ListSize

|The specified tags list size cannot be more than “5”.

|The error message returned because the maximum number of Tags that can be specified for the ECS instances has been reached. |
|400

|InvalidUserData.Base64FormatInvalid

|The specified parameter UserData must be base64 encoded.

|The error message returned because the specified user data is not encoded in Base64. |
|400

|InvalidUserData.SizeExceeded

|The specified parameter UserData exceeds the size.

|The error message returned because the user data size has exceeded the upper limit. |

