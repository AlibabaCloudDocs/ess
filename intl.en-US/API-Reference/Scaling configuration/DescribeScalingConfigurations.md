# DescribeScalingConfigurations {#doc_api_Ess_DescribeScalingConfigurations .reference}

You can call this operation to query scaling configurations.

## Debugging {#api_explorer .section}

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeScalingConfigurations&type=RPC&version=2014-08-28)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|RegionId|String|Yes|cn-qingdao|The region ID of the scaling group to which a scaling configuration belongs.

 |
|Action|String|No|DescribeScalingConfigurations|The operation that you want to perform. Set the value to DescribeScalingConfigurations.

 |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

 Default value: 1.

 |
|PageSize|Integer|No|50|The number of entries to return on each page. Maximum value: 50.

 Default value: 10.

 |
|ScalingConfigurationId.1|String|No|bU5uZHcAgtzwcL4IeDea\*\*\*\*|The ID of scaling configuration N to be queried. Valid values of N: 1 to 10. The IDs of active and inactive scaling configurations are displayed in the query result, and can be differentiated by LifecycleState.

 |
|ScalingConfigurationName.1|String|No|c1908dd1-690f-4c9b-ab73-350f1f06\*\*\*\*|The name of scaling configuration N to be queried. Valid values of N: 1 to 20. The names of inactive scaling configurations will not be displayed in the query result and no errors will be returned.

 |
|ScalingGroupId|String|No|dE9YbOdCHqaFdFZHXVdD\*\*\*\*|The ID of the scaling group. You can query all scaling configurations in the scaling group.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The current page number.

 |
|PageSize|Integer|50|The number of entries returned on each page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request.

 |
|ScalingConfigurations| | |The set of scaling configurations.

 |
|Cpu|Integer|2|The number of vCPUs.

 You can specify the number of vCPUs and the amount of memory to define the range of instance types. For example, to specify instances that have 2 vCPUs and 16 GiB memory, set the value of Cpu to 2 and the value of Memory to 16. Auto Scaling uses factors such as I/O optimization and zone to determine a set of available instance types. Auto Scaling then creates instances of the type that is most cost-effective out of the available types.

 **Note:** This instance type range takes effect only when cost optimization is enabled and you have not specified an instance type in the scaling configuration.

 |
|CreationTime|String|2014-08-14T10:58Z|The time when a scaling configuration was created.

 |
|DataDisks| | |The set of data disks.

 |
|Category|String|cloud|The disk type of a data disk. Valid values:

 -   cloud: basic disk The DeleteWithInstance attribute of a basic disk created along with the instance is true.
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   ephemeral\_ssd: local SSD
-   cloud\_essd: enhanced SSD

 |
|DeleteWithInstance|Boolean|true|Indicates whether the data disk will be released with the instance. Valid values:

 -   true: releases the data disk when the instance is released.
-   false: retains the data disk when the instance is released.

 |
|Description|String|FinanceDept|The description of the data disk.

 |
|Device|String|/dev/xvdb|The mount point of the data disk.

 |
|DiskName|String|cloud\_ssdData|The name of the data disk.

 |
|Encrypted|String|false|Indicates whether the data disk is encrypted. Valid values:

 -   true: The disk is encrypted.
-   false: The disk is not encrypted.

 |
|KMSKeyId|String|0e478b7a-4262-4802-b8cb-00d3fb40826X|The ID of the KMS key corresponding to the data disk.

 |
|Size|Integer|200|The size of the data disk. Unit: GiB Valid values:

 -   cloud: 5 to 2000
-   cloud\_efficiency: 20 to 32768
-   cloud\_ssd: 20 to 32768
-   ephemeral\_ssd: 5 to 800

 |
|SnapshotId|String|s-23f2i\*\*\*\*|The ID of the snapshot used to create data disks.

 |
|DeploymentSetId|String|ds-bp1frxuzdg87zh4p\*\*\*\*|The ID of the deployment set to which an ECS instance belongs.

 |
|HostName|String|LocalHost|The hostname of an ECS instance.

 |
|HpcClusterId|String|hpc-clusterid|The ID of the Elastic HPC cluster to which an ECS instance belongs.

 |
