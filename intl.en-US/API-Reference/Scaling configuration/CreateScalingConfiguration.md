# CreateScalingConfiguration {#concept_25944_zh .concept}

This interface creates a scaling configuration.

## Request parameters {#section_qhk_hfk_sfb .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|Operation interface, required. The parameter value is CreateScalingConfiguration.|
|ScalingGroupId|String|Yes|ID of the scaling group of a scaling configuration.|
|ImageId|String|No|ID of an image file, indicating the image resource selected when an instance is enabled.|
|ImageName|String|No|Name of an image file. An image name is unique within a region. If ImageId is set, ImageName is ignored. You cannot specify a marketplace image by ImageName.|
|InstanceType|String|Yes|Resource type of an ECS instance.|
|SecurityGroupId|String|Yes|ID of the security group to which a newly created instance belongs. Mutual access is allowed between instances in one security group.|
|ScalingConfigurationName|String|No|Name shown for the scheduled task. The name must contain 2-40 English or Chinese characters, and start with a number, a letter in upper or lower case or a Chinese character. The name can contain numbers, “\_“, “-“ or “.”. The account name in the same scaling group is unique in the same region. If this parameter value is not specified, the default value is ScalingConfigurationId.|
|InternetChargeType|String|No|Network billing type. Values: -   PayByBandwidth: The users are charged by bandwidth and the bandwidth is specified by InternetMaxBandwidthOut.
-   PayByTraffic: The users are charged by traffic and InternetMaxBandwidthOut only specifies the upper limit of bandwidth. The users need to pay according to the actual traffic.

If this parameter value is not specified, the default value is PayByBandwidth in classic network and PayByTraffic in VPC separately.|
|InternetMaxBandwidthIn|Integer|No|Maximum incoming bandwidth from the public network, measured in Mbps \(Mega bit per second\). The value range is \[1,200\]. If this parameter value is not specified, AliyunAPI automatically sets the value to 200 Mbps. This is for free in any cases. The inbound traffic of your instance is not billed.|
|InternetMaxBandwidthOut|Integer|No|Maximum outgoing bandwidth from the public network, measured in Mbps \(Mega bit per second\). The value range -   for PayByBandwidth is \[0,100\]. If this parameter value is not specified, AliyunAPI automatically sets the value to 0 Mbps.
-   The value range for PayByTraffic is \[0,100\]. If this parameter value is not specified, an error is reported.

 |
|IoOptimized|String|No|Whether the instance is I/O optimized or not. For non I/O optimized instance, IoOptimized is not an available parameter. Optional values: -   optimized: The specified instance is I/O optimized.
-   When IoOptimized is not available,
    -   instances of generation I instance types are non I/O optimized by default.
    -   instances of non generation I instance types are I/O optimized by default.

 |
|SystemDisk.Category|String|No|Category of the system disk. Optional values: -   cloud: Common cloud disk
-   cloud\_efficiency: Efficient cloud disk
-   cloud\_ssd: SSD cloud disk
-   ephemeral\_ssd: Local SSD disk

The default value is cloud for instances of generation I instance types \(non I/O optimized\) and cloud\_efficiency for other types.|
|SystemDisk.Size|Integer|No|Size of system disk, in GiB. Optional values: -   cloud: 40-500
-   cloud\_efficiency: 40-500
-   cloud\_ssd: 40-500
-   ephemeral\_ssd: 40-500

The default value is \{40, ImageSize\}. If SystemDisk.Size is set, the system disk size must be greater than or equal to max\{40, ImageSize\}.|
|DataDisk.n.Category|String|No|Category of data disk n. The value range of n is \[1, 16\]. Optional values: -   cloud: Common cloud disk. The DeleteWithInstance property of a common cloud disk that is created along with the instance is true.
-   cloud\_efficiency: Efficient cloud disk
-   cloud\_ssd: SSD cloud disk
-   ephemeral\_ssd: Local SSD disk

 The default value is cloud.|
|DataDisk.n.Size|Integer|No|Size of data disk n, in GiB. Optional values: -   cloud: 5-2,000
-   cloud\_efficiency: 20-32,768
-   cloud\_ssd: 20-32,768
-   ephemeral\_ssd: 5-800

