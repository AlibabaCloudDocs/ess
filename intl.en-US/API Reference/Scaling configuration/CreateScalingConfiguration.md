# CreateScalingConfiguration

You can call this operation to create a scaling configuration.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer automatically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=CreateScalingConfiguration&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateScalingConfiguration|The operation that you want to perform. Set the value to CreateScalingConfiguration. |
|ScalingGroupId|String|Yes|asg-bp14wlu85wrpchm0\*\*\*\*|The ID of the scaling group to which the scaling configuration belongs. |
|ImageId|String|No|centos6u5\_64\_20G\_aliaegis\*\*\*\*.vhd|The ID of the image that you specified when you create the instance. |
|ImageName|String|No|image\*\*\*\*|The name of the image. Image names must be unique within a region. This parameter is ignored if ImageId is specified.

Alibaba Cloud Marketplace images cannot be specified by the ImageName parameter. |
|InstanceType|String|No|ecs.g6.large|The instance type from which ECS instances are to be created. For more information, see [Instance families](~~25378~~). |
|Cpu|Integer|No|2|The number of vCPUs.

You can specify the number of vCPUs and the amount of memory to define the range of instance types. For example, to specify instance types that have 2 vCPUs and 16 GiB memory, set Cpu to 2 and Memory to 16. Auto Scaling uses factors such as I/O optimization and zone to determine a set of available instance types. Auto Scaling then creates instances based on the unit prices of instance types in ascending order.

**Note:** This instance type range takes effect only when cost optimization is enabled and you have not specified an instance type in the scaling configuration. |
|Memory|Integer|No|16|The amount of memory.

You can specify the number of vCPUs and the amount of memory to define the range of instance types. For example, to specify instance types that have 2 vCPUs and 16 GiB memory, set Cpu to 2 and Memory to 16. Auto Scaling uses factors such as I/O optimization and zone to determine a set of available instance types. Auto Scaling then creates instances based on the unit prices of instance types in ascending order.

**Note:** This instance type range takes effect only when cost optimization is enabled and you have not specified an instance type in the scaling configuration. |
|DeploymentSetId|String|No|ds-bp1frxuzdg87zh4pz\*\*\*\*|The ID of the deployment set to which the ECS instance belongs. |
|InstanceTypes.N|RepeatList|No|ecs.g6.large|The instance type N from which ECS instances can be created. If you specify this parameter, InstanceType is ignored. You can specify a maximum of 10 instance types for a scaling configuration. Valid values of N: 1 to 10.

N represents the priority of an instance type in the scaling configuration. A lower value of N indicates a higher priority. Auto Scaling creates instances based on the priority of instance types. If Auto Scaling cannot create instances based on the instance type of the highest priority, the instance type of the next highest priority will be used. |
|SecurityGroupId|String|No|sg-280ih\*\*\*\*|The ID of the security group to which the ECS instance belongs. ECS instances in the same security group can access each other. |
|IoOptimized|String|No|optimized|Specifies whether the instance to be created is I/O optimized. For instances of retired instance types, the default value is none. For other instances, the default value is optimized. For more information, see [Phased-out instance types](~~55263~~). Valid values:

-   none: The instance to be created is non-I/O optimized.
-   optimized: The instance to be created is I/O optimized. |
|InternetChargeType|String|No|PayByTraffic|The billing method for network usage. Valid values:

-   PayByBandwidth: You must pay for the maximum available bandwidth specified by the InternetMaxBandwidthOut parameter.
-   PayByTraffic: You pay for the actual traffic used. The InternetMaxBandwidthOut parameter specifies only the upper limit of available bandwidth when this parameter is specified.

Default value: PayByBandwidth for the classic network or PayByTraffic for VPCs. |
|InternetMaxBandwidthIn|Integer|No|100|The maximum inbound bandwidth from the Internet. Unit: Mbit/s. Valid values: 1 to 200.

Default value: 200. This parameter is not used for billing because the inbound traffic to instances is free of charge. |
|InternetMaxBandwidthOut|Integer|No|50|The maximum outbound bandwidth to the Internet. Unit: Mbit/s. Valid values: 0 to 100.

