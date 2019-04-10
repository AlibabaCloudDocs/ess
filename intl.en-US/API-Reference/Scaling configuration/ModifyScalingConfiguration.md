# ModifyScalingConfiguration {#concept_ohp_tc2_sfb .concept}

You can call this operation to modify a specified scaling configuration. When you modify the name of a scaling configuration, ensure that the name is different from the existing names of scaling configurations in a scaling group.

## Request parameters {#section_a2k_dp2_sfb .section}

|Name|Type|Required|Description|
|----|----|--------|-----------|
|Action|String|Yes|The operation that you want to perform. Set the value to ModifyScalingConfiguration.|
|ScalingConfigurationName|String|No|The name of the scaling configuration. The name is a combination of 2 to 40 characters including Chinese characters, numbers, uppercase letters, lowercase letters, underscores \(\_\), hyphens \(-\), and periods \(.\). Additionally, the name must start with a number, letter, or Chinese character. The name must be unique in a scaling group that is located in a region of an account. If you do not specify the parameter, the ID of the scaling configuration is specified as the name by default.|
|InstanceName|String|No|The name of the ECS instance that is created based on the current scaling configuration.|
|HostName|String|No| The hostname of the ECS instance. The name cannot start or end with a period \(.\) or hyphen \(-\). Additionally, a period cannot be next another period and a hyphen cannot be next to another hyphen. The naming rules for various types of instances are described as follows:

 -   For Windows instances: The length of a hostname ranges from 2 to 15 characters. The hostname is a combination of characters including uppercase and lowercase letters, numbers, and hyphens \(-\), excluding periods \(.\). Additionally, the hostname cannot consist of all numbers.
-   For other instances, such as Linux instances: The length of a hostname ranges from 2 to 128 characters. Separate the hostname with periods \(.\). Characters between two periods \(.\) form a segment. Each segment is a combination of characters including uppercase and lowercase letters, numbers, and hyphens \(-\).

 |
|ImageId|String|No|The ID of the image file. Specifies the image resource for an instance when you start the instance.|
|ImageName|String|No|The name of the image file. The name must be unique in a region. If you specify the ImageId, the ImageName is not used. If you specify the ImageName rather than the ImageId, the ImageName is used by the current scaling configuration to identify an image file.|
|ScalingConfigurationId|String|Yes|The ID of the scaling configuration. Specifies the scaling configuration to be modified.|
|InternetChargeType|String|No| The billing method. Valid values:

 -   PayByBandwidth: indicates that you pay by bandwidth. In this case, the InternetMaxBandwidthOut is the specified bandwidth.
-   PayByTraffic: indicates that you pay by traffic. In this case, the InternetMaxBandwidthOut is the upper limit of the bandwidth. You pay for the amount of data that you use.

 If you do not specify the parameter, the default value is PayByBandwidth in a classic network, while the default value is PayByTraffic in a VPC network.

 |
|InternetMaxBandwidthOut|Integer|No| The maximum outgoing bandwidth for the public network. Unit: Mbit/s. Valid values:

 -   PayByBandwidth: 1 to 100. If you do not specify the parameter, the outgoing bandwidth is set to 0 Mbit/s
-   PayByTraffic: 1 to 100. If you do not specify the parameter, an error occurs.

 |
|SystemDisk.Category|String|No| The types of the system disk. Valid values:

 -   cloud: basic disks.
-   cloud\_efficiency: ultra disks.
-   cloud\_ssd: SSDs.
-   ephemeral\_ssd: local SSDs.

 If the specification of the InstanceType is series I and the instance is not I/O optimized, the default value is cloud. Otherwise, the default value is cloud\_efficiency.

 |
|SystemDisk.Size|Integer|No| The size of the system disk. Unit: GB. Valid values:

 -   cloud: 40 to 500.
-   cloud\_efficiency: 40 to 500.
-   cloud\_ssd: 40 to 500.
-   ephemeral\_ssd: 40 to 500.

 Default value: max\{40, ImageSize\}. After you specify the parameter, the size of the system disk must be equal to or greater than max\{40, ImageSize\}.

 |
