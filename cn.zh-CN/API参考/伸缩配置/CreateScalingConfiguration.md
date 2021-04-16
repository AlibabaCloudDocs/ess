# CreateScalingConfiguration

调用CreateScalingConfiguration创建一个伸缩配置。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=CreateScalingConfiguration&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateScalingConfiguration|系统规定参数。取值： CreateScalingConfiguration |
|ScalingGroupId|String|是|asg-bp14wlu85wrpchm0\*\*\*\*|伸缩配置所属的伸缩组的ID。 |
|ImageId|String|否|centos6u5\_64\_20G\_aliaegis\*\*\*\*.vhd|镜像文件ID，自动创建实例时使用的镜像资源。 |
|ImageName|String|否|image\*\*\*\*|镜像文件名称，同一个地域内镜像名称唯一。如果设置了ImageId， ImageName将被忽略。

 不支持通过ImageName设置镜像市场镜像。 |
|InstanceType|String|否|ecs.g6.large|ECS实例的实例规格，更多信息请参见[实例规格族](~~25378~~)。 |
|Cpu|Integer|否|2|vCPU个数。

 同时指定CPU和Memory可以定义实例规格范围，例如，CPU=2且Memory=16可以定义配置为2 vCPU和16 GiB的所有实例规格。弹性伸缩会结合IO优化、可用区等因素确定可用实例规格集合，并根据价格排序为您创建价格最低的实例。

 **说明：** 该区间配置效果仅在成本优化模式下且伸缩配置未设置实例规格时生效。 |
|Memory|Integer|否|16|内存大小。

 同时指定CPU和Memory可以定义实例规格范围。例如，CPU=2且Memory=16可以定义配置为2 vCPU和16 GiB的所有实例规格。弹性伸缩会结合IO优化、可用区等因素确定可用实例规格集合，并根据价格排序为您创建价格最低的实例。

 **说明：** 该区间配置效果仅在成本优化模式下且伸缩配置未设置实例规格时生效。 |
|DeploymentSetId|String|否|ds-bp1frxuzdg87zh4pz\*\*\*\*|ECS实例所属的部署集的ID。 |
|InstanceTypes.N|RepeatList|否|ecs.g6.large|多实例规格参数。如果使用了InstanceTypes.N，InstanceType将被忽略，其中N的取值范围：1~10，即一个伸缩配置内最多可以设置10种实例规格。

 N代表当前伸缩配置中实例规格的优先级，编号为1的实例规格优先级最高，实例规格优先级随着编号的增大依次降低。当无法根据优先级较高的实例规格创建出实例时，弹性伸缩服务会自动选择下一优先级的实例规格来创建实例。 |
|InstanceTypeOverride.N.InstanceType|String|否|ecs.c5.xlarge|当您需要指定伸缩配置中实例规格的容量时，请同时指定本参数和InstanceTypeOverride.N.WeightedCapacity。

 本参数用于指定实例规格。您可以指定N个本参数，结合InstanceTypeOverride.N.WeightedCapacity参数，扩展多实例规格支持自定义权重。N的取值范围：1~10。

 **说明：** 指定本参数时，不允许同时指定instanceTypes。

 InstanceType的取值范围：在售的ECS实例规格，请参见[实例规格族](~~25378~~)。 |
|InstanceTypeOverride.N.WeightedCapacity|Integer|否|4|当您需要指定伸缩配置中实例规格的容量时，在指定InstanceTypeOverride.N.InstanceType后，再指定本参数。两个参数一一对应，N需要保持一致。

 本参数用于指定实例规格的权重，即实例规格的单台实例在伸缩组中表示的容量大小。权重越大，满足期望容量所需的本实例规格的实例数量越少。

 由于每个实例规格的vCPU个数、内存大小等性能指标会有差异，您可以根据自身需求，给不同的实例规格配置不同的权重。

 例如：

 -   当前容量：0
