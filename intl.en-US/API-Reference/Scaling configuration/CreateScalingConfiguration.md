# CreateScalingConfiguration {#doc_api_Ess_CreateScalingConfiguration .reference}

You can call this operation to create a scaling configuration.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=CreateScalingConfiguration) simplifies API usage. You can use OpenAPI Explorer to perform operations such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description |
|---------|----|--------|-------|------------|
|ScalingGroupId|String|Yes|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|The ID of the scaling group to which the scaling configuration to be created belongs.

 |
|SecurityGroupId|String|Yes|sg-280ih\*\*\*\*|The ID of the security group to which created instances belong. Mutual access is allowed between instances in a security group.

 |
|Action|String|No|CreateScalingConfiguration|The operation that you want to perform. Set the value to CreateScalingConfiguration.

 |
|Cpu|Integer|No|2|The number of vCPUs.

 You can specify the number of CPU cores and the amount of memory to define the range of instance types. For example, instance types with a specified value of CPU as 2 and Memory as 16 can be defined as 2 vCPU 16 GiB. Auto Scaling uses factors such as I/O optimization and zone to determine a set of available instance types. Auto Scaling then creates instances of the type that is most cost-effective out of the available types.

 **Note:** This instance type range takes effect only when cost optimization is enabled and the scaling configuration does not have a specified instance type.

 |
|DataDisk.N.Category|String|No|cloud\_ssd|The category of data disk N. Valid values of N: 1 to 16. Valid values:

 -   cloud: indicates a basic disk. The DeleteWithInstance property of a basic disk created along with the instance is true.
-   cloud\_efficiency: indicates an ultra disk.
-   cloud\_ssd: indicates an SSD disk.
-   ephemeral\_ssd: indicates a local SSD disk.

 Default value: cloud.

 |
|DataDisk.N.DeleteWithInstance|Boolean|No|true|Indicates whether data disk N is to be released with its attached instance. Valid values:

 -   true: Release the data disk with its attached instance.
-   false: Retain the data disk when the attached instance is released.

 Default value: true. This parameter is valid only for independent disks, for which the DataDisk.N.Category parameter is set to cloud, cloud\_efficiency, or cloud\_ssd. An error will be returned if you set this parameter for other disks.

 |
|DataDisk.N.Description|String|No|FinanceDept|The description of data disk N. It must be 2 to 256 characters in length and cannot start with "http://" or "https://."

 |
|DataDisk.N.Device|String|No|/dev/xvdb|The mount point of data disk N. Valid values of N: 1 to 4. If this parameter is not specified, ECS automatically allocates a mount point to created ECS instances. The name of the mount point ranges from /dev/xvdb to /dev/xvdz in an alphabetical order.

 |
|DataDisk.N.DiskName|String|No|cloud\_ssdData|The name of data disk N. It must be 2 to 128 characters in length. It must start with a letter and cannot start with "http://" or "https://." It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). Default value: empty.

 |
|DataDisk.N.Encrypted|String|No|false|Indicates whether data disk N is to be encrypted. Default value: false.

 |
|DataDisk.N.KMSKeyId|String|No|0e478b7a-4262-4802-b8cb-00d3fb40826X|The KMS key ID corresponding to the data disk.

 |
|DataDisk.N.Size|Integer|No|100|The size of data disk N. Unit: GB. Valid values:

 -   cloud: 5 to 2000
-   cloud\_efficiency: 20 to 32768.
-   cloud\_ssd: 20 to 32768.
-   ephemeral\_ssd: 5 to 800.

 If this parameter is specified, the data disk size must be greater than or equal to the size of the snapshot specified by SnapshotId.

 |
|DataDisk.N.SnapshotId|String|No|s-280s7\*\*\*\*|The ID of the snapshot used to create data disk N. After this parameter is specified, DataDisk.N.Size is ignored and the size of the created disk is the size of the specified snapshot. You cannot specify a snapshot that was created on or before July 15, 2013.

 |
|DeploymentSetId|String|No|ds-bp1frxuzdg87zh4pz\*\*\*\*|The ID of the deployment set.

 |