If DataDisk.n.Size is set, the data disk size must be greater than or equal to the snapshot size \(use SnapshotId to specify the snapshot\).|
|DataDisk.n.SnapshotId|String|No|Snapshot used for creating the data disk n. If this parameter is specified, the DataDisk.n.Size parameter is neglected, and the size of the created disk is the size of the snapshot. If this snapshot is created before July 15, 2013 \(included\), the snapshot cannot be called, and InvalidSnapshot.TooOld is returned in Response.|
|DataDisk.n.DeleteWithInstance|Boolean|No|Whether the data disk will be released along with the instance. Optional values: -   true: Release the data disk along with the instance.
-   false: Retain the data disk when you release the instance.

Default value: true DataDisk.n.DeleteWithInstance is valid only for independent cloud disks, for which the parameter DataDisk.n.Category is set to cloud, cloud\_efficiency or cloud\_ssd. Otherwise, an error returns.|
|LoadBalancerWeight|Integer|No|The weight of the backend server, the value range is \[0, 100\] and the default value is 50.|
|UserData|String|No|The user-defined data of the instance. The UserData of an instance must be encoded in Base64 format. The maximum size of the raw data is 16 KB.|
|KeyPairName|String|No|Key pair name. -   If a Windows ECS instance is being created, ignore this parameter. By default, no value is set.
-   The user password authentication method will be disabled during the initialization of a Linux instance.

 |