-   If InternetChargeType is set to PayByBandwidth and this parameter is not specified, this parameter is automatically set to 0.
-   If InternetChargeType is set to PayByTraffic and this parameter is not specified, an error is returned. |
|SystemDisk.Category|String|No|cloud\_ssd|The category of the system disk. Valid values:

-   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   ephemeral\_ssd: local SSD
-   cloud\_essd: enhanced SSD

For non-I/O optimized instances of generation I instance types, the default value is cloud. In other cases, the default value is cloud\_eﬃciency. |
|SystemDisk.Size|Integer|No|100|The size of the system disk. Unit: GiB. Valid values:

-   Valid values when SystemDisk.Category is set to cloud: 20 to 500
-   Valid values when SystemDisk.Category is set to cloud\_efficiency: 20 to 500
-   Valid values when SystemDisk.Category is set to cloud\_ssd: 20 to 500
-   Valid values when SystemDisk.Category is set tocloud\_essd: 20 to 500
-   Valid values when SystemDisk.Category is set toephemeral\_ssd: 20 to 500

If this parameter is specified, the system disk size must be greater than or equal to max\{20, ImageSize\}.

The default value is 40 GiB or the size of the image, depending on whichever is greater. |
|SystemDisk.DiskName|String|No|cloud\_ssdSystem|The name of the system disk. The name must be 2 to 128 characters in length, and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://.

This parameter is empty by default. |
|SystemDisk.Description|String|No|Test system disk.|The description of the system disk. The description must be 2 to 256 characters in length and cannot start with http:// or https://. |
|SystemDisk.AutoSnapshotPolicyId|String|No|sp-bp12m37ccmxvbmi5\*\*\*\*|The ID of the automatic snapshot policy that is applied to the system disk. |
|ScalingConfigurationName|String|No|scalingconfig\*\*\*\*|The name of the scaling configuration. It must be 2 to 64 characters in length, and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a letter or a digit.

The name of the scaling configuration must be unique within a scaling group in a specific region. If this parameter is not specified, the value of ScalingConfigurationId is used. |
|DataDisk.N.Size|Integer|No|100|The size of data disk N. Unit: GiB. Valid values of N: 1 to 16. Valid values:

-   Valid values when DataDisk.N.Category is set to cloud: 5 to 2000
-   Valid values when DataDisk.N.Category is set to cloud\_efficiency: 20 to 32768
-   Valid values when DataDisk.N.Category is set to cloud\_ssd: 20 to 32768
-   Valid values when DataDisk.N.Category is set to cloud\_essd: 20 to 32768
-   Valid values when DataDisk.N.Category is set to ephemeral\_ssd: 5 to 800

If this parameter is specified, the data disk size must be greater than or equal to that of the snapshot specified by SnapshotId. |
|DataDisk.N.SnapshotId|String|No|s-280s7\*\*\*\*|The ID of the snapshot used to create data disk N. Valid values of N: 1 to 16. When this parameter is specified, the DataDisk.N.Size parameter is ignored. The size of the disk will be the same as that of the specified snapshot.

If you specify a snapshot that was created on or before July 15, 2013, the operation fails and returns InvalidSnapshot.TooOld. |
|DataDisk.N.Category|String|No|cloud\_ssd|The category of data disk N. Valid values of N: 1 to 16. Valid values:

-   cloud: basic disk. The DeleteWithInstance attribute of a basic disk created together with the instance is true.
-   cloud\_efficiency: ultra disk.
-   cloud\_ssd: standard SSD.
-   ephemeral\_ssd: local SSD.
-   cloud\_essd: enhanced SSD.

For I/O optimized instances, the default value is cloud\_efficiency. For non-I/O optimized instances, the default value is cloud. |
|DataDisk.N.Device|String|No|/dev/xvdb|The mount point of data disk N. Valid values of N: 1 to 16. If this parameter is not specified, the system automatically allocates a mount point to created ECS instances. The name of the mount point ranges from /dev/xvdb to /dev/xvdz in alphabetical order. |
|DataDisk.N.DeleteWithInstance|Boolean|No|true|Specifies whether data disk N is to be released with its attached instance. Valid values of N: 1 to 16. Valid values:

-   true: releases the data disk with its attached instance.
-   false: retains the data disk when the attached instance is released.

