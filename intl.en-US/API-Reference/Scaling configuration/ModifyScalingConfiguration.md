# ModifyScalingConfiguration {#doc_api_Ess_ModifyScalingConfiguration .reference}

You can call this operation to modify a scaling configuration. If you are modifying the name of a scaling configuration, ensure that the new name is unique within the scaling group.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=ModifyScalingConfiguration) simplifies API usage. You can use OpenAPI Explorer to perform operations such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|ScalingConfigurationId|String|Yes|asc-\*\*\*\*|The ID of the scaling configuration to be modified.

 |
|Action|String|No|ModifyScalingConfiguration|The operation that you want to perform. Set the value to ModifyScalingConfiguration.

 |
|Cpu|Integer|No|2|The number of vCPUs.

 You can specify the number of CPU cores and the amount of memory to define the range of instance types. For example, instance types with a specified value of CPU as 2 and Memory as 16 can be defined as 2 vCPU 16 GiB. Auto Scaling uses factors such as I/O optimization and zone to determine a set of available instance types. Auto Scaling then creates instances of the type that is most cost-effective out of the available types.

 **Note:** This instance type range takes effect only when cost optimization is enabled and the scaling configuration does not have a specified instance type.

 |
|DataDisk.N.Category|String|No|cloud\_ssd|The category of data disk N. Valid values:

 -   cloud: indicates a basic disk. The DeleteWithInstance property of a basic disk created along with the instance is true.
-   cloud\_efficiency: indicates an ultra disk.
-   cloud\_ssd: indicates an SSD disk.
-   ephemeral\_ssd: indicates a local SSD disk.

 Default value: cloud.

 |
|DataDisk.N.DeleteWithInstance|Boolean|No|true|Indicates whether data disk N is to be released with its attached instance. Valid values:

 -   true: Release the data disk with its attached instance.
-   false: Retain the data disk when the attached instance is released.

 Default value: true. This parameter is valid only for independent disks, for which the **DataDisk.N.Category** parameter is set to cloud, cloud\_efficiency, or cloud\_ssd. An error will be returned if you set this parameter for other disks.

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
|DataDisk.N.Size|Integer|No|100|The size of data disk N. Unit: GB. Valid values of N: 1 to 16. Valid values:

 -   cloud: 5 to 2000.
-   cloud\_efficiency: 20 to 32768.
-   cloud\_ssd: 20 to 32768.
-   ephemeral\_ssd: 5 to 800.

 If this parameter is specified, the data disk size must be greater than or equal to the size of the snapshot specified by **SnapshotId**.

 |
|DataDisk.N.SnapshotId|String|No|s-snapshot\*\*\*\*|The ID of the snapshot used to create data disk N. Valid values of N: 1 to 4. If this parameter is specified, **DataDisk.N.Size** is ignored and the size of the created disk is the size of the specified snapshot. You cannot specify a snapshot that was created on or before July 15, 2013****.

 |
|DeploymentSetId|String|No|ds-bp13v7bjnj9gis\*\*\*\*|The ID of the deployment set.

 |
|HostName|String|No|Joshu\*\*\*\*|The name of the host server where created ECS instances reside. It cannot start or end with a period \(.\) or hyphen \(-\). It cannot contain consecutive periods \(.\) or hyphens \(-\). Naming rules:

 -   Windows-based instances: It must be 2 to 15 characters in length. It can contain uppercase or lowercase letters, digits, and hyphens \(-\). It cannot contain periods \(.\) or be entirely composed of digits.
-   Other instances such as Linux-based instances: It must be 2 to 128 characters in length. It can be segments separated by periods \(.\). Each segment can contain uppercase or lowercase letters, digits, and hyphens \(-\).

 |
|ImageId|String|No|centos6u5\_64\_20G\_aliaegis\_20140703.vhd|The ID of the image file to be specified when created instances are started.

 |
