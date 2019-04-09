# ModifyScalingConfiguration {#doc_api_Ess_ModifyScalingConfiguration .reference}

修改一个指定的伸缩配置。如果修改伸缩配置名称，请注意同一伸缩组下不能存在名称相同的伸缩配置。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=ModifyScalingConfiguration)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ScalingConfigurationId|String|是|asc-\*\*\*\*|伸缩配置 ID，指定待修改的伸缩配置。

 |
|Action|String|否|ModifyScalingConfiguration|操作接口名，系统规定参数，取值： ModifyScalingConfiguration。

 |
|Cpu|Integer|否|12|vCPU 的个数。

 |
|DataDisk.N.Category|String|否|cloud\_ssd|数据盘 N 的磁盘种类。取值范围：

 -   cloud：普通云盘，随实例创建的普通云盘的 DeleteWithInstance 属性为 true
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD 云盘
-   ephemeral\_ssd：本地 SSD 盘

 默认值：cloud

 |
|DataDisk.N.DeleteWithInstance|Boolean|否|true|指定数据盘是否随实例释放。取值范围：

 -   true：释放实例时，该磁盘随实例一起释放
-   false：释放实例时，该磁盘保留不释放

 默认值：true，该参数只可对独立云盘（**DataDisk.n.Category** 为 cloud、cloud\_efficiency 或 cloud\_ssd）设置，否则会出现报错。

 |
|DataDisk.N.Device|String|否|/dev/xvdb|数据盘挂载点，N 取值：1~4。如果您没有指定该参数，则默认在自动创建 ECS 实例时由 ECS 系统分配，从 /dev/xvdb 开始到 /dev/xvdz。

 |
|DataDisk.N.Size|Integer|否|100|数据盘 N 的磁盘大小，单位：GB。N 从 1 开始编号，最多 16 块。取值范围：

 -   cloud：5-2000
-   cloud\_efficiency：20-32768
-   cloud\_ssd：20-32768
-   ephemeral\_ssd：5-800

 指定该参数后，磁盘大小必须 ≥ 快照大小（快照通过 **SnapshotId** 指定）。

 |
|DataDisk.N.SnapshotId|String|否|s-snapshot\*\*\*\*|创建数据盘使用的快照，N 取值：1~4。指定该参数后 **DataDisk.N.Size** 会被忽略，实际创建的磁盘大小为指定快照的大小。如果该快照创建于 2013 年 7 月 15 日或之前，该次调用会被拒绝，返回参数中最多可以输入 4 个 **InvalidSnapshot.TooOld**。

 |
|DeploymentSetId|String|否|ds-bp13v7bjnj9gis\*\*\*\*|部署集 ID。

 |
|HostName|String|否|Joshu\*\*\*\*|云服务器的主机名，不能以点号（.）或短横线（-）开头或结束，不能连续使用点号（.）或短横线（-）。另外，不同类型实例的命名要求如下：

 -   对 Windows 实例：主机名长度为 2~15，可包含大小写字母、数字和短横线（-），不能包含点号（.），不能全是数字。
-   对其他类型（Linux 等）实例：主机名长度：2~128，可包含多个点号，两个点号之间为一段，每段可包含大小写字母、数字和短横线（-）。

 |
|ImageId|String|否|centos6u5\_64\_20G\_aliaegis\_20140703.vhd|镜像文件 ID，指定启动实例时选择的镜像资源。

 |
|ImageName|String|否|suse11sp3\_64\_20G\_aliaegis\_20150428.vhd|镜像名称，同一个地域内镜像名称唯一。如果设置了 **ImageId** 参数，**ImageName** 将被忽略。如果未设置 **ImageId** 参数，设置了 **ImageName**，那么当前的伸缩配置镜像将以 **ImageName** 为准。

 |
|InstanceName|String|否|Joshu\*\*\*\*|基于当前伸缩配置创建的实例名称。

 |
