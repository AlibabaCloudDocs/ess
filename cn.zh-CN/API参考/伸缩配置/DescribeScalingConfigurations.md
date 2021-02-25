# DescribeScalingConfigurations

调用DescribeScalingConfigurations查询伸缩配置的信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DescribeScalingConfigurations&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeScalingConfigurations|系统规定参数。取值：DescribeScalingConfigurations |
|RegionId|String|是|cn-qingdao|伸缩配置所属伸缩组的地域ID。 |
|PageNumber|Integer|否|1|伸缩配置列表的页码，起始值：1。

 默认值：1 |
|PageSize|Integer|否|50|分页查询时设置的每页行数，最大值：50。

 默认值：10 |
|ScalingGroupId|String|否|asg-bp17pelvl720x3v7\*\*\*\*|伸缩组的ID，您可以查询该伸缩组下所有的伸缩配置。 |
|ScalingConfigurationId.N|RepeatList|否|asc-bp17pelvl720x5ub\*\*\*\*|ScalingConfigurationId.N为待查询伸缩配置的ID，N的取值范围：1～10。查询结果包括生效和未生效的伸缩配置，并通过返回参数LifecycleState进行标识。 |
|ScalingConfigurationName.N|RepeatList|否|scalingcon\*\*\*\*|ScalingConfigurationName.N为待查询伸缩配置的名称，N的取值范围：1～10。查询结果会忽略失效的伸缩配置名称，并且不报错。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|当前页码。 |
|PageSize|Integer|50|每页行数。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|ScalingConfigurations|Array of ScalingConfiguration| |伸缩配置信息的集合。 |
|ScalingConfiguration| | | |
|Affinity|String|default|专有宿主机实例是否与专有宿主机关联。取值范围：

 -   default：实例不与专有宿主机关联。已开启停机不收费功能的实例，停机后再次启动时，若原专有宿主机可用资源不足，则实例被放置在自动部署资源池的其它专有宿主机上。
-   host：实例与专有宿主机关联。已开启停机不收费功能的实例，停机后再次启动时，仍放置在原专有宿主机上。若原专有宿主机可用资源不足，则实例重启失败。 |
|Cpu|Integer|2|vCPU个数。

 同时指定CPU和Memory可以定义实例规格范围，例如，CPU=2且Memory=16可以定义配置为2 vCPU和16 GiB的所有实例规格。弹性伸缩会结合IO优化、可用区等因素确定可用实例规格集合，并根据价格排序为您创建价格最低的实例。

 **说明：** 该区间配置效果仅在成本优化模式下且伸缩配置未设置实例规格时生效。 |
|CreationTime|String|2014-08-14T10:58Z|伸缩配置的创建时间。 |
|CreditSpecification|String|Standard|突发性能实例的运行模式。取值范围：

 -   Standard：标准模式，实例性能请参见[什么是突发性能实例](~~59977~~)下的性能约束模式章节。
-   Unlimited：无性能约束模式，实例性能请参见[什么是突发性能实例](~~59977~~)下的无性能约束模式章节。 |
|DataDisks|Array of DataDisk| |数据盘信息的集合。 |
|DataDisk| | | |
|AutoSnapshotPolicyId|String|sp-bp19nq9enxqkomib\*\*\*\*|数据盘使用的自动快照策略ID。 |
|Category|String|cloud|数据盘的磁盘种类。取值范围：

 -   cloud：普通云盘。随实例创建的普通云盘的DeleteWithInstance属性为true。
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘 |
|DeleteWithInstance|Boolean|true|数据盘是否随实例释放。取值范围：

 -   true：释放实例时，该磁盘随实例一起释放。
-   false：释放实例时，该磁盘保留不释放。 |
|Description|String|FinanceDept|数据盘的描述。 |
|Device|String|/dev/xvdb|数据盘的挂载点。 |
|DiskName|String|cloud\_ssdData|数据盘的名称。 |
|Encrypted|String|false|数据盘是否加密。取值范围：

 -   true：加密
-   false：不加密 |
|KMSKeyId|String|0e478b7a-4262-4802-b8cb-00d3fb40\*\*\*\*|数据盘对应的KMS密钥的ID。 |
|PerformanceLevel|String|PL1|当数据盘为ESSD云盘时，ESSD云盘的性能等级。 |
|Size|Integer|200|数据盘的磁盘大小，内存单位为GiB。取值范围：

 -   cloud：5~2000