|ImageId|String|centos6u5\_64\_20G\_aliaegis\_20140703.vhd|The ID of the image file used to automatically create an instance.

 |
|ImageName|String|centos6u5\_64\_20G\_aliaegis\_20140703.vhd|The name of the image file.

 |
|InstanceDescription|String|FinaceDept|The description of an ECS instance.

 |
|InstanceGeneration|String|ecs-3|The generation of an ECS instance.

 |
|InstanceName|String|fortest|The name of an ECS instance.

 |
|InstanceType|String|ecs.t1.xsmall|The type of an ECS instance.

 |
|InstanceTypes| |ecs.t1.xsmall|The set of ECS instance types.

 |
|InternetChargeType|String|PayByTraffic|The bandwidth billing method of created instances. Valid values:

 -   PayByTraffic: You pay for the actual traffic used. The InternetMaxBandwidthOut parameter only specifies the upper limit of available bandwidth when this parameter is specified.

 |
|InternetMaxBandwidthIn|Integer|200|The maximum inbound bandwidth from the public network. Unit: Mbit/s. Valid values: 1 to 200.

 |
|InternetMaxBandwidthOut|Integer|0|The maximum outbound bandwidth to the public network. Unit: Mbit/s. Valid values: 0 to 100.

 -   If InternetChargeType is set to PayByTraffic and this parameter is not specified, an error is returned.

 |
|IoOptimized|String|none|Indicates whether the instance is I/O optimized.

 |
|KeyPairName|String|fortest|The name of the key pair used to log on to an ECS instance.

 |
|LifecycleState|String|Active|The state of the scaling configuration in a scaling group. Valid values:

 -   Active: Active scaling configurations are used by a scaling group to automatically create ECS instances.
-   Inactive: Inactive scaling configurations are still retained in a scaling group, but are not used by the group to create ECS instances.

 |
|LoadBalancerWeight|Integer|1|The weight of the backend server. Valid values: 0 to 100.

 |
|Memory|Integer|16|The size of memory.

 You can specify the number of vCPUs and the amount of memory to define the range of instance types. For example, to specify instances that have 2 vCPUs and 16 GiB memory, set the value of Cpu to 2 and the value of Memory to 16. Auto Scaling uses factors such as I/O optimization and zone to determine a set of available instance types. Auto Scaling then creates instances of the type that is most cost-effective out of the available types.

 **Note:** This instance type range takes effect only when cost optimization is enabled and you have not specified an instance type in the scaling configuration.

 |
|PasswordInherit|Boolean|true|Indicates whether the password predefined in the specified image is used.

 |
|RamRoleName|String|RamRoleTest|The name of the instance RAM role. This name is provided and maintained by RAM. You can call the [ListRoles](~~28713~~) operation to query the list of RAM role names. For more information about how to create a RAM role, see [CreateRole](~~28710~~).

 |
|ResourceGroupId|String|abcd1234abcd\*\*\*\*|The ID of the resource group to which an ECS instance belongs.

 |
|ScalingConfigurationId|String|bU5uZHcAgtzwcL4IeDea\*\*\*\*|The ID of the scaling configuration.

 |
|ScalingConfigurationName|String|c1908dd1-690f-4c9b-ab73-350f1f06\*\*\*\*|The name of the scaling configuration.

 |
|ScalingGroupId|String|sg-280ih\*\*\*\*|The ID of the scaling group to which the scaling configuration belongs.

 |
|SecurityEnhancementStrategy|String|Active|Indicates whether security hardening is enabled. Valid values:

 -   Active: enables security hardening for public images.
-   Deactive: disables security hardening for all images.

 |
|SecurityGroupId|String|sg-280ih\*\*\*\*|The ID of the security group to which an ECS instance belongs. ECS instances in the same security group can access each other.

 |
|SecurityGroupIds| |sg-bp18kz60mefs\*\*\*\*|The IDs of the security groups to which an ECS instance belongs. ECS instances in the same security group can access each other.

 |
|SpotPriceLimit| | |The set of the preemptible instances.

 |
|InstanceType|String|ecs.t1.xsmall|The type of a preemptible instance.

 |
|PriceLimit|Float|0.125|The price limit of the preemptible instance.

 |