|LoadBalancerWeight|Integer|No|The weight of the backend server. Valid values: 0 to 100. Default value: 50.|
|UserData|String|No|The custom data of the instance. The data is encoded by Base64. The size of the initial data is 16 KB.|
|KeyPairName|String|No| The name of the key pair.

 -   For Windows ECS instances, the parameter is empty by default and is not used.
-   For Linux ECS instances, the logon method with a password is disabled by the initialization process.

 |
|RamRoleName|String|No|The RAM role of the instance. The role is provided and maintained by RAM. You can call the [ListRoles](../../../../../reseller.en-US/API Reference/Role management APIs/ListRoles.md#) operation to query roles. For more information, see [CreateRole](../../../../../reseller.en-US/API Reference/Role management APIs/CreateRole.md#).|
|InstanceTypes.N|String|No|Includes one or more types of instances specifications. If you specify the InstanceTypes.N, the InstanceType is not used. Valid values of N: 1 to 10. Namely, you can specify up to 10 instance specifications in a scaling configuration. N is a number that represents the priority of an instance specification in the current scaling configuration. The instance specification with the number 1 indicates the highest priority. The priority decreases along with the increasing number. When an instance cannot be created based on an instance specification with a high priority, Auto Scaling creates the instance using an instance specification with the next highest level of priority.|
|Tags|String|No| The tags of the instance. A tag is a key-value pair. You can specify up to five sets of tags. The format is: \{“key1”:”value1”,”key2”:”value2”, … “key5”:”value5”\}. Keys and values are required to follow these rules:

 -   The length of a key is up to 64 characters. A key cannot start with a string including aliyun, http://, and https://. You cannot specify an empty string for a key.
-   The length of a value is up to 128 characters. A value cannot start with a string including aliyun, http://, and https://. You can specify an empty string for a value.

 |
|PasswordInherit|Boolean|No|Indicates whether you can use a password pre-defined by an image. When you specify the parameter, ensure that the selected image has a pre-defined password.|
|IoOptimized|String|No| Indicates whether the instance is I/O optimized. Valid values:

 -   none: not I/O optimized.
-   optimized: I/O optimized.

 When the instance specification defined by the InstanceType parameter is in out-of-sale, the default value is none.

 When the instance specification specified by InstanceType is not series I, the default value is optimized.

 |
|SpotStrategy|String|No| The preemptible type of postpaid instances. When the value of InstanceChargeType is PostPaid, the parameter is valid. Valid values:

 -   NoSpot: normal Pay-As-You-Go instances.
-   SpotWithPriceLimit: preemptible instances that are specified with the maximum price.
-   SpotAsPriceGo: the price is automatically set based on the current market price.

 Default value: NoSpot.

 |
|SpotPriceLimit.N.InstanceType|String|No|The instance specification of the preemptible instance. Valid values of N: 1 to 10. When the value of SpotStrategy is SpotWithPriceLimit, the parameter is valid.|
|SpotPriceLimit.N.PriceLimit|Float|No|The corresponding price of the preemptible instance. Valid values of N: 1 to 10. When the value of SpotStrategy is SpotWithPriceLimit, the parameter is valid.|
|DataDisk.N.Category|String|No| The disk type of the data disk N. Valid values:

 -   cloud: basic disks. For a basic disk that is created along with the creation of an instance, the value of the disk's DeleteWithInstance property is true.
-   cloud\_efficiency: ultra disks.
-   cloud\_ssd: SSDs.
-   ephemeral\_ssd: local SSDs.

 Default value: cloud.

 |
|DataDisk.N.Size|Integer|No| The size of the data disk N. Unit: GB. Valid values of N: 1 to 16. Valid values:

 -   cloud: 5 to 2000.
-   cloud\_efficiency: 20 to 32768.
-   cloud\_ssd: 20 to 32768.
-   ephemeral\_ssd: 50 to 800.

 After you specify the parameter, the size of the disk must be equal to or greater than the size of the snapshot. The snapshot is specified by the SnapshotId parameter.

 |
|DataDisk.N.SnapshotId|String|No|The snapshot that is used to create the data disk. Valid values of N: 1 to 4. After you specify the parameter, the DataDisk.N.Size parameter is not used. The actual size of the created disk is equal to the size of the specified snapshot. If the snapshot was created on or before Jul 15, 2013, this call will be rejected. Up to four pieces of InvalidSnapshot.TooOld can be included in a response parameter.|
|DataDisk.N.Device|String|No|The mount point of the data disk. Valid values of N: 1 to 4. If you do not specify the parameter, ECS allocates a mount point to an automatically created ECS instance by default. The name of the mount point ranges from /dev/xvdb to /dev/xvdz in alphabetical order.|
|DataDisk.n.DeleteWithInstance|Boolean|No| Indicates whether the data disk is released along with the instance. Valid values:

 -   true: When you release the instance, the data disk will also be released.
-   false: When you release the instance, the data disk will not be released.

 Default value: true. You can only specify the parameter for independent disks, which means that the value of the DataDisk.n.Category parameter is cloud, cloud\_efficiency, or cloud\_ssd. Otherwise, an error occurs.

 |

## Response parameters {#section_jzw_252_sfb .section}

|Name|Type|Description|
|----|----|-----------|
|RequestId|String|The GUID generated by Alibaba Cloud for the request.|

## Examples {#section_oyq_352_sfb .section}

Sample requests

```
http://ess.aliyuncs.com/?Action=ModifyScalingConfiguration
&ScalingConfigurationId=asc-xxxxxxxxxxxxxx
&ScalingConfigurationName=test-modify
&ImageId=centos6u5_64_20G_aliaegis_20140703.vhd 
& <Common request parameters>
```

Successful response examples

`XML` format

```
<ModifyScalingConfigurationResponse> 
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyScalingConfigurationResponse>
```

`JSON` format

```
{
    "requestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## Error codes {#section_kkw_s52_sfb .section}

For more information about common errors, see [Client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [Server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|The error message returned when you have not been authorized to perform the Action.|
|404|InvalidDataDiskSnapshotId.NotFound|Snapshot “XXX” does not exist.|The error message returned when the specified snapshot does not exist.|
|400|InvalidDataDiskSnapshotId.SizeNotSupported|The capacity of snapshot “XXX” exceeds the size limit of the specified disk category.|The error message returned when the size of the snapshot exceeds the maximum size of the disk.|
|404|InvalidImageId.NotFound|The specified image does not exist.|The error message returned when the specified ImageId does not exist.|
|400t|InvalidKeyPairName.NotFound|The specified KeyPairName does not exist in our records.|The error message returned when the specified KeyPairName does not exist.|
|400|InvalidNetworkType.ForRAMRole|RAMRole can’t be used For classic instance.|The error message returned when you specify theRamRoleName parameter for an instance in a classic network.|
|400|InvalidParamter|The specified value of parameter is not valid.|The error message returned when the value of the specified parameter is invalid.|
|400|InvalidScalingConfigurationName.Duplicate|The specified value of parameter is not valid.|The error message returned when the name of the scaling configuration exists.|
|400|InvalidSecurityGroupId.IncorrectNetworkType|The network type of specified Security Group does not support this action.|The error message returned when the network type of the specified security group is different from that of the specified scaling group.|
|400|InvalidSecurityGroupId.VPCMismatch|The specified security group and the specified virtual switch are not in the same VPC.|The error message returned when the specified security group and the VSwitch are not in the same VPC.|
|400|InvalidTags.KeyValue|The specified tags key/value cannot be empty.|The error message returned when the Tags parameter is empty.|
|400|InvalidTags.ListSize|The specified tags list size cannot be more than “5”.|The error message returned when the length of the Tags list exceeds the specified length.|
|400|InvalidUserData.Base64FormatInvalid|The specified parameter UserData must be base64 encoded.|The error message returned when the UserData does not conform to Base64 encoding.|
|400|InvalidUserData.SizeExceeded|The specified parameter UserData exceeds the size.|The error message returned when the length of the UserData exceeds the specified size.|