|InstanceTypes.N|RepeatList|否|ecs.t1.xsmall|多实例规格参数。如果使用了 **InstanceTypes.N**，**InstanceType** 将被忽略，其中 N 的取值范围：1~10，即一个伸缩配置内最多可以设置 10 种实例规格。N 代表当前伸缩配置中实例规格的优先级，编号为 1 的实例规格优先级最高，实例规格优先级随着编号的增大依次降低。当无法根据优先级较高的实例规格创建出实例时，弹性伸缩服务会自动选择下一优先级的实例规格来创建实例。

 |
|InternetChargeType|String|否|PayByBandwidth|网络计费类型，可选值：

 -   PayByBandwidth：按带宽计费，此时 **InternetMaxBandwidthOut** 即为所选的固定带宽值
-   PayByTraffic：按流量计费，此时 **InternetMaxBandwidthOut** 只是一个带宽上限，计费以发生的网络流量为依据

 如果您没有指定该参数，则经典网络下默认值为 PayByBandwidth，VPC 下默认值为 PayByTraffic。

 |
|InternetMaxBandwidthOut|Integer|否|50|公网出带宽最大值，单位为 Mbps \(Mega bit per second\)，取值范围：

 -   按带宽计费：1~100，如果您没有指定该参数，则出带宽将自动被设置为 0 Mbps
-   按流量计费：1~100，如果您没有指定该参数，则会出现报错

 |
|IoOptimized|String|否|none|是否为 I/O 优化实例。取值范围：

 -   none：非 I/O 优化
-   optimized：I/O 优化

 如果 **InstanceType** 为已停售的实例规格的规格，默认值：none。

 如果 **InstanceType** 为非系列 I 的规格，默认值：optimized 。

 |
|KeyPairName|String|否|null|密钥对名称。

 -   对 Windows ECS 实例，该参数将被忽略，默认为空。
-   对 Linux ECS 实例，密码登录方式会被初始化成禁止。

 |
|LoadBalancerWeight|Integer|否|50|后端服务器的权重，取值范围：0~100，默认值：50。

 |
|Memory|Integer|否|48|内存大小。

 |
|Override|Boolean|否|true|是否覆盖。取值范围：

 -   true
-   false

 |
|PasswordInherit|Boolean|否|false|是否使用镜像预设的密码。使用该参数时，您需要确保所用镜像已经预设了密码。

 |
|RamRoleName|String|否|RamRoleTest|实例 RAM 角色名称。本名称由 RAM 提供和维护，可通过 [ListRoles](~~28713~~) 查询，您还可以参考 [CreateRole](~~28710~~)。

 |
|ResourceGroupId|String|否|abcd1234abcd\*\*\*\*|资源组 ID。

 |
|ScalingConfigurationName|String|否|test-modify|伸缩配置的显示名称，2~40 个英文或中文字符，以数字、大小写字母或中文开头，可包含数字、下划线（\_）、短横线（-）或点号（.）。在同一账号的同一地域下，同一伸缩组内该名称是唯一的。如果您没有指定该参数，则默认使用伸缩配置 ID。

 |
|SecurityGroupId|String|否|sg-F876F\*\*\*\*|安全组 ID。

 |
|SpotPriceLimit.N.InstanceType|String|否|ecs.t1.small|抢占式实例的实例规格，其中 N 的取值范围：1~10。

 SpotStrategy 取值为 SpotWithPriceLimit 时生效。

 |
|SpotPriceLimit.N.PriceLimit|Float|否|0.125|抢占式实例对应的出价，其中 N 的取值范围：1~10。**SpotStrategy** 取值为 SpotWithPriceLimit 时生效。

 |
|SpotStrategy|String|否|NoSpot|后付费实例的抢占策略。当参数 **InstanceChargeType** 取值为 PostPaid 时生效。取值范围：

 -   NoSpot：正常按量付费实例