|SpotStrategy|String|NoSpot|The preemption strategy for pay-as-you-go instances. Valid values:

 -   NoSpot: a pay-as-you-go instance.
-   SpotWithPriceLimit: a preemptible instance with a maximum hourly price.
-   SpotAsPriceGo: an instance priced at the market price at the time of purchase.

 |
|SystemDiskCategory|String|cloud|The category of the system disk. Valid values:

 -   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   ephemeral\_ssd: local SSD
-   cloud\_essd: enhanced SSD

 |
|SystemDiskDescription|String|FinanceDept|The description of the system disk.

 |
|SystemDiskName|String|cloud\_ssdSystem|The name of the system disk.

 |
|SystemDiskSize|Integer|100|The size of the system disk.

 |
|Tags| | |The set of tags.

 |
|Key|String|binary|The key of the tag.

 |
|Value|String|alterTable|The value of the tag.

 |
|UserData|String|echo hello ecs!|The user data of an ECS instance.

 |
|TotalCount|Integer|1|The total number of scaling configurations.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://[Endpoint]/? Action=DescribeScalingConfigurations
&RegionId=cn-qingdao
&<Common request parameters>

```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
<DescribeScalingConfigurationsResponse>
      <RequestId>804F240A-8D3E-40A1-BD68-6B333DEA2CA8</RequestId>
      <TotalCount>1</TotalCount>
      <PageNumber>1</PageNumber>
      <PageSize>50</PageSize>
      <ScalingConfigurations>
            <ScalingConfiguration>
                  <CreationTime>2014-08-14T10:58Z</CreationTime>
                  <ImageId>centos6u5_64_20G_aliaegis_20140703.vhd</ImageId>
                  <InstanceType>ecs.t1.xsmall</InstanceType>
                  <InternetChargeType>PayByTraffic</InternetChargeType>
                  <InternetMaxBandwidthIn>200</InternetMaxBandwidthIn>
                  <InternetMaxBandwidthOut>0</InternetMaxBandwidthOut>
                  <LifecycleState>Active</LifecycleState>
                  <ScalingConfigurationId>bU5uZHcAgtzwcL4IeDea****</ScalingConfigurationId>
                  <ScalingConfigurationName>c1908dd1-690f-4c9b-ab73-350f1f06****</ScalingConfigurationName>
                  <ScalingGroupId>dE9YbOdCHqaFdFZHXVdD****</ScalingGroupId>
                  <SecurityGroupId>sg-280ih****</SecurityGroupId>
                  <SystemDiskCategory>cloud</SystemDiskCategory>
                  <DataDisks>
                    <DataDisk>
                          <Size>200</Size>
                          <Category>cloud</Category>
                          <SnapshotId>s-280s7****</SnapshotId>
                          <Device>/dev/xvdb</Device>
                    </DataDisk>
                  </DataDisks>
            </ScalingConfiguration>
      </ScalingConfigurations>
</DescribeScalingConfigurationsResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":"1",
	"TotalCount":"1",
	"ScalingConfigurations":{
		"ScalingConfiguration":{
			"ImageId":"centos6u5_64_20G_aliaegis_20140703.vhd",
			"SecurityGroupId":"sg-280ih****",
			 "InternetMaxBandwidthIn":"200",
			"DataDisks":{
				"DataDisk":[]
					"Category":"cloud",
					"Device":"/dev/xvdb",
					"SnapshotId":"s-280s7****",
					"Size":"200"
				}
			},
			"InternetChargeType":"PayByTraffic",
			"InstanceType":"ecs.t1.xsmall",
			"CreationTime":"2014-08-14T10:58Z",
			"ScalingConfigurationId":"bU5uZHcAgtzwcL4IeDea****",
			"InternetMaxBandwidthOut":"0",
			"ScalingGroupId":"dE9YbOdCHqaFdFZHXVdD****",
			"ScalingConfigurationName":"c1908dd1-690f-4c9b-ab73-350f1f06****",
			"SystemDiskCategory":"cloud",
			"LifecycleState":"Active"
		}
	},
	"PageSize":"50",
	"RequestId":"804F240A-8D3E-40A1-BD68-6B333DEA2CA8"
}
```

## Error codes { .section}