|HostName|String|No|Host\*\*\*\*|The hostname of the ECS instance. It cannot start or end with a period \(.\) or hyphen \(-\). It cannot have two or more consecutive periods \(.\) or hyphens \(-\). Naming rules:

 -   Windows-based instances: It must be 2 to 15 characters in length. It can contain uppercase or lowercase letters, digits, and hyphens \(-\). It cannot contain periods \(.\) or be entirely composed of digits.
-   Other instances such as Linux instances: It must be 2 to 64 characters in length. It can be segments separated by periods \(.\). Each segment can contain uppercase or lowercase letters, digits, and hyphens \(-\).

 |
|ImageId|String|No|centos6u5\_64\_20G\_aliaegis\_20140703.vhd|The ID of the image file that was specified when the instance was started.

 |
|ImageName|String|No|myimage|The name of the image file. Image names must be unique within a region. This parameter is ignored if ImageId is specified. Marketplace images cannot be specified by the ImageName parameter.

 |
|InstanceName|String|No|Instance\*\*\*\*|The name of the instance that is created based on the current scaling configuration.

 |
|InstanceType|String|No|ecs.t1.xsmall|The single instance type from which ECS instances are to be created.

 |
|InstanceTypes.N|RepeatList|No|ecs.t1.xsmall. 1|The multiple instance types from which ECS instances are to be created. InstanceType is ignored if this parameter is specified. Valid values of N: 1 to 10. This means that up to 10 instance types can be configured for a scaling configuration. N represents the priority of the instance type in the scaling configuration. A lower value of N indicates a higher priority for the instance type. If an instance of the highest priority type cannot be created, Auto Scaling will create an instance of the next highest priority type.

 |
|InternetChargeType|String|No|PayByBandwidth|The bandwidth billing type of created instances. Valid values:

 -   PayByBandwidth: Users pay for the maximum available bandwidth specified by the InternetMaxBandwidthOut parameter.
-   PayByTraffic Users pay for the actual traffic used. The InternetMaxBandwidthOut parameter only specifies the upper limit of available bandwidth when this parameter is specified.

 Default value: PayByBandwidth for classic networks or PayByTraffic for VPCs.

 |
|InternetMaxBandwidthIn|Integer|No|100|The maximum inbound bandwidth from the public network. Unit: Mbit/s. Valid values: 1 to 200. Default value: 200. This parameter is not used for billing because the inbound traffic to instances is free of charge.

 |
|InternetMaxBandwidthOut|Integer|No|50|The maximum outbound bandwidth to the public network. Unit: Mbit/s. Valid values: 0 to 100.

 -   If InternetChargeType is set to PayByBandwidth and this parameter is not specified, this parameter is automatically set to 0.
-   If InternetChargeType is set to PayByTraffic and this parameter is not specified, an error is returned.

 |
|IoOptimized|String|No|optimized|Indicates whether the instance is I/O optimized. This parameter is unavailable for non I/O-optimized instances. Valid value:

 -   optimized
-   Empty:
    -   Generation I instance types are not I/O optimized by default.
    -   Instance types of later generations are I/O optimized by default.

 |
|KeyPairName|String|No|KeyPairTest|The name of the key pair.

 -   Ignore this parameter if you are creating a Windows-based ECS instance. This parameter is null by default.
-   Password logon is disabled for Linux-based ECS instances by default.

 |
|LoadBalancerWeight|Integer|No|50|The weight of the back-end server. Valid values: 0 to 100. Default value: 50.

 |
|Memory|Integer|No|16|The size of memory.

 You can specify the number of CPU cores and the amount of memory to define the range of instance types. For example, instance types with a specified value of CPU as 2 and Memory as 16 can be defined as 2 vCPU 16 GiB. Auto Scaling uses factors such as I/O optimization and zone to determine a set of available instance types. Auto Scaling then creates instances of the type that is most cost-effective out of the available types.

 **Note:** This instance type range takes effect only when cost optimization is enabled and the scaling configuration does not have a specified instance type.

 |