-   期望容量：6
-   ecs.c5.xlarge规格容量：4

 为满足期望容量，伸缩组将为用户扩容2台ecs.c5.xlarge实例。

 **说明：** 扩容时伸缩组的容量不得超过最大容量（MaxSize）与实例规格的最大权重之和。

 WeightedCapacity的取值范围：1~500。 |
|SecurityGroupId|String|否|sg-280ih\*\*\*\*|ECS实例所属的安全组的ID，同一个安全组内的ECS实例可以互相访问。 |
|IoOptimized|String|否|optimized|是否为I/O优化实例。[已停售的实例规格](~~55263~~)实例默认值是none，其他实例规格默认值是optimized。取值范围：

 -   none：非I/O优化实例。
-   optimized：I/O优化实例。 |
|InternetChargeType|String|否|PayByTraffic|网络计费类型。取值范围：

 -   PayByBandwidth：按带宽计费。此时InternetMaxBandwidthOut即为所选的固定带宽值。
-   PayByTraffic：按流量计费。此时InternetMaxBandwidthOut只是一个带宽上限，计费以实际产生的网络流量为依据。

 如果未指定该参数，经典网络下默认值为PayByBandwidth，专有网络VPC下默认值为PayByTraffic。 |
|InternetMaxBandwidthIn|Integer|否|100|公网入带宽最大值，单位为Mbps（Mega bit per second），取值范围：1~200。

 如果您没有指定该参数，则入带宽将自动被设置为200Mbps。实例的入数据流量免费，该参数在任何情况下都不涉及计费。 |
|InternetMaxBandwidthOut|Integer|否|50|公网出带宽最大值，单位为Mbps（Mega bit per second）。取值范围：

 -   按带宽计费：0~100，如果您没有指定该参数，则出带宽将自动被设置为0Mbps。
-   按流量计费：0~100，如果您没有指定该参数，则会出现报错。 |
|SystemDisk.Category|String|否|cloud\_ssd|系统盘的磁盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘

 InstanceType为系列I的实例规格且实例属于非I/O优化实例时，默认值：cloud。否则，默认值：cloud\_efficiency。 |
|SystemDisk.Size|Integer|否|100|系统盘的大小，单位：GiB。取值范围：

 -   cloud：20~500
-   cloud\_efficiency：20~500
-   cloud\_ssd：20~500
-   cloud\_essd：20~500
-   ephemeral\_ssd：20~500

 指定该参数后，系统盘大小必须大于等于max\{20, ImageSize\}。

 默认值：max\{40, ImageSize\} |
|SystemDisk.DiskName|String|否|cloud\_ssdSystem|系统盘的名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 默认值：空 |
|SystemDisk.Description|String|否|Test system disk.|系统盘的描述。长度为2~256个英文或中文字符，不能以http://和https://开头。 |
|SystemDisk.AutoSnapshotPolicyId|String|否|sp-bp12m37ccmxvbmi5\*\*\*\*|系统盘使用的自动快照策略ID。 |
|SystemDisk.PerformanceLevel|String|否|PL0|当系统盘为ESSD云盘时，设置云盘的性能等级。取值范围：

 -   PL0：单盘最高随机读写IOPS 1万。
-   PL1：单盘最高随机读写IOPS 5万。
-   PL2：单盘最高随机读写IOPS 10万。
-   PL3：单盘最高随机读写IOPS 100万。

 默认值：PL0

 **说明：** 关于如何选择ESSD云盘性能等级，请参见[ESSD云盘](~~122389~~)。 |
|ScalingConfigurationName|String|否|scalingconfig\*\*\*\*|伸缩配置的名称，2~64英文或中文字符，以数字、大小写字母或中文开头，可包含数字、下划线（\_）、连字符（-）或点号（.）。

 在同一地域下同一伸缩组内伸缩配置名称唯一。如果您没有指定该参数，则默认使用伸缩配置的ID。 |
