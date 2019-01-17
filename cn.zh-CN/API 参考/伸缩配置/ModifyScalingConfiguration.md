# ModifyScalingConfiguration {#concept_ohp_tc2_sfb .concept}

修改一个指定的伸缩配置。如果修改伸缩配置名称，请注意同一伸缩组下不能存在名称相同的伸缩配置。

## 请求参数 {#section_a2k_dp2_sfb .section}

|名称|类型|是否必选|描述|
|--|--|----|--|
|Action|String|是|操作接口名，系统规定参数，取值： ModifyScalingConfiguration。|
|ScalingConfigurationName|String|否|伸缩配置的显示名称，2-40 个英文或中文字符，以数字、大小写字母或中文开头，可包含数字、下划线（\_）、短横线（-）或点号（.）。在同一账号的同一地域下，同一伸缩组内该名称是唯一的。如果您没有指定该参数，则默认使用伸缩配置 ID。|
|InstanceName|String|否|基于当前伸缩配置创建的实例名称。|
|HostName|String|否| 云服务器的主机名，不能以点号（.）或短横线（-）开头或结束，不能连续使用点号（.）或短横线（-）。另外，不同类型实例的命名要求如下：

 -   对 Windows 实例：主机名长度为 2-15，可包含大小写字母、数字和短横线（-），不能包含点号（.），不能全是数字。
-   对其他类型（Linux 等）实例：主机名长度：2-128，可包含多个点号，两个点号之间为一段，每段可包含大小写字母、数字和短横线（-）。

 |
|ImageId|String|否|镜像文件 ID，指定启动实例时选择的镜像资源。|
|ImageName|String|否|镜像名称，同一个地域内镜像名称唯一。如果设置了ImageId参数，ImageName将被忽略。如果未设置ImageId参数，设置了ImageName，那么当前的伸缩配置镜像将以ImageName为准。|
|ScalingConfigurationId|String|是|伸缩配置 ID，指定待修改的伸缩配置。|
|InternetChargeType|String|否| 网络计费类型，可选值：

 -   PayByBandwidth：按带宽计费，此时InternetMaxBandwidthOut即为所选的固定带宽值
-   PayByTraffic：按流量计费，此时InternetMaxBandwidthOut只是一个带宽上限，计费以发生的网络流量为依据

 如果您没有指定该参数，则经典网络下默认值为PayByBandwidth，VPC 下默认值为PayByTraffic。

 |
|InternetMaxBandwidthOut|Integer|否| 公网出带宽最大值，单位为 Mbps \(Mega bit per second\)，取值范围：

 -   按带宽计费：1-100，如果您没有指定该参数，则出带宽将自动被设置为 0 Mbps
-   按流量计费：1-100，如果您没有指定该参数，则会出现报错

 |
|SystemDisk.Category|String|否| 系统盘的磁盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD 云盘
-   ephemeral\_ssd：本地 SSD 盘

 InstanceType 为系列 I 的规格且实例属于非 I/O 优化实例时，默认值：cloud。否则，默认值：cloud\_efficiency。

 |
|SystemDisk.Size|Integer|否| 系统盘大小，单位：GB。取值范围：

 -   cloud：40-500
-   cloud\_efficiency：40-500
-   cloud\_ssd：40-500
-   ephemeral\_ssd：40-500

 默认值：max\{40, ImageSize\}，指定该参数后，系统盘大小必须 ≥ max\{40, ImageSize\}。

 |
|LoadBalancerWeight|Integer|否|后端服务器的权重，取值范围：0-100，默认值：50。|
|UserData|String|否|实例自定义数据，需要以 Base64 方式编码，原始数据最多为 16 KB。|
|KeyPairName|String|否| 密钥对名称。

 -   对 Windows ECS 实例，该参数将被忽略，默认为空。
-   对 Linux ECS 实例，密码登录方式会被初始化成禁止。

 |