|ImageName|String|No|suse11sp3\_64\_20G\_aliaegis\_20150428.vhd|The name of the image file. Image names must be unique within a region. This parameter is ignored if **ImageId****** is specified. If you specify this parameter instead of **ImageId******, the image with the specified name is used for the scaling configuration****.

 |
|InstanceName|String|No|Joshu\*\*\*\*|The name of the instance created based on the current scaling configuration.

 |
|InstanceTypes.N|RepeatList|No|ecs.t1.xsmall|The multiple instance types from which ECS instances are to be created. **InstanceType****** is ignored if this parameter is specified. Valid values of N: 1 to 10. Up to 10 instance types can be configured for a scaling configuration. N represents the priority of the instance type in the scaling configuration. A lower value of N indicates a higher priority for the instance type. If an instance of the highest priority type cannot be created, Auto Scaling will create an instance of the next highest priority type.

 |
|InternetChargeType|String|No|PayByBandwidth|The bandwidth billing type of created instances. Valid values:

 -   PayByBandwidth:**** Users pay for the maximum available bandwidth.
-   PayByTraffic: ****Users pay for the actual traffic used. The InternetMaxBandwidthOut parameter only specifies the upper limit of available bandwidth when this parameter is specified.

 Default value: PayByBandwidth for classic networks or PayByTraffic for VPCs.

 |
|InternetMaxBandwidthOut|Integer|No|50|The maximum outbound bandwidth to the public network. Unit: Mbit/s. Valid values: 1 to 100.

 -   If InternetChargeType is set to PayByBandwidth and this parameter is not specified, this parameter is automatically set to 0.
-   If InternetChargeType is set to PayByTraffic and this parameter is not specified, an error is returned.

 |
|IoOptimized|String|No|none|Indicates whether created instances are I/O optimized. Valid values:

 -   none
-   optimized

 The value of this parameter is none if **InstanceType** is set to an instance type which has been phased out.

 The value of this parameter is optimized if **InstanceType** is set to an instance types later than Generation I.

 |
|KeyPairName|String|No|null|The name of the key pair.

 -   Ignore this parameter if you are creating a Windows-based ECS instance. This parameter is null by default.
-   Password logon is disabled for Linux-based ECS instances by default.

 |
|LoadBalancerWeight|Integer|No|50|The weight of the back-end server. Valid values: 0 to 100. Default value: 50.

 |
|Memory|Integer|No|16|The size of memory.

 You can specify the number of CPU cores and the amount of memory to define the range of instance types. For example, instance types with a specified value of CPU as 2 and Memory as 16 can be defined as 2 vCPU 16 GiB. Auto Scaling uses factors such as I/O optimization and zone to determine a set of available instance types. Auto Scaling then creates instances of the type that is most cost-effective out of the available types.

 **Note:** This instance type range takes effect only when cost optimization is enabled and the scaling configuration does not have a specified instance type.

 |
|Override|Boolean|No|true|Indicates whether to overwrite the existing data. Valid values:

 -   true
-   false

 |
|PasswordInherit|Boolean|No|false|Indicates whether to use the preconfigured password of the specified image. To use this parameter, ensure that a password is configured for the specified image.

 |
|RamRoleName|String|No|RamRoleTest|The name of the instance RAM role. This name is provided and maintained by RAM. Call [ListRoles](~~28713~~) to query the list of RAM role names. For more information, see [CreateRole](~~28710~~).

 |
|ResourceGroupId|String|No|abcd1234abcd\*\*\*\*|The ID of the resource group.

 |
|ScalingConfigurationName|String|No|test-modify|The new name of the scaling configuration. It must be 2 to 40 characters in length. It must start with a digit, uppercase letter, or lowercase letter. It can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). Scaling configuration names must be unique within a scaling group. If this parameter is not specified, the value of ScalingConfigurationId is used.

 |
|SecurityGroupId|String|No|sg-F876F\*\*\*\*|The ID of the security group.

 |
|SpotPriceLimit.N.InstanceType|String|No|ecs.t1.small|The instance type of preemptible instance N. Valid values of N: 1 to 10.

 This parameter takes effect only when the SpotStrategy parameter is set to SpotWithPriceLimit.

 |