|DataDisk.N.Size|Integer|否|100|数据盘N的磁盘大小，N的取值范围：1~16，内存单位为GiB。取值范围：

 -   cloud：5~2000
-   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768
-   ephemeral\_ssd：5~800

 指定该参数后，磁盘大小必须大于等于快照大小（快照通过SnapshotId指定）。 |
|DataDisk.N.SnapshotId|String|否|s-280s7\*\*\*\*|创建数据盘时使用的快照，N的取值范围：1~16。指定该参数后，DataDisk.N.Size会被忽略，实际创建的磁盘大小为指定快照的大小。

 如果该快照创建于2013年7月15日或之前，调用会被拒绝，返回参数中会提示InvalidSnapshot.TooOld。 |
|DataDisk.N.Category|String|否|cloud\_ssd|数据盘N的磁盘种类，N的取值范围：1~16。该参数取值范围：

 -   cloud：普通云盘。随实例创建的普通云盘的DeleteWithInstance属性为true。
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘

 对于I/O优化实例，默认值为cloud\_efficiency。对于非I/O优化实例，默认值为cloud。 |
|DataDisk.N.Device|String|否|/dev/xvdb|数据盘挂载点，N的取值范围：1~16。如果您没有指定该参数，则默认在自动创建ECS实例时由系统分配，从/dev/xvdb开始，到/dev/xvdz结束。 |
|DataDisk.N.DeleteWithInstance|Boolean|否|true|指定数据盘是否随实例释放，N的取值范围：1~16。该参数取值范围：

 -   true：释放实例时，该磁盘随实例一起释放。
-   false：释放实例时，该磁盘保留不释放。

 该参数只可对独立云盘设置（DataDisk.N.Category为cloud、cloud\_efficiency、cloud\_ssd或cloud\_essd），否则会出现报错。

 默认值：true |
|DataDisk.N.Encrypted|String|否|false|数据盘N是否加密，N的取值范围：1~16。该参数取值范围：

 -   true：加密
-   false：不加密

 默认值：false |
|DataDisk.N.KMSKeyId|String|否|0e478b7a-4262-4802-b8cb-00d3fb40\*\*\*\*|数据盘对应的KMS密钥的ID，N的取值范围：1~16。 |
|DataDisk.N.DiskName|String|否|cloud\_ssdData|数据盘的名称，N的取值范围：1~16。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 默认值：空 |
|DataDisk.N.Description|String|否|Test data disk.|数据盘的描述，N的取值范围：1~16。长度为2~256个英文或中文字符，不能以 http:// 和 https:// 开头。 |
|DataDisk.N.AutoSnapshotPolicyId|String|否|sp-bp19nq9enxqkomib\*\*\*\*|数据盘使用的自动快照策略ID，N的取值范围：1~16。 |
|DataDisk.N.PerformanceLevel|String|否|PL1|当数据盘为ESSD云盘时，设置云盘的性能等级。N的取值必须和DataDisk.N.Category=cloud\_essd中的N保持一致。取值范围：

 -   PL0：单盘最高随机读写IOPS 1万。
-   PL1：单盘最高随机读写IOPS 5万。
-   PL2：单盘最高随机读写IOPS 10万。
-   PL3：单盘最高随机读写IOPS 100万。

 默认值：PL1

 **说明：** 关于如何选择ESSD云盘性能等级，请参见[ESSD云盘](~~122389~~)。 |
|LoadBalancerWeight|Integer|否|50|ECS实例作为负载均衡后端服务器时的权重，取值范围：1~100。

 默认值：50 |
|Tags|String|否|\{"key1":"value1","key2":"value2", ... "key5":"value5"\}|ECS实例的标签。标签以键值对方式传入，最多可以使用20组标签。Key和Value的使用要求如下：

 -   Key最多支持64个字符，不能以aliyun和acs:开头，不能包含 http:// 或者 https:// 。一旦使用标签，Key不允许为空字符串。