-   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768
-   ephemeral\_ssd：5~800 |
|SnapshotId|String|s-23f2i\*\*\*\*|创建数据盘使用的快照ID。 |
|DedicatedHostId|String|dh-bp67acfmxazb4p\*\*\*\*|是否在专有宿主机上创建ECS实例。由于专有宿主机不支持创建抢占式实例，指定DedicatedHostId参数后，会自动忽略请求中的SpotStrategy和SpotPriceLimit设置。

 您可以通过[DescribeDedicatedHosts](~~134242~~)查询专有宿主机ID列表。 |
|DeploymentSetId|String|ds-bp1frxuzdg87zh4p\*\*\*\*|ECS实例所属的部署集的ID。 |
|HostName|String|LocalHost|云服务器的主机名。 |
|HpcClusterId|String|hpc-clus\*\*\*\*|ECS实例所属的HPC集群的ID。 |
|ImageFamily|String|hangzhou-daily-update|镜像族系名称，通过设置该参数来获取当前镜像族系内最新可用的自定义镜像，用于创建实例。如果已经设置了参数ImageId，则不能设置该参数。 |
|ImageId|String|centos6u5\_64\_20G\_aliaegis\_2014\*\*\*\*.vhd|镜像文件ID，自动创建实例时使用的镜像资源。 |
|ImageName|String|centos6u5\_64\_20G\_aliaegis\_20140703.vhd|镜像文件名称。 |
|InstanceDescription|String|FinanceDept|ECS实例的描述。 |
|InstanceGeneration|String|ecs-3|ECS实例的系列。 |
|InstanceName|String|instance\*\*\*\*|ECS实例的名称。 |
|InstanceType|String|ecs.g6.large|ECS实例的实例规格。 |
|InstanceTypes|List|ecs.g6.large|ECS实例的实例规格的集合。 |
|InternetChargeType|String|PayByTraffic|网络计费类型。取值范围：

 -   PayByBandwidth：按带宽计费。此时InternetMaxBandwidthOut即为所选的固定带宽值。
-   PayByTraffic：按流量计费。此时InternetMaxBandwidthOut只是一个带宽上限，计费以实际产生的网络流量为依据。 |
|InternetMaxBandwidthIn|Integer|200|公网入带宽最大值，单位为Mbps（Mega bit per second），取值范围：1~200。 |
|InternetMaxBandwidthOut|Integer|0|公网出带宽最大值，单位为Mbps（Mega bit per second）。取值范围：

 -   按带宽计费：0~100，如果您没有指定该参数，则出带宽将自动被设置为0Mbps。
-   按流量计费：0~100，如果您没有指定该参数，则会出现报错。 |
|IoOptimized|String|none|是否为I/O优化实例。取值范围：

 -   none：非I/O优化。
-   optimized：I/O优化。 |
|Ipv6AddressCount|Integer|1|为弹性网卡指定随机生成的IPv6地址数量。 |
|KeyPairName|String|keypair\*\*\*\*|登录ECS实例时使用的密钥对的名称。 |
|LifecycleState|String|Active|伸缩配置在伸缩组中的状态。取值范围：

 -   Active：生效状态。伸缩组会使用处于生效状态的伸缩配置自动创建ECS实例。
-   Inacitve：未生效状态。处于未生效状态的伸缩配置存在于伸缩组中，但伸缩组不会使用此类伸缩配置自动创建ECS实例。 |
|LoadBalancerWeight|Integer|1|ECS实例作为后端服务器时的权重，取值范围：1~100。 |
|Memory|Integer|16|内存大小。

 同时指定CPU和Memory可以定义实例规格范围。例如，CPU=2且Memory=16可以定义配置为2 vCPU和16 GiB的所有实例规格。弹性伸缩会结合IO优化、可用区等因素确定可用实例规格集合，并根据价格排序为您创建价格最低的实例。

 **说明：** 该区间配置效果仅在成本优化模式下且伸缩配置未设置实例规格时生效。 |
|PasswordInherit|Boolean|true|是否使用镜像预设的密码。 |
|PrivatePoolOptions.Id|String|eap-bp67acfmxazb4\*\*\*\*|私有池ID。即弹性保障服务ID或容量预定服务ID。

 **说明：** 该参数邀测中，详情请提交工单咨询。 |
|PrivatePoolOptions.MatchCriteria|String|Open|实例启动的私有池容量选项。弹性保障服务或容量预定服务在生效后会生成私有池容量，供实例启动时选择。取值范围：

 -   Open：开放模式。将自动匹配开放类型的私有池容量。如果没有符合条件的私有池容量，则使用公共池资源启动。