|RamRoleName|String|否|实例 RAM 角色名称。本名称由 RAM 提供和维护，可通过 [ListRoles](../../../../../cn.zh-CN/API参考/角色管理接口/ListRoles.md#) 查询，您还可以参考 [CreateRole](../../../../../cn.zh-CN/API参考/角色管理接口/CreateRole.md#)。|
|InstanceTypes.N|String|否|多实例规格参数。如果使用了InstanceTypes.N，InstanceType将被忽略，其中 N 的取值范围：1-10，即一个伸缩配置内最多可以设置 10 种实例规格。N 代表当前伸缩配置中实例规格的优先级，编号为 1 的实例规格优先级最高，实例规格优先级随着编号的增大依次降低。当无法根据优先级较高的实例规格创建出实例时，弹性伸缩服务会自动选择下一优先级的实例规格来创建实例。|
|Tags|String|否| 实例标签。标签以键值对方式传入，最多可以使用 5 组标签，格式：\{“key1”:”value1”,”key2”:”value2”, … “key5”:”value5”\}。Key 和 Value 的使用要求如下：

 -   Key 最多支持 64 个字符，不支持以 aliyun、http:// 和 https:// 开头。一旦使用标签，Key 不允许为空字符串。
-   Value 最多支持 128 个字符，不支持以 aliyun、http:// 和 https:// 开头。Value 可以为空字符串。

 |
|PasswordInherit|Boolean|否|是否使用镜像预设的密码。使用该参数时，您需要确保所用镜像已经预设了密码。|
|IoOptimized|String|否| 是否为 I/O 优化实例。取值范围：

 -   none：非I/O优化
-   optimized：I/O优化

 InstanceType 为 已停售的实例规格 的规格默认值：none

 InstanceType 为非系列I的规格默认值：optimized

 |
|SpotStrategy|String|否| 后付费实例的抢占策略。当参数 InstanceChargeType 取值为 PostPaid 时生效。取值范围：

 -   NoSpot：正常按量付费实例
-   SpotWithPriceLimit：设置上限价格的抢占式实例
-   SpotAsPriceGo：系统自动出价，跟随当前市场实际价格

 默认值：NoSpot。

 |
|SpotPriceLimit.N.InstanceType|String|否|抢占式实例的实例规格，其中 N 的取值范围：1-10。SpotStrategy 取值为 SpotWithPriceLimit 时生效。|
|SpotPriceLimit.N.PriceLimit|Float|否|抢占式实例对应的出价，其中 N 的取值范围：1-10。SpotStrategy 取值为 SpotWithPriceLimit 时生效。|
|DataDisk.N.Category|String|否| 数据盘 N 的磁盘种类。取值范围：

 -   cloud：普通云盘，随实例创建的普通云盘的DeleteWithInstance属性为true
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD 云盘
-   ephemeral\_ssd：本地 SSD 盘

 默认值：cloud。

 |
|DataDisk.N.Size|Integer|否| 数据盘 N 的磁盘大小，单位：GB。N 从 1 开始编号，最多 16 块。取值范围：

 -   cloud：5-2000
-   cloud\_efficiency：20-32768
-   cloud\_ssd：20-32768
-   ephemeral\_ssd：5-800

 指定该参数后，磁盘大小必须 ≥ 快照大小（快照通过SnapshotId指定）。

 |
|DataDisk.N.SnapshotId|String|否|创建数据盘使用的快照，N 取值：1-4。指定该参数后DataDisk.N.Size会被忽略，实际创建的磁盘大小为指定快照的大小。如果该快照创建于2013年7月15日或之前，该次调用会被拒绝，返回参数中最多可以输入 4 个InvalidSnapshot.TooOld。|
|DataDisk.N.Device|String|否|数据盘挂载点，N 取值：1-4。如果您没有指定该参数，则默认在自动创建 ECS 实例时由 ECS 系统分配，从/dev/xvdb开始到/dev/xvdz。|
|DataDisk.n.DeleteWithInstance|Boolean|否| 指定数据盘是否随实例释放。取值范围：

 -   true：释放实例时，该磁盘随实例一起释放
-   false：释放实例时，该磁盘保留不释放

 默认值：true，该参数只可对独立云盘（DataDisk.n.Category为cloud、cloud\_efficiency或cloud\_ssd）设置，否则会出现报错。

 |

## 返回参数 {#section_jzw_252_sfb .section}

|名称|类型|描述|
|--|--|--|
|RequestId|String|请求 ID，由系统生成。|

## 示例 {#section_oyq_352_sfb .section}

请求示例

```
http://ess.aliyuncs.com/?Action=ModifyScalingConfiguration
&ScalingConfigurationId=asc-xxxxxxxxxxxxxx
&ScalingConfigurationName=test-modify
&ImageId=centos6u5_64_20G_aliaegis_20140703.vhd
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ModifyScalingConfigurationResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyScalingConfigurationResponse>
```

`JSON` 格式

```
{
    "requestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 {#section_kkw_s52_sfb .section}

对于所有接口的通用性错误，请参考 [客户端错误](cn.zh-CN/API 参考/错误代码/客户端错误.md#) 或 [服务器端错误](cn.zh-CN/API 参考/错误代码/服务器端错误.md#)。

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|未授权操作当前Action。|
|404|InvalidDataDiskSnapshotId.NotFound|Snapshot “XXX” does not exist.|不存在指定的快照。|
|400|InvalidDataDiskSnapshotId.SizeNotSupported|The capacity of snapshot “XXX” exceeds the size limit of the specified disk category.|指定快照的大小超过了磁盘大小的限制。|
|404|InvalidImageId.NotFound|The specified image does not exist.|指定的镜像不存在。|
|400|InvalidKeyPairName.NotFound|The specified KeyPairName does not exist in our records.|指定的KeyPairName不存在。|
|400|InvalidNetworkType.ForRAMRole|RAMRole can’t be used For classic instance.|经典网络实例不支持RamRoleName参数。|
|400|InvalidParamter|The specified value of parameter is not valid.|指定的参数值无效。|
|400|InvalidScalingConfigurationName.Duplicate|The specified value of parameter is duplicated.|伸缩配置名已存在。|
|400|InvalidSecurityGroupId.IncorrectNetworkType|The network type of specified Security Group does not support this action.|指定的安全组与伸缩组指定网络类型不一致。|
|400|InvalidSecurityGroupId.VPCMismatch|The specified security group and the specified virtual switch are not in the same VPC.|指定的安全组和虚拟交换机不属于同一个虚拟专有网络。|
|400|InvalidTags.KeyValue|The specified tags key/value cannot be empty.|必须指定Tags参数。|
|400|InvalidTags.ListSize|The specified tags list size cannot be more than “5”.|Tags列表长度超过限制长度。|
|400|InvalidUserData.Base64FormatInvalid|The specified parameter UserData must be base64 encoded.|UserData不符合 Base64 编码规范。|
|400|InvalidUserData.SizeExceeded|The specified parameter UserData exceeds the size.|指定的UserData过长。|