This parameter is valid only for independently created disks, whose DataDisk.N.Category parameter is set to cloud, cloud\_efficiency, cloud\_ssd, or cloud\_essd. An error will be returned if you set this parameter for other disks.

Default value: true |
|DataDisk.N.Encrypted|String|No|false|Specifies whether to encrypt data disk N. Valid values of N: 1 to 16. Valid values:

-   true: encrypts the data disks.
-   false: does not encrypt the data disks.

Default value: false |
|DataDisk.N.KMSKeyId|String|No|0e478b7a-4262-4802-b8cb-00d3fb40\*\*\*\*|The ID of the KMS key corresponding to data disk N. Valid values of N: 1 to 16. |
|DataDisk.N.DiskName|String|No|cloud\_ssdData|The name of data disk N. Valid values of N: 1 to 16. It must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\).

This parameter is empty by default. |
|DataDisk.N.Description|String|No|Test data disk.|The description of data disk N. Valid values of N: 1 to 16. It must be 2 to 256 characters in length and cannot start with http:// or https://. |
|DataDisk.N.AutoSnapshotPolicyId|String|No|sp-bp19nq9enxqkomib\*\*\*\*|The ID of the automatic snapshot policy that is applied to data disk N. Valid values of N: 1 to 16. |
|LoadBalancerWeight|Integer|No|50|The weight of the ECS instance as a backend server. Valid values: 1 to 100.

Default value: 50 |
|Tags|String|No|\{"key1":"value1","key2":"value2", ... "key5":"value5"\}|The tags of the ECS instance. Tags must be specified as key-value pairs. A maximum of five tags can be specified. The following limits apply to keys and values:

-   A key can be up to 64 characters in length and cannot start with acs: or aliyun. It cannot contain http:// or https://. You cannot specify an empty string as a key.
-   A value can be up to 128 characters in length and cannot start with acs: or aliyun. It cannot contain http:// or https://. You can specify an empty string as a value. |
|UserData|String|No|echo hello ecs!|The user data of the ECS instance. It must be encoded in Base64. The maximum size of the raw data is 16 KB. |
|KeyPairName|String|No|KeyPairTest|The name of the key pair used to log on to the ECS instance.

-   Ignore this parameter if you are creating an ECS Windows instance. This parameter is empty by default.
-   By default, the username and password authentication method is disabled for ECS Linux instances. |
|RamRoleName|String|No|ramrole\*\*\*\*|The name of the RAM role associated with the ECS instance. This name is provided and maintained by RAM. You can call the [ListRoles](~~28713~~) operation to query available RAM roles. For more information about how to create a RAM role, see [CreateRole](~~28710~~). |
|SecurityEnhancementStrategy|String|No|Active|Specifies whether to enable security hardening. Valid values:

-   Active: enables security hardening. This value is applicable only to public images.
-   Deactive: disables security hardening. This value is applicable to all image types. |
|InstanceName|String|No|instance\*\*\*\*|The name of the instance to be created based on the current scaling configuration. |
|HostName|String|No|host\*\*\*\*|The name of the host where the created ECS instances reside. The name cannot start or end with a period \(.\) or hyphen \(-\). It cannot contain consecutive periods \(.\) or hyphens \(-\). Naming conventions:

-   Windows instances: The name must be 2 to 15 characters in length, and can contain letters, digits, and hyphens \(-\). It cannot contain periods \(.\) or contain only digits.
-   Other instances such as Linux instances: The name must be 2 to 64 characters in length. It can be segments separated by periods \(.\). Each segment can contain letters, digits, and hyphens \(-\). |
|SpotStrategy|String|No|NoSpot|The preemption strategy to be applied to pay-as-you-go instances. Valid values:

-   NoSpot: applies to regular pay-as-you-go instances.
-   SpotWithPriceLimit: applies to preemptible instances with maximum hourly prices.
-   SpotAsPriceGo: applies to preemptible instances whose prices are based on the current market price.

Default value: NoSpot |
|PasswordInherit|Boolean|No|false|Specifies whether to use the password predefined in the image. To use this parameter, ensure that a password is configured for the specified image. Valid values:

-   true: uses the password predefined in the image.
-   false: does not use the password predefined in the image. |
|SpotPriceLimit.N.InstanceType|String|No|ecs.g6.large|The instance type of preemptible instance N. Valid values of N: 1 to 10. This parameter takes effect only when the SpotStrategy parameter is set to SpotWithPriceLimit. |
|SpotPriceLimit.N.PriceLimit|Float|No|0.5|The price limit of preemptible instance N. Valid values of N: 1 to 10. This parameter takes effect only when the SpotStrategy parameter is set to SpotWithPriceLimit. |
|Password|String|No|123abc\*\*\*\*|The password that is used to access the ECS instance. The password must be 8 to 30 characters in length and contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include

```
()` ~! @#$%^&*-_+=\|{}[]:;'<>,.? /
```

The password of Windows instances cannot start with a forward slash \(/\).

**Note:** For security reasons, we recommend that you use HTTPS to send requests if the Password parameter is specified. |
|ResourceGroupId|String|No|rg-resource\*\*\*\*|The ID of the resource group to which the ECS instance belongs. |
|SecurityGroupIds.N|RepeatList|No|sg-bp18kz60mefs\*\*\*\*|Specifies the ID of security group N to which ECS instances are added. The valid values of N depend on the maximum number of security groups to which an instance can be added. For more information, see the "Security groups" section in [Limits](~~25412~~).

**Note:** You cannot specify SecurityGroupId and SecurityGroupIds.N at the same time. |
|HpcClusterId|String|No|hpc-clusterid|The ID of the HPC cluster to which the ECS instance belongs. |
|InstanceDescription|String|No|Test instance.|The description of the ECS instance. It must be 2 to 256 characters in length and cannot start with http:// or https://. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |
|Ipv6AddressCount|Integer|No|1|The number of randomly generated IPv6 addresses that are assigned to the ENI. |
|CreditSpecification|String|No|Standard|The performance mode of the burstable instance. Valid values:

-   Standard: standard mode. For more information, see the "Standard mode" section in [Burstable instances](~~63440~~).
-   Unlimited: unlimited mode. For more information, see the "Unlimited mode" section in [Burstable instances](~~63440~~).

This parameter is empty by default. |
|ImageFamily|String|No|hangzhou-daily-update|The name of the image family. You can configure this parameter to obtain the latest available custom images within the specified image family to create ECS instances. If you have set the ImageId parameter, you cannot set the ImageFamily parameter. |
|DedicatedHostId|String|No|dh-bp67acfmxazb4p\*\*\*\*|The ID of the dedicated host on which to create the instance. If the DedicatedHostId parameter is specified, the SpotStrategy and SpotPriceLimit parameters are ignored. This is because preemptible instances cannot be created on dedicated hosts.

You can call the [DescribeDedicatedHosts](~~134242~~) operation to query the dedicated host list. |
|Affinity|String|No|default|Specifies whether the instance on a dedicated host is associated with the dedicated host. Valid values:

-   default: The instance is not associated with the dedicated host. When the No Fees for Stopped Instances \(VPC-Connected\) feature is enabled and the instance is restarted, the instance is automatically deployed to another dedicated host in the automatic deployment resource pool if resources of the original dedicated host are insufficient.
-   host: The instance is associated with the dedicated host. When the No Fees for Stopped Instances \(VPC-Connected\) feature is enabled and the instance is restarted, the instance still resides on the original dedicated host. If resources of the original dedicated host are insufficient, the instance fails to be restarted.

Default value: default |
|Tenancy|String|No|default|Specifies whether to create the instance on a dedicated host. Valid values:

-   default: creates the instance on a non-dedicated host.
-   host: creates the instance on a dedicated host. If you do not specify the DedicatedHostId parameter, Alibaba Cloud automatically selects a dedicated host for the instance.

Default value: default |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|ScalingConfigurationId|String|asc-bp1ffogfdauy0nu5\*\*\*\*|The ID of the scaling configuration. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=CreateScalingConfiguration
&ScalingGroupId=asg-bp14wlu85wrpchm0****
&SecurityGroupId=sg-280ih****
&ImageId=centos6u5_64_20G_aliaegis****.vhd
&InstanceTypes.1=ecs.g6.large
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateScalingConfigurationResponse>
      <ScalingConfigurationId>asc-bp1ffogfdauy0nu5****</ScalingConfigurationId>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</CreateScalingConfigurationResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "ScalingConfigurationId": "asc-bp1ffogfdauy0nu5****"
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

|InstanceType.Mismatch

|The specified scaling configuration and existing active scaling configuration have different instance type.

|The error message returned because the instance types of the specified scaling configuration and the current scaling configuration are different. |
|404

|InvalidDataDiskSnapshotId.NotFound

|Snapshot “XXX” does not exist.

|The error message returned because the specified snapshot does not exist. |
|400

|InvalidDataDiskSnapshotId.SizeNotSupported

|The capacity of snapshot “XXX” exceeds the size limit of the specified disk category.

|The error message returned because the size of the specified snapshot exceeds the maximum size allowed for the specified disk category. |
|403

|InvalidDevice.InUse

|Device “XXX” has been occupied.

|The error message returned because the mount point of the data disk is already occupied. |
|400

|InvalidImageId.InstanceTypeMismatch

|The specified image does not support the specified instance type.

|The error message returned because the specified image does not support the specified instance type. |
|404

|InvalidImageId.NotFound

|The specified image does not exist.

|The error message returned because the specified image does not exist in the current account. |
|400

|InvalidKeyPairName.NotFound

|The specified KeyPairName does not exist in our records.

|The error message returned because the specified key pair name does not exist. |
|400

|InvalidNetworkType.ForRAMRole

|RAMRole can't be used For classic instance.

|The error message returned because the network type of the instance is classic network that does not support the RamRoleName parameter. |
|400

|InvalidParameter

|The specified value of parameter KeyPairName is not valid.

|The error message returned because the specified instance OS is Windows that does not support the KeyPairName parameter. |
|400

|InvalidParameter.Conflict

|The value of parameter SystemDisk.Category and parameter DataDisk.N.Category are conflict.

|The error message returned because the specified system disk category conflicts with the data disk category. |
|400

|InvalidRamRole.NotFound

|The specified RamRoleName does not exist.

|The error message returned because the specified RAM role name does not exist. |
|400

|InvalidScalingConfigurationName.Duplicate

|The specified value of parameter ScalingConfigurationName is duplicated.

|The error message returned because the scaling configuration name already exists. |
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist in the current account. |
|400

|InvalidSecurityGroupId.IncorrectNetworkType

|The network type of specified security Group does not support this action.

|The error message returned because the network types of the specified security group and the scaling group are different. |
|404

|InvalidSecurityGroupId.NotFound

|The specified security group does not exist.

|The error message returned because the specified security group does not exist in the current account. |
|400

|InvalidSecurityGroupId.VPCMismatch

|The specified security group and the specified virtual switch are not in the same VPC.

|The error message returned because the specified security group and the VSwitch are not in the same VPC. |
|403

|InvalidSnapshot.TooOld

|This operation is denied because the specified snapshot is created before 2013-07-15.

|The error message returned because the snapshot was created on or before July 15, 2013 and the request is rejected. |
|403

|InvalidSystemDiskCategory.ValueUnauthorized

|The system disk category is not authorized.

|The error message returned because you are not authorized to create an ephemeral system disk. |
|400

|InvalidUserData.Base64FormatInvalid

|The specified parameter UserData must be base64 encoded.

|The error message returned because the specified user data is not encoded in Base64. |
|400

|InvalidUserData.SizeExceeded

|The specified parameter UserData exceeds the size.

|The error message returned because the maximum size of the user data has been reached. |
|403

|QuotaExceeded.EphemeralDiskSize

|Ephemeral disk size quota exceeded.

|The error message returned because the total capacity of mounted ephemeral data disks has exceeded 2 TiB \(2,048 GiB\). |
|400

|QuotaExceeded.ScalingConfiguration

|Scaling configuration quota exceeded in the specified scaling group.

|The error message returned because the maximum number of scaling configurations has been reached. |
|400

|QuotaExceeded.SecurityGroupInstance

|Instance quota exceeded in the specified security group.

|The error message returned because the maximum number of ECS instances that can be added to the specified security group has been reached. |