|RamRoleName|String|No|The name of the instance RAM role. You can query the name of an instance RAM role by using the RAM API [ListRoles](../../../../reseller.en-US/API reference/API reference (RAM)/Role Management Interface/ListRoles.md#) . You can also see the API [CreateRole](../../../../reseller.en-US/API reference/API reference (RAM)/Role Management Interface/CreateRole.md#) for more information.|
|Tags|String|No|The tags of an instance. You should input the information of the tag with the format of the Key-Value, such as \{“key1”:”value1”,”key2”:”value2”, … “key5”:”value5”\}. At most 5 tags can be specified. Key: -   It can be up to 64 characters in length. It cannot begin with aliyun. It cannot begin with http:// or https://. It cannot be a null string.
-   Value: It can be up to 128 characters in length. It cannot begin with aliyun. It cannot begin with http:// or https://. It can be a null string.

 |
|InstanceTypes.N|String|No|Multiple instance types InstanceType will be ignored if InstanceTypes.N is applied. N ranges from 1 to 10, which means one scaling configuration can contain up to 10 instance types. N is the priority of each instance type in your scaling configuration and 1 means the highest. In other words, the greater the number is, the lower the priority of instance type is. If you cannot launch an instance from the instance type with the relatively higher priority, the system will automatically use the instance type a level lower.|
|InstanceName|String|No|The name of the instance launched from the current scaling configuration.|
|HostName|String|No|Host name of the ECS instance. It cannot start or end with a period \(.\) or a hyphen \(-\). It cannot have two or more consecutive periods \(.\) or hyphens \(-\). Naming requirements: -   For Windows instances: It can be \[2, 15\] characters in length. It can contain uppercase or lowercase letters, digits, periods \(.\), and hyphens \(-\). It cannot be all digits.
-   For other instances, such as Linux instances: It can be \[2, 64\] characters in length. It can be segments separated by periods \(.\). It can contain uppercase or lowercase letters, digits, and hyphens \(-\).

 |
|PasswordInherit|Boolean|No|Whether to use the password pre-configured in the image you select or not. For a secure access, make sure that the selected image has password configured.|
|SpotStrategy|String|No|The spot price you are willing to accept for a preemptible instance. It takes effect only when parameter InstanceChargeType is PostPaid. Optional values: -   NoSpot: A normal Pay-As-You-Go instance.
-   SpotWithPriceLimit: Sets the price threshold for a preemptible instance.
-   SpotAsPriceGo: A price that is based on the highest Pay-As-You-Go instance.

Default value: NoSpot|
|SpotPriceLimit.N.InstanceType|String|No|The instance type for a preemptible instance \(N ranges from 1 to 10\), and it takes effect only when parameter SpotStrategy is SpotWithPriceLimit.|
|SpotPriceLimit.N.PriceLimit|Float|No|The hourly price threshold for a preemptible instance \(N ranges from 1 to 10\), and it takes effect only when parameter SpotStrategy is SpotWithPriceLimit.|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|ScalingConfigurationId|String|ID of a scaling configuration. It is generated by the system and is globally unique.|

## Request example { .section}

```
http://ess.aliyuncs.com/?Action=CreateScalingConfiguration
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&SecurityGroupId=sg-280ih3w4b
&ImageId=centos6u5_64_20G_aliaegis_20140703.vhd
&InstanceType=ecs.t1.xsmall
&<Public Request Parameters>
```

## Response example { .section}

XML format:

```
<CreateScalingConfigurationResponse>
    <ScalingConfigurationId>eOs27Kb0oXvQcUYjEGelJqUy</ScalingConfigurationId>
    <RequestId>5CC0AD41-08ED-4559-A683-6F56355FE068</RequestId>
</CreateScalingConfigurationResponse>
```

JSON format:

```
{
    "RequestId": "5CC0AD41-08ED-4559-A683-6F56355FE068",
    "ScalingConfigurationId": "eOs27Kb0oXvQcUYjEGelJqUy",
}
```

## Error codes { .section}

For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|Error code|Error message|HTTP status code|Description|
|:---------|:------------|:---------------|:----------|
|InstanceType.Mismatch|The specified scaling configuration and existing active scaling configuration have different instance type.|400|The specified scaling configuration and the existing scaling configuration have different instance types.|
|InvalidDataDiskSnapshotId.NotFound|Snapshot “XXX” does not exist.|404|Specified snapshot does not exist.|
|InvalidDataDiskSnapshotId.SizeNotSupported|The capacity of snapshot “XXX” exceeds the size limit of the specified disk category.|400|Capacity of the specified snapshot exceeds the upper limit of the disk size.|
|InvalidDevice.InUse|Device “XXX” has been occupied.|403|Data disk attaching point has been occupied.|
|InvalidImageId.InstanceTypeMismatch|The specified image does not support the specified instance type.|400|Specified image does not support the specified instance type.|
|InvalidImageId.NotFound|The specified image does not exist.|404|Specified image is not in this account.|
|InvalidKeyPairName.NotFound|The specified KeyPairName does not exist in our records.|400|The specified KeyPairName does not exist.|
|InvalidNetworkType.ForRAMRole|RAMRole can't be used For classic instance.|400|The RamRoleName is only applicable to VPC instances.|
|InvalidParameter|The specified value of parameter `KeyPairName` is not valid.|400|The parameter `KeyPairName` is only valid for a Windows instance.|
|InvalidParameter.Conflict|The value of parameter `SystemDisk.Category` and parameter `DataDisk.N.Category` are conflict.|400|Type of the specified system disk conflicts with that of the data disk.|
|InvalidRamRole.NotFound|The specified RamRoleName does not exist.|400|The specified RAM role name does not exist.|
|InvalidScalingConfigurationName.Duplicate|The specified value of parameter `ScalingConfigurationName` is duplicated.|400|The scaling configuration name already exists.|
|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|404|The specified scaling group does not exist in this account.|
|InvalidSecurityGroupId.IncorrectNetworkType|The network type of specified security Group does not support this action.|400|Specified network type is inconsistent for the specified security group and the scaling group.|
|InvalidSecurityGroupId.NotFound|The specified security group does not exist.|404|Specified security group is not in this account.|
|InvalidSecurityGroupId.VPCMismatch|The specified security group and the specified virtual switch are not in the same VPC.|400|The specified security group and the virtual switch are not in the same VPC.|
|InvalidSnapshot.TooOld|This operation is denied because the specified snapshot is created before 2013-07-15.|403|The snapshot is created before July 15, 2013 \(included\), and thus cannot be called.|
|InvalidSystemDiskCategory.ValueUnauthorized|The system disk category is not authorized.|403|You are unauthorized to create an ephemeral system disk.|
|InvalidUserData.Base64FormatInvalid|The specified parameter UserData must be base64 encoded.|400|The specified UserData should be encoded in Base64 format.|
|InvalidUserData.SizeExceeded|The specified parameter UserData exceeds the size.|400|The size of the specified UserData exceeds 16 KB.|
|QuotaExceeded.EphemeralDiskSize|Ephemeral disk size quota exceeded.|403|Ephemeral disk capacity exceeds 2 TB \(2,048 GB\).|
|QuotaExceeded.ScalingConfiguration|Scaling configuration quota exceeded in the specified scaling group.|400|Scaling configuration quantity exceeds the upper limit for a user to use.|
|QuotaExceeded.SecurityGroupInstance|Instance quota exceeded in the specified security group.|400|The number of ECS instances attached to the specified security group exceeds the upper limit.|