-   Value最多支持128个字符，不能以aliyun和acs:开头，不能包含 http:// 或者 https:// 。Value可以为空字符串。 |
|UserData|String|否|echo hello ecs!|ECS实例的自定义数据，需要以Base64方式编码，编码前的原始数据最多为16KB。 |
|KeyPairName|String|否|KeyPairTest|登录ECS实例时使用的密钥对的名称。

 -   对Windows实例，该参数将被忽略，默认为空。
-   对Linux实例，密码登录方式会被初始化成禁止。 |
|RamRoleName|String|否|ramrole\*\*\*\*|ECS实例的RAM角色名称。RAM角色名称由RAM提供和维护，您可调用[ListRoles](~~28713~~)查询可用的RAM角色。创建RAM角色的方法请参见[CreateRole](~~28710~~)。 |
|SecurityEnhancementStrategy|String|否|Active|是否开启安全加固。取值范围：

 -   Active：启用安全加固，只对公共镜像生效。
-   Deactive：不启用安全加固，对所有镜像类型生效。 |
|InstanceName|String|否|instance\*\*\*\*|使用本伸缩配置自动创建的ECS实例的名称。 |
|HostName|String|否|host\*\*\*\*|云服务器的主机名。点号（.）或连字符（-）不能作为首尾字符，不能连续使用点号（.）或连字符（-）。另外，不同类型实例的命名要求如下：

 -   Windows实例：主机名长度为2~15，可以包含大小写字母、数字和连字符（-）。不能包含点号（.），不能全是数字。
-   其他类型实例（Linux等）：主机名长度为2~64，可以包含多个点号（.）。两个点号（.）之间为一段，每段可以包含大小写字母、数字和连字符（-）。 |
|SpotStrategy|String|否|NoSpot|后付费实例的抢占策略。取值范围：

 -   NoSpot：普通的按量付费实例。
-   SpotWithPriceLimit：设置上限价格的抢占式实例。
-   SpotAsPriceGo：系统自动出价，跟随当前市场实际价格。

 默认值：NoSpot |
|PasswordInherit|Boolean|否|false|是否使用镜像预设的密码。使用该参数时，您需要确保使用的镜像已经设置了密码。取值范围：

 -   true：使用镜像预设密码。
