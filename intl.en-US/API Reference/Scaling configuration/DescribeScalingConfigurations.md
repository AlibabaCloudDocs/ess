# DescribeScalingConfigurations

You can call this operation to query scaling configurations.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeScalingConfigurations&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeScalingConfigurations|The operation that you want to perform. Set the value to DescribeScalingConfigurations. |
|RegionId|String|Yes|cn-qingdao|The region ID of the scaling group to which a scaling configuration belongs. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default value: 1 |
|PageSize|Integer|No|50|The number of entries to return on each page. Maximum value: 50.

Default value: 10 |
|ScalingGroupId|String|No|asg-bp17pelvl720x3v7\*\*\*\*|The ID of the scaling group. You can query all scaling configurations in the scaling group. |
|ScalingConfigurationId.1|String|No|asc-bp17pelvl720x5ub\*\*\*\*|The ID of scaling configuration N to be queried. Valid values of N: 1 to 10. The IDs of active and inactive scaling configurations are displayed in the query result, and can be differentiated by LifecycleState. |
|ScalingConfigurationName.1|String|No|scalingcon\*\*\*\*|The name of scaling configuration N to be queried. Valid values of N: 1 to 10. The names of inactive scaling configurations are not displayed in the query result and no errors are reported. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|50|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request |
|ScalingConfigurations|Array of ScalingConfiguration| |The collection of scaling configurations. |
|ScalingConfiguration| | | |
|Affinity|String|default|Indicates whether the instance on a dedicated host is associated with the dedicated host. Valid values:

-   default: The instance is not associated with the dedicated host. When the No Fees for Stopped Instances \(VPC-Connected\) feature is enabled and the instance is restarted, the instance is automatically deployed to another dedicated host in the automatic deployment resource pool if resources of the original dedicated host are insufficient.
-   host: The instance is associated with the dedicated host. When the No Fees for Stopped Instances \(VPC-Connected\) feature is enabled and the instance is restarted, the instance still resides on the original dedicated host. If resources of the original dedicated host are insufficient, the instance fails to be restarted. |
|Cpu|Integer|2|The number of vCPUs.

You can specify the number of vCPUs and the amount of memory to define the range of instance types. For example, to specify instance types that have 2 vCPUs and 16 GiB memory, set Cpu to 2 and Memory to 16. Auto Scaling uses factors such as I/O optimization and zone to determine a set of available instance types. Auto Scaling then creates instances based on the unit prices of instance types in ascending order.

**Note:** This instance type range takes effect only when cost optimization is enabled and you have not specified an instance type in the scaling configuration. |
|CreationTime|String|2014-08-14T10:58Z|The time when a scaling configuration was created. |
|CreditSpecification|String|Standard|The performance mode of the burstable instance. Valid values:

-   Standard: standard mode. For more information, see the "Standard mode" section in [Burstable instances](~~59977~~).
-   Unlimited: unlimited mode. For more information, see the "Unlimited mode" section in [Burstable instances](~~59977~~). |
|DataDisks|Array of DataDisk| |The collection of data disk details. |
|DataDisk| | | |
|AutoSnapshotPolicyId|String|sp-bp19nq9enxqkomib\*\*\*\*|The ID of the automatic snapshot policy that is applied to the data disk. |
|Category|String|cloud|The category of the data disk. Valid values:

-   cloud: basic disk. The DeleteWithInstance attribute of a basic disk created together with the instance is true.
-   cloud\_efficiency: ultra disk.
-   cloud\_ssd: standard SSD.
-   ephemeral\_ssd: local SSD.
-   cloud\_essd: enhanced SSD. |
|DeleteWithInstance|Boolean|true|Indicates whether the data disk will be released with the instance. Valid values:

-   true: releases the data disk when the instance is released.
-   false: retains the data disk when the instance is released. |
|Description|String|FinanceDept|The description of the data disk. |
|Device|String|/dev/xvdb|The mount point of the data disk. |
|DiskName|String|cloud\_ssdData|The name of the data disk. |
|Encrypted|String|false|Indicates whether the data disk is encrypted. Valid values:

-   true: The disk is encrypted.
-   false: The disk is not encrypted. |
|KMSKeyId|String|0e478b7a-4262-4802-b8cb-00d3fb40\*\*\*\*|The ID of the KMS key corresponding to the data disk. |
|Size|Integer|200|The size of the data disk. Unit: GiB. Valid values:

-   Valid values when Category is set to cloud: 5 to 2000
-   Valid values when Category is set to cloud\_efficiency: 20 to 32768
-   Valid values when Category is set to cloud\_ssd: 20 to 32768
-   Valid values when Category is set to cloud\_essd: 20 to 32768
-   Valid values when Category is set to ephemeral\_ssd: 5 to 800 |
|SnapshotId|String|s-23f2i\*\*\*\*|The ID of the snapshot used to create data disks. |
|DedicatedHostId|String|dh-bp67acfmxazb4p\*\*\*\*|The ID of the dedicated host on which to create the instance. If the DedicatedHostId parameter is specified, the SpotStrategy and SpotPriceLimit parameters are ignored. This is because preemptible instances cannot be created on dedicated hosts.