-   Target：指定模式。使用指定的私有池容量启动实例，如果该私有池容量不可用，则实例会启动失败。
-   None：不使用模式。实例启动将不使用私有池容量。

 **说明：** 该参数邀测中，详情请提交工单咨询。 |
|RamRoleName|String|ramrole\*\*\*\*|ECS实例的RAM角色名称。RAM角色名称由RAM提供和维护，您可调用[ListRoles](~~28713~~)查询可用的RAM角色。创建RAM角色的方法请参见[CreateRole](~~28710~~)。 |
|ResourceGroupId|String|rg-aekzn2ou7xo\*\*\*\*|ECS实例所属资源组的ID。 |
|ScalingConfigurationId|String|asc-bp1ezrfgoyn5kijl\*\*\*\*|伸缩配置的ID。 |
|ScalingConfigurationName|String|scalingconfi\*\*\*\*|伸缩配置的名称。 |
|ScalingGroupId|String|asg-bp17pelvl720x3v7\*\*\*\*|伸缩配置所属伸缩组的ID。 |
|SchedulerOptions|Struct| |**说明：** 该参数正在邀测中，暂未开放使用。 |
|ManagedPrivateSpaceId|String|testManagedPrivateSpaceId|**说明：** 该参数正在邀测中，暂未开放使用。 |
|SecurityEnhancementStrategy|String|Active|是否开启安全加固。取值范围：

 -   Active：启用安全加固，只对公共镜像生效。
-   Deactive：不启用安全加固，对所有镜像类型生效。 |
|SecurityGroupId|String|sg-bp18kz60mefs\*\*\*\*|ECS实例所属的安全组的ID，同一个安全组内的ECS实例可以互相访问。 |
|SecurityGroupIds|List|sg-bp18kz60mefs\*\*\*\*|ECS实例所属的多个安全组的ID，同一个安全组内的ECS实例可以互相访问。 |
|SpotDuration|Integer|1|抢占式实例的保留时长，单位为小时。 |
|SpotInterruptionBehavior|String|Terminate|抢占实例中断模式。 |
|SpotPriceLimit|Array of SpotPriceModel| |抢占式实例信息的集合。 |
|SpotPriceModel| | | |
|InstanceType|String|ecs.g6.large|抢占式实例的实例规格。 |
|PriceLimit|Float|0.125|抢占式实例对应的出价。 |
|SpotStrategy|String|NoSpot|后付费实例的抢占策略。取值范围：

 -   NoSpot：普通的按量付费实例。
-   SpotWithPriceLimit：设置上限价格的抢占式实例。
-   SpotAsPriceGo：系统自动出价，跟随当前市场实际价格。 |
|SystemDiskAutoSnapshotPolicyId|String|sp-bp12m37ccmxvbmi5\*\*\*\*|系统盘使用的自动快照策略ID。 |
|SystemDiskCategory|String|cloud|系统盘的磁盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘 |
|SystemDiskDescription|String|Test system disk.|系统盘的描述。 |
|SystemDiskName|String|cloud\_ssd\_Test|系统盘的名称。 |
|SystemDiskPerformanceLevel|String|PL1|当系统盘为ESSD云盘时，ESSD云盘的性能等级。 |
|SystemDiskSize|Integer|100|系统盘的磁盘大小。 |
|Tags|Array of Tag| |标签信息的集合。 |
|Tag| | | |
|Key|String|binary|标签键。 |
|Value|String|alterTable|标签值。 |
|Tenancy|String|default|是否在专有宿主机上创建实例。取值范围：

 -   default：创建非专有宿主机实例。
-   host：创建专有宿主机实例。若您不指定DedicatedHostId，则由阿里云自动选择专有宿主机放置实例。 |
|UserData|String|echo hello ecs!|ECS实例的自定义数据。 |
|WeightedCapacities|List|4|对应指定实例规格的权重，即实例规格的单台实例在伸缩组中表示的容量大小。权重越大，满足期望容量所需的本实例规格的实例数量越少。 |
|ZoneId|String|cn-hangzhou-g|实例所属的可用区ID，您可以调用[DescribeZones](~~25610~~)获取可用区列表。 |
|TotalCount|Integer|1|伸缩配置的总数。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=DescribeScalingConfigurations
&RegionId=cn-qingdao
&<公共请求参数>
```

正常返回示例

`XML`格式

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

`JSON`格式

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

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