-   false：不使用镜像预设密码。 |
|SpotPriceLimit.N.InstanceType|String|否|ecs.g6.large|抢占式实例的实例规格，N的取值范围：1~10。SpotStrategy取值为SpotWithPriceLimit时生效。 |
|SpotPriceLimit.N.PriceLimit|Float|否|0.5|抢占式实例对应的出价，N的取值范围：1~10。SpotStrategy取值为SpotWithPriceLimit时生效。 |
|Password|String|否|123abc\*\*\*\*|ECS实例的密码。长度为8至30个字符，必须同时包含大小写英文字母、数字和特殊符号中的三类字符。特殊符号可以是：

 ```
()` ~!@#$%^&*-_+=\|{}[]:;'<>,.?/
```

 其中，Windows实例不能以斜线号（/）为密码首字符。

 **说明：** 如果传入Password参数，建议您使用HTTPS协议发送请求，避免密码泄露。 |
|ResourceGroupId|String|否|rg-resource\*\*\*\*|ECS实例所属资源组的ID。 |
|SecurityGroupIds.N|RepeatList|否|sg-bp18kz60mefs\*\*\*\*|将ECS实例同时加入多个安全组。N的取值范围与实例能够加入安全组上限有关。更多详情，请参见[使用限制](~~25412~~)下的安全组章节。

 **说明：** 不支持同时指定SecurityGroupId和SecurityGroupIds.N。 |
|HpcClusterId|String|否|hpc-clusterid|ECS实例所属的HPC集群的ID。 |
|InstanceDescription|String|否|Test instance.|ECS实例的描述。长度为2~256个英文或中文字符，不能以 http:// 和 https:// 开头。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |
|Ipv6AddressCount|Integer|否|1|为弹性网卡指定随机生成的IPv6地址数量。 |
|CreditSpecification|String|否|Standard|指定突发性能实例的运行模式。取值范围：

 -   Standard：标准模式，实例性能请参见[什么是突发性能实例](~~63440~~)下的性能约束模式章节。
-   Unlimited：无性能约束模式，实例性能请参见[什么是突发性能实例](~~63440~~)下的无性能约束模式章节。

 默认值：无 |
|ImageFamily|String|否|hangzhou-daily-update|镜像族系名称，通过设置该参数来获取当前镜像族系内最新可用的自定义镜像，用于创建实例。如果已经设置了参数ImageId，则不能设置该参数。 |
|ZoneId|String|否|cn-hangzhou-g|ECS实例所属的可用区ID。 |
|DedicatedHostId|String|否|dh-bp67acfmxazb4p\*\*\*\*|是否在专有宿主机上创建ECS实例。由于专有宿主机不支持创建抢占式实例，指定DedicatedHostId参数后，会自动忽略请求中的SpotStrategy和SpotPriceLimit设置。

 您可以调用[DescribeDedicatedHosts](~~134242~~)查询专有宿主机ID列表。 |
|Affinity|String|否|default|专有宿主机实例是否与专有宿主机关联。取值范围：

 -   default：实例不与专有宿主机关联。已开启停机不收费功能的实例，停机后再次启动时，若原专有宿主机可用资源不足，则实例被放置在自动部署资源池的其它专有宿主机上。
-   host：实例与专有宿主机关联。已开启停机不收费功能的实例，停机后再次启动时，仍放置在原专有宿主机上。若原专有宿主机可用资源不足，则实例重启失败。

 默认值：default |
|Tenancy|String|否|default|是否在专有宿主机上创建实例。取值范围：

 -   default：创建非专有宿主机实例。
-   host：创建专有宿主机实例。若您不指定DedicatedHostId，则由阿里云自动选择专有宿主机放置实例。

 默认值：default |
|PrivatePoolOptions.MatchCriteria|String|否|Open|实例启动的私有池容量选项。弹性保障服务或容量预定服务在生效后会生成私有池容量，供实例启动时选择。取值范围：

 -   Open：开放模式。将自动匹配开放类型的私有池容量。如果没有符合条件的私有池容量，则使用公共池资源启动。该模式下无需设置PrivatePoolOptions.Id参数。
-   Target：指定模式。使用指定的私有池容量启动实例，如果该私有池容量不可用，则实例会启动失败。该模式下必须指定私有池ID，即PrivatePoolOptions.Id参数为必填项。
-   None：不使用模式。实例启动将不使用私有池容量。

 默认值：空

 **说明：** 该参数邀测中，详情请提交工单咨询。 |
|PrivatePoolOptions.Id|String|否|eap-bp67acfmxazb4\*\*\*\*|私有池ID。即弹性保障服务ID或容量预定服务ID。

 **说明：** 该参数邀测中，详情请提交工单咨询。 |
|SpotDuration|Integer|否|1|抢占式实例的保留时长，单位为小时。取值范围：0~6。

 -   保留时长2~6正在邀测中，如需开通请提交工单。
-   保留时长为0，则为无保护期模式。

 默认值：1 |
|SpotInterruptionBehavior|String|否|Terminate|抢占实例中断模式。目前仅支持Terminate（默认）直接释放实例。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|ScalingConfigurationId|String|asc-bp1ffogfdauy0nu5\*\*\*\*|伸缩配置ID。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=CreateScalingConfiguration
&ScalingGroupId=asg-bp14wlu85wrpchm0****
&SecurityGroupId=sg-280ih****
&ImageId=centos6u5_64_20G_aliaegis****.vhd
&InstanceTypes.1=ecs.g6.large
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateScalingConfigurationResponse>
      <ScalingConfigurationId>asc-bp1ffogfdauy0nu5****</ScalingConfigurationId>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</CreateScalingConfigurationResponse>
```