You can call the [DescribeDedicatedHosts](~~134242~~) operation to query the dedicated host list. |
|DeploymentSetId|String|ds-bp1frxuzdg87zh4p\*\*\*\*|The ID of the deployment set to which the ECS instance belongs. |
|HostName|String|LocalHost|The name of the host where the created ECS instances reside. |
|HpcClusterId|String|hpc-clus\*\*\*\*|The ID of the HPC cluster to which the ECS instance belongs. |
|ImageFamily|String|hangzhou-daily-update|The name of the image family. You can configure this parameter to obtain the latest available custom images within the specified image family to create ECS instances. If you have set the ImageId parameter, you cannot set the ImageFamily parameter. |
|ImageId|String|centos6u5\_64\_20G\_aliaegis\_2014\*\*\*\*.vhd|The ID of the image used to automatically create an instance. |
|ImageName|String|centos6u5\_64\_20G\_aliaegis\_20140703.vhd|The name of the image. |
|InstanceDescription|String|FinanceDept|The description of the ECS instance. |
|InstanceGeneration|String|ecs-3|The generation of the ECS instance. |
|InstanceName|String|instance\*\*\*\*|The name of the ECS instance. |
|InstanceType|String|ecs.g6.large|The instance type of the ECS instance. |
|InstanceTypes|List|ecs.g6.large|The collection of ECS instance types. |
|InternetChargeType|String|PayByTraffic|The billing method for network usage. Valid values:

-   PayByBandwidth: You must pay for the maximum available bandwidth specified by the InternetMaxBandwidthOut parameter.
-   PayByTraffic: You pay for the actual traffic used. The InternetMaxBandwidthOut parameter only specifies the upper limit of available bandwidth when this parameter is specified. |
|InternetMaxBandwidthIn|Integer|200|The maximum inbound bandwidth from the Internet. Unit: Mbit/s. Valid values: 1 to 200. |
|InternetMaxBandwidthOut|Integer|0|The maximum outbound bandwidth to the Internet. Unit: Mbit/s. Valid values: 0 to 100.

-   If InternetChargeType is set to PayByBandwidth and this parameter is not specified, this parameter is automatically set to 0.
-   If InternetChargeType is set to PayByTraffic and this parameter is not specified, an error is returned. |
|IoOptimized|String|none|Indicates whether the instance is I/O optimized. Valid values:

-   none: The instance is not I/O optimized.
-   optimized: The instance is I/O optimized. |
|Ipv6AddressCount|Integer|1|The number of randomly generated IPv6 addresses that are assigned to the ENI. |
|KeyPairName|String|keypair\*\*\*\*|The name of the key pair used to log on to the ECS instance. |
|LifecycleState|String|Active|The status of the scaling configuration in the scaling group. Valid values:

-   Active: The scaling configuration is active in the scaling group. The scaling group uses the active scaling configuration to automatically create ECS instances.
-   Inactive: The scaling configuration is inactive in the scaling group. Inactive scaling configurations are still retained in the scaling group, but are not used by the scaling group to create ECS instances. |
|LoadBalancerWeight|Integer|1|The weight of the ECS instance as a backend server. Valid values: 1 to 100. |
|Memory|Integer|16|The amount of memory.

You can specify the number of vCPUs and the amount of memory to define the range of instance types. For example, to specify instance types that have 2 vCPUs and 16 GiB memory, set Cpu to 2 and Memory to 16. Auto Scaling uses factors such as I/O optimization and zone to determine a set of available instance types. Auto Scaling then creates instances based on the unit prices of instance types in ascending order.

**Note:** This instance type range takes effect only when cost optimization is enabled and you have not specified an instance type in the scaling configuration. |
|PasswordInherit|Boolean|true|Indicates whether the password predefined in the specified image is used. |
|RamRoleName|String|ramrole\*\*\*\*|The name of the RAM role associated with the ECS instance. This name is provided and maintained by RAM. You can call the [ListRoles](~~28713~~) operation to query the list of RAM roles. For more information about how to create a RAM role, see [CreateRole](~~28710~~). |
|ResourceGroupId|String|rg-aekzn2ou7xo\*\*\*\*|The ID of the resource group to which the ECS instance belongs. |
|ScalingConfigurationId|String|asc-bp1ezrfgoyn5kijl\*\*\*\*|The ID of the scaling configuration. |
|ScalingConfigurationName|String|scalingconfi\*\*\*\*|The name of the scaling configuration. |
|ScalingGroupId|String|asg-bp17pelvl720x3v7\*\*\*\*|The ID of the scaling group to which the scaling configuration belongs. |
|SecurityEnhancementStrategy|String|Active|Indicates whether to enable security hardening. Valid values:

-   Active: enables security hardening. This value is applicable only to public images.
-   Deactive: disables security hardening. This value is applicable to all images. |
|SecurityGroupId|String|sg-bp18kz60mefs\*\*\*\*|The ID of the security group to which the ECS instance belongs. ECS instances in the same security group can access each other. |
|SecurityGroupIds|List|sg-bp18kz60mefs\*\*\*\*|The IDs of the security groups to which the ECS instance belongs. ECS instances in the same security group can access each other. |
|SpotPriceLimit|Array of SpotPriceModel| |The collection of preemptible instances. |
|SpotPriceModel| | | |
|InstanceType|String|ecs.g6.large|The instance type of the preemptible instance. |
|PriceLimit|Float|0.125|The price limit of the preemptible instance. |
|SpotStrategy|String|NoSpot|The preemption strategy to be applied to pay-as-you-go instances. Valid values:

-   NoSpot: applies to regular pay-as-you-go instances.
-   SpotWithPriceLimit: applies to preemptible instances that have maximum hourly prices.
-   SpotAsPriceGo: applies to preemptible instances whose prices are based on the current market price. |
|SystemDiskAutoSnapshotPolicyId|String|sp-bp12m37ccmxvbmi5\*\*\*\*|The ID of the automatic snapshot policy that is applied to the system disk. |
|SystemDiskCategory|String|cloud|The category of the system disk. Valid values:

-   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   ephemeral\_ssd: local SSD
-   cloud\_essd: enhanced SSD |
|SystemDiskDescription|String|Test system disk.|The description of the system disk. |
|SystemDiskName|String|cloud\_ssd\_Test|The name of the system disk. |
|SystemDiskSize|Integer|100|The size of the system disk. |
|Tags|Array of Tag| |The collection of tags. |
|Tag| | | |
|Key|String|binary|The key of the tag. |
|Value|String|alterTable|The value of the tag. |
|Tenancy|String|default|Indicates whether the instance is created on a dedicated host. Valid values:

-   default: The instance is created on a non-dedicated host.
-   host: The instance is created on a dedicated host. If you do not specify the DedicatedHostId parameter, Alibaba Cloud automatically selects a dedicated host for the instance. |
|UserData|String|echo hello ecs!|The user data of the ECS instance. |
|ZoneId|String|cn-hangzhou-g|The zone ID of the instance. You can call the [DescribeZones](~~25610~~) operation to query the most recent zone list. |
|TotalCount|Integer|1|The total number of scaling configurations. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DescribeScalingConfigurations
&RegionId=cn-qingdao
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeScalingConfigurationsResponse>
      <RequestId>804F240A-8D3E-40A1-BD68-6B333DEA2CA8</RequestId>
      <TotalCount>1</TotalCount>
      <PageNumber>1</PageNumber>
      <PageSize>50</PageSize>
      <ScalingConfigurations>
            <ScalingConfiguration>
                  <CreationTime>2014-08-14T10:58Z</CreationTime>
                  <ImageId>centos6u5_64_20G_aliaegis_2014****.vhd</ImageId>
                  <InstanceType>ecs.g6.large</InstanceType>
                  <InternetChargeType>PayByTraffic</InternetChargeType>
                  <InternetMaxBandwidthIn>200</InternetMaxBandwidthIn>
                  <InternetMaxBandwidthOut>0</InternetMaxBandwidthOut>
                  <LifecycleState>Active</LifecycleState>
                  <ScalingConfigurationId>asc-bp1ezrfgoyn5kijl****</ScalingConfigurationId>
                  <ScalingConfigurationName>scalingconfig****</ScalingConfigurationName>
                  <ScalingGroupId>asg-bp17pelvl720x3v7****</ScalingGroupId>
                  <SecurityGroupId>sg-bp18kz60mefs****</SecurityGroupId>
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

```
{
    "RequestId": "804F240A-8D3E-40A1-BD68-6B333DEA2CA8",
    "TotalCount": "1",
    "PageNumber": "1",
    "PageSize": "50",
    "ScalingConfigurations": {
        "ScalingConfiguration": {
            "CreationTime": "2014-08-14T10:58Z",
            "ImageId": "centos6u5_64_20G_aliaegis_2014****.vhd",
            "InstanceType": "ecs.g6.large",
            "InternetChargeType": "PayByTraffic",
            "InternetMaxBandwidthIn": "200",
            "InternetMaxBandwidthOut": "0",
            "LifecycleState": "Active",
            "ScalingConfigurationId": "asc-bp1ezrfgoyn5kijl****",
            "ScalingConfigurationName": "scalingconfig****",
            "ScalingGroupId": "asg-bp17pelvl720x3v7****",
            "SecurityGroupId": "sg-bp18kz60mefs****",
            "SystemDiskCategory": "cloud",
            "DataDisks": {
                "DataDisk": {
                    "Size": "200",
                    "Category": "cloud",
                    "SnapshotId": "s-280s7****",
                    "Device": "/dev/xvdb"
                }
            }
        }
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