-   SpotWithPriceLimit：设置上限价格的抢占式实例
-   SpotAsPriceGo：系统自动出价，跟随当前市场实际价格

 默认值：NoSpot

 |
|SystemDisk.Category|String|否|cloud\_efficiency|系统盘的磁盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD 云盘
-   ephemeral\_ssd：本地 SSD 盘

 如果 **InstanceType** 为系列 I 的规格且实例属于非 I/O 优化实例，默认值：cloud。否则，默认值：cloud\_efficiency。

 |
|SystemDisk.Size|Integer|否|50|系统盘大小，单位：GB。取值范围：

 -   cloud：40~500
-   cloud\_efficiency：40~500
-   cloud\_ssd：40~500
-   ephemeral\_ssd：40~500

 默认值：max\{40, ImageSize\}，指定该参数后，系统盘大小必须 ≥ max\{40, ImageSize\}。

 |
|Tags|String|否|“key1”:”value1”|实例标签。标签以键值对方式传入，最多可以使用 5 组标签，格式：\{“key1”:”value1”,”key2”:”value2”, … “key5”:”value5”\}。Key 和 Value 的使用要求如下：

 -   Key 最多支持 64 个字符，不支持以 aliyun、http:// 和 https:// 开头。一旦使用标签，Key 不允许为空字符串。
-   Value 最多支持 128 个字符，不支持以 aliyun、http:// 和 https:// 开头。Value 可以为空字符串。

 |
|UserData|String|否|echo hello ecs!|实例自定义数据，需要以 Base64 方式编码，原始数据最多为 16 KB。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=ModifyScalingConfiguration
&ScalingConfigurationId=asc-****
&ScalingConfigurationName=test-modify
&ImageId=centos6u5_64_20G_aliaegis_20140703.vhd
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyScalingConfigurationResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyScalingConfigurationResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ess)

|HttpCode

|错误码

|错误信息

|描述

|
|----------|-----|------|----|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|未授权操作当前Action。

|
|404

|InvalidDataDiskSnapshotId.NotFound

|Snapshot “XXX” does not exist.

|不存在指定的快照。

|
|400

|InvalidDataDiskSnapshotId.SizeNotSupported

|The capacity of snapshot “XXX” exceeds the size limit of the specified disk category.

|指定快照的大小超过了磁盘大小的限制。

|
|404

|InvalidImageId.NotFound

|The specified image does not exist.

|指定的镜像不存在。

|
|400

|InvalidKeyPairName.NotFound

|The specified KeyPairName does not exist in our records.

|指定的 KeyPairName 不存在。

|
|400

|InvalidNetworkType.ForRAMRole

|RAMRole can’t be used For classic instance.

|经典网络实例不支持 RamRoleName 参数。

|
|400

|InvalidParamter

|The specified value of parameter is not valid.

|指定的参数值无效。

|
|400

|InvalidScalingConfigurationName.Duplicate

|The specified value of parameter is duplicated.

|伸缩配置名已存在。

|
|400

|InvalidSecurityGroupId.IncorrectNetworkType

|The network type of specified Security Group does not support this action.

|指定的安全组与伸缩组指定网络类型不一致。

|
|400

|InvalidSecurityGroupId.VPCMismatch

|The specified security group and the specified virtual switch are not in the same VPC.

|指定的安全组和虚拟交换机不属于同一个虚拟专有网络。

|
|400

|InvalidTags.KeyValue

|The specified tags key/value cannot be empty.

|必须指定 Tags 参数。

|
|400

|InvalidTags.ListSize

|The specified tags list size cannot be more than “5”.

|Tags 列表长度超过限制长度。

|
|400

|InvalidUserData.Base64FormatInvalid

|The specified parameter UserData must be base64 encoded.

|UserData 不符合 Base64 编码规范。

|
|400

|InvalidUserData.SizeExceeded

|The specified parameter UserData exceeds the size.

|指定的 UserData 过长。

|