|Password|String|No|123-abcABC|The password of the instance. It must be 8 to 30 characters in length. It must include at least three of the following characters types: uppercase letters, lowercase letters, digits, and special characters. Special characters include:

 ```
()`~! @#$%^&*-_+=\|{}[]:;'<>,.? /
```

 Passwords for Windows-based instances cannot start with a forward slash \(/\).

 **Note:** We recommend that you use HTTPS to send requests if the Password parameter is specified to avoid password leakage.

 |
|PasswordInherit|Boolean|No|false|Indicates whether to use the preconfigured password of the specified image. To use this parameter, ensure that a password is configured for the specified image.

 |
|RamRoleName|String|No|RamRoleTest|The name of the instance RAM role. This name is provided and maintained by RAM. Call [ListRoles](~~28713~~) to query the list of RAM role names. For more information, see [CreateRole](~~28710~~).

 |
|ResourceGroupId|String|No|rg-resource\*\*\*\*|The ID of the resource group.

 |
|ScalingConfigurationName|String|No|Test\_ sc|The name of the scaling configuration. It must be 2 to 40 characters in length. It must start with a digit, uppercase letter, or lowercase letter. It can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). Scaling configuration names must be unique within a scaling group. If this parameter is not specified, the value of ScalingConfigurationId is used.

 |
|SecurityEnhancementStrategy|String|No|Active|Indicates whether to enable security hardening. Valid values:

 -   Active: Enables security hardening for public images.
-   Deactive: Disables security hardening for all images.

 |
|SpotPriceLimit.N.InstanceType|String|No|ecs.t1.xsmall|The instance type of preemptible instance N. Valid values of N: 1 to 10. This parameter takes effect only when the SpotStrategy parameter is set to SpotWithPriceLimit.

 |
|SpotPriceLimit.N.PriceLimit|Float|No|0.5|The price limit of preemptible instance N. Valid values of N: 1 to 10. This parameter takes effect only when the SpotStrategy parameter is set to SpotWithPriceLimit.

 |
|SpotStrategy|String|No|NoSpot|The preemption policy to be used for pay-as-you-go instances. Valid values:

 -   NoSpot: indicates a pay-as-you-go instance.
-   SpotWithPriceLimit: indicates a preemptible instance with a maximum price.
-   SpotAsPriceGo: indicates an instance with its price based on the market price at the time of purchase.

 Default value: NoSpot.

 |
|SystemDisk.Category|String|No|cloud\_ssd|The type of the system disk. Valid values:

 -   cloud: indicates a basic disk.
-   cloud\_efficiency: indicates an ultra disk.
-   cloud\_ssd: indicates an SSD disk.
-   ephemeral\_ssd: indicates a local SSD disk.

 Default value: cloud for Generation I type instances that are not I/O optimized, and cloud\_efficiency for other types.

 |
|SystemDisk.Description|String|No|FinanceDept|The description of the system disk. It must be 2 to 256 characters in length and cannot start with "http://" or "https://."

 |
|SystemDisk.DiskName|String|No|cloud\_ssdSystem|The name of the system disk. It must be 2 to 128 characters in length. It must start with a letter and cannot start with "http://" or "https://." It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). Default value: null.

 |
|SystemDisk.Size|Integer|No|100|The size of the system disk. Unit: GB. Valid values:

 -   cloud: 40 to 500.
-   cloud\_efficiency: 40 to 500.
-   cloud\_ssd: 40 to 500.
-   ephemeral\_ssd: 40 to 500.

 Default value: the greater value out of ImageSize and 40. The specified value must be greater than or equal to the default value.

 |
|Tags|String|No|\{"key1":"value1","key2":"value2", ... "key5":"value5"\}|The tags of the instance. Tags must be specified as key-value pairs. Up to five tags can be used. Requirements for keys and values:

 -   A key can be up to 64 characters in length. It cannot start with "aliyun", "http://", or "https://." It cannot be left empty.
-   A value can be up to 128 characters in length. It cannot start with "aliyun", "http://", or "https://." It can be left empty.

 |
|UserData|String|No|echo hello ecs!|The custom data of the instance. It must be encoded in the Base64 format. The maximum size of the raw data is 16 KB.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description |
|---------|----|-------|------------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |
|ScalingConfigurationId|String|eOs27Kb0oXvQcUYjEGel\*\*\*\*|The ID of the scaling configuration. It is generated by the system and must be globally unique.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://[Endpoint]/? Action=CreateScalingConfiguration
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&SecurityGroupId=sg-280ih****
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CreateScalingConfigurationResponse> 
  <ScalingConfigurationId>eOs27Kb0oXvQcUYjEGel****</ScalingConfigurationId>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</CreateScalingConfigurationResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"ScalingConfigurationId":"eOs27Kb0oXvQcUYjEGel****",
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Ess)

 

|HTTP status code

|Error code

|Error message

|Description

|
|------------------|------------|---------------|-------------|
|400

|InstanceType.Mismatch

|The specified scaling configuration and existing active scaling configuration have different instance type.

|The error message returned when the instance types of the specified scaling configuration and the current scaling configuration are different.

|
|404

|InvalidDataDiskSnapshotId.NotFound

|Snapshot “XXX” does not exist.

|The error message returned when the specified snapshot does not exist.

|
|400

|InvalidDataDiskSnapshotId.SizeNotSupported

|The capacity of snapshot “XXX” exceeds the size limit of the specified disk category.

|The error message returned when the size of the specified snapshot exceeds the maximum size of the specified disk category.

|
|403

|InvalidDevice.InUse

|Device “XXX” has been occupied.

|The error message returned when the mount point of the data disk is already occupied.

|
|400

|InvalidImageId.InstanceTypeMismatch

|The specified image does not support the specified instance type.

|The error message returned when the specified image does not support the specified instance type.

|
|404

|InvalidImageId.NotFound

|The specified image does not exist.

|The error message returned when the specified image does not exist in the current account.

|
|400

|InvalidKeyPairName.NotFound

|The specified KeyPairName does not exist in our records.

|The error message returned when the specified key pair name does not exist.

|
|400

|InvalidNetworkType.ForRAMRole

|RAMRole can't be used For classic instance.

|The error message returned when the network type of the instance is classic network and does not support the RamRoleName parameter.

|
|400

|InvalidParameter

|The specified value of parameter KeyPairName is not valid.

|The error message returned when the specified instance OS is Windows and does not support the KeyPairName parameter.

|
|400

|InvalidParameter.Conflict

|The value of parameter SystemDisk.Category and parameter DataDisk.N.Category are conflict.

|The error message returned when the specified system disk type conflicts with the data disk type.

|
|400

|InvalidRamRole.NotFound

|The specified RamRoleName does not exist.

|The error message returned when the specified RAM role name does not exist.

|
|400

|InvalidScalingConfigurationName.Duplicate

|The specified value of parameter ScalingConfigurationName is duplicated.

|The error message returned when the scaling configuration name already exists.

|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned when the specified scaling group does not exist in the current account.

|
|400

|InvalidSecurityGroupId.IncorrectNetworkType

|The network type of specified security Group does not support this action.

|The error message returned when the network types of the specified security group and scaling group are different.

|
|404

|InvalidSecurityGroupId.NotFound

|The specified security group does not exist.

|The error message returned when the specified security group does not exist in the current account.

|
|400

|InvalidSecurityGroupId.VPCMismatch

|The specified security group and the specified virtual switch are not in the same VPC.

|The error message returned when the specified security group and VSwitch are not in the same VPC.

|
|403

|InvalidSnapshot.TooOld

|This operation is denied because the specified snapshot is created before 2013-07-15.

|The error message returned when the snapshot was created on or before July 15, 2013 and cannot be called.

|
|403

|InvalidSystemDiskCategory.ValueUnauthorized

|The system disk category is not authorized.

|The error message returned when you are not authorized to create an ephemeral disk.

|
|400

|InvalidUserData.Base64FormatInvalid

|The specified parameter UserData must be base64 encoded.

|The error message returned when the specified user data is not encoded in the Base64 format.

|
|400

|InvalidUserData.SizeExceeded

|The specified parameter UserData exceeds the size.

|The error message returned when the specified user data exceeds 16 KB.

|
|403

|QuotaExceeded.EphemeralDiskSize

|Ephemeral disk size quota exceeded.

|The error message returned when the total capacity of mounted ephemeral disks exceeds 2,048 GB.

|
|400

|QuotaExceeded.ScalingConfiguration

|Scaling configuration quota exceeded in the specified scaling group.

|The error message returned when the maximum number of scaling configurations has been reached.

|
|400

|QuotaExceeded.SecurityGroupInstance

|Instance quota exceeded in the specified security group.

|The error message returned when the maximum number of ECS instances that can be added to the specified security group has been reached.

|