`JSON`格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "ScalingConfigurationId": "asc-bp1ffogfdauy0nu5****"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|400

|InstanceType.Mismatch

|The specified scaling configuration and existing active scaling configuration have different instance type.

|指定的伸缩配置的实例规格与当前的伸缩配置的实例规格不匹配。 |
|404

|InvalidDataDiskSnapshotId.NotFound

|Snapshot “XXX” does not exist.

|不存在指定的快照。 |
|400

|InvalidDataDiskSnapshotId.SizeNotSupported

|The capacity of snapshot “XXX” exceeds the size limit of the specified disk category.

|指定快照的大小超过了磁盘大小的限制。 |
|403

|InvalidDevice.InUse

|Device “XXX” has been occupied.

|数据盘挂载点重复。 |
|400

|InvalidImageId.InstanceTypeMismatch

|The specified image does not support the specified instance type.

|不允许在指定的实例规格下使用该镜像。 |
|404

|InvalidImageId.NotFound

|The specified image does not exist.

|该账号下不存在指定的镜像。 |
|400

|InvalidKeyPairName.NotFound

|The specified KeyPairName does not exist in our records.

|指定的KeyPairName不存在。 |
|400

|InvalidNetworkType.ForRAMRole

|RAMRole can't be used For classic instance.

|经典网络实例不支持RamRoleName参数。 |
|400

|InvalidParameter

|The specified value of parameter KeyPairName is not valid.

|Windows系统不支持KeyPairName参数。 |
|400

|InvalidParameter.Conflict

|The value of parameter SystemDisk.Category and parameter DataDisk.N.Category are conflict.

|指定的系统盘类型和数据盘类型冲突。 |
|400

|InvalidRamRole.NotFound

|The specified RamRoleName does not exist.

|不存在指定的RamRoleName。 |
|400

|InvalidScalingConfigurationName.Duplicate

|The specified value of parameter ScalingConfigurationName is duplicated.

|已存在相同伸缩配置名。 |
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|该账号下不存在指定的伸缩组。 |
|400

|InvalidSecurityGroupId.IncorrectNetworkType

|The network type of specified security Group does not support this action.

|指定的安全组与伸缩组指定网络类型不一致。 |
|404

|InvalidSecurityGroupId.NotFound

|The specified security group does not exist.

|该账号下不存在指定的安全组。 |
|400

|InvalidSecurityGroupId.VPCMismatch

|The specified security group and the specified virtual switch are not in the same VPC.

|指定的安全组和虚拟交换机不属于同一个虚拟专有网络。 |
|403

|InvalidSnapshot.TooOld

|This operation is denied because the specified snapshot is created before 2013-07-15.

|该快照创建于2013年7月15日或之前，调用被拒绝。 |
|403

|InvalidSystemDiskCategory.ValueUnauthorized

|The system disk category is not authorized.

|没有创建临时磁盘系统盘的权限。 |
|400

|InvalidUserData.Base64FormatInvalid

|The specified parameter UserData must be base64 encoded.

|UserData不符合Base64编码规范。 |
|400

|InvalidUserData.SizeExceeded

|The specified parameter UserData exceeds the size.

|指定的UserData过长。 |
|403

|QuotaExceeded.EphemeralDiskSize

|Ephemeral disk size quota exceeded.

|临时磁盘数据盘总容量超过2TiB（2048GiB）。 |
|400

|QuotaExceeded.ScalingConfiguration

|Scaling configuration quota exceeded in the specified scaling group.

|您目前拥有的伸缩配置个数已经达到上限。 |
|400

|QuotaExceeded.SecurityGroupInstance

|Instance quota exceeded in the specified security group.

|指定的安全组中添加的ECS实例个数已经达到上限。 |