|SpotPriceLimit.N.PriceLimit|Float|No|0.125|The price limit of preemptible instance N. Valid values of N: 1 to 10. This parameter takes effect only when the **SpotStrategy** parameter is set to SpotWithPriceLimit.

 |
|SpotStrategy|String|No|NoSpot|The preemption policy to be used for pay-as-you-go instances. It takes effect only when the **InstanceChargeType** parameter is set to PostPaid. Valid values:

 -   NoSpot: indicates a pay-as-you-go instance.
-   SpotWithPriceLimit: indicates a preemptible instance with a maximum price.
-   SpotAsPriceGo: indicates an instance with its price based on the market price at the time of purchase.

 Default value: NoSpot.

 |
|SystemDisk.Category|String|No|cloud\_efficiency|The type of the system disk. Valid values:

 -   cloud: indicates a basic disk.
-   cloud\_efficiency: indicates an ultra disk.
-   cloud\_ssd: indicates an SSD disk.
-   ephemeral\_ssd: indicates a local SSD disk.

 ****Default value: cloud for Generation I type instances that are not I/O optimized, and cloud\_efficiency for other types.

 |
|SystemDisk.Description|String|No|FinanceDept|The description of the system disk. It must be 2 to 256 characters in length and cannot start with "http://" or "https://."

 |
|SystemDisk.DiskName|String|No|cloud\_ssdSystem|The name of the system disk. It must be 2 to 128 characters in length. It must start with a letter and cannot start with "http://" or "https://." It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). Default value: null.

 |
|SystemDisk.Size|Integer|No|50|The size of the system disk. Unit: GB. Valid values:

 -   cloud: 40 to 500.
-   cloud\_efficiency: 40 to 500.
-   cloud\_ssd: 40 to 500.
-   ephemeral\_ssd: 40 to 500.

 Default value: the greater value out of ImageSize and 40. The specified value must be greater than or equal to the default value.

 |
|Tags|String|No|“key1”:”value1”|The tags of the instance. Tags must be specified as key-value pairs. Up to five tags in the \{“key1”:”value1”,”key2”:”value2”, … “key5”:”value5”\} format can be specified. Requirements for keys and values:

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

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://[Endpoint]/? Action=ModifyScalingConfiguration
&ScalingConfigurationId=asc-****
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyScalingConfigurationResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</ModifyScalingConfigurationResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"requestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
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
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned when you are not authorized to perform the specified operation.

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
|404

|InvalidImageId.NotFound

|The specified image does not exist.

|The error message returned when the specified image does not exist.

|
|400

|InvalidKeyPairName.NotFound

|The specified KeyPairName does not exist in our records.

|The error message returned when the specified key pair name does not exist.

|
|400

|InvalidNetworkType.ForRAMRole

|RAMRole can’t be used For classic instance.

|The error message returned when the network type of the instance is classic network and does not support the RamRoleName parameter.

|
|400

|InvalidParamter

|The specified value of parameter is not valid.

|The error message returned when the specified parameter value is invalid.

|
|400

|InvalidScalingConfigurationName.Duplicate

|The specified value of parameter is duplicated.

|The error message returned when the specified scaling configuration name already exists.

|
|400

|InvalidSecurityGroupId.IncorrectNetworkType

|The network type of specified Security Group does not support this action.

|The error message returned when the network types of the specified security group and scaling group are different.

|
|400

|InvalidSecurityGroupId.VPCMismatch

|The specified security group and the specified virtual switch are not in the same VPC.

|The error message returned when the specified security group and VSwitch are not in the same VPC.

|
|400

|InvalidTags.KeyValue

|The specified tags key/value cannot be empty.

|The error message returned when the Tags parameter is not specified.

|
|400

|InvalidTags.ListSize

|The specified tags list size cannot be more than “5”.

|The error message returned when the length of the Tags list exceeds the limit.

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

