# ModifyScalingConfiguration {#doc_api_Ess_ModifyScalingConfiguration .reference}

调用ModifyScalingConfiguration修改一个伸缩配置。

## 接口说明 {#description .section}

如果修改伸缩配置的名称，请注意同一伸缩组下不能存在名称相同的伸缩配置。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=ModifyScalingConfiguration&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ScalingConfigurationId|String|是|asc-\*\*\*\*|待修改伸缩配置的ID。

 |
|Action|String|否|ModifyScalingConfiguration|系统规定参数，取值： ModifyScalingConfiguration。

 |
|Cpu|Integer|否|2|vCPU个数。

 同时指定CPU和Memory可以定义实例规格范围，例如，CPU=2且Memory=16可以定义配置为2 vCPU和16 GiB的所有实例规格。弹性伸缩会结合IO优化、可用区等因素确定可用实例规格集合，并根据价格排序为您创建价格最低的实例。

 **说明：** 该区间配置效果仅在成本优化模式下且伸缩配置未设置实例规格时生效。

 |
|DataDisk.N.Category|String|否|cloud\_ssd|数据盘N的磁盘种类，N的取值范围：1~16。该参数取值范围：

 -   cloud：普通云盘。随实例创建的普通云盘的DeleteWithInstance属性为true。
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘

 |
|DataDisk.N.DeleteWithInstance|Boolean|否|true|指定数据盘是否随实例释放，N的取值范围：1~16。该参数取值范围：

 -   true：释放实例时，该磁盘随实例一起释放。
-   false：释放实例时，该磁盘保留不释放。

 该参数只可对独立云盘设置（DataDisk.N.Category为cloud、cloud\_efficiency或cloud\_ssd），否则会出现报错。

 |
|DataDisk.N.Description|String|否|FinanceDept|数据盘的描述，N的取值范围：1~16。长度为2~256个英文或中文字符，不能以 http:// 和 https:// 开头。

 |
|DataDisk.N.Device|String|否|/dev/xvdb|数据盘挂载点，N的取值范围：1~16。如果您没有指定该参数，则默认在自动创建ECS实例时由系统分配，从/dev/xvdb开始，到/dev/xvdz结束。

 |
|DataDisk.N.DiskName|String|否|cloud\_ssdData|数据盘的名称，N的取值范围：1~16。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 |
|DataDisk.N.Encrypted|String|否|false|数据盘N是否加密，N的取值范围：1~16。该参数取值范围：

 -   true：加密
-   false：不加密

 |
|DataDisk.N.KMSKeyId|String|否|0e478b7a-4262-4802-b8cb-00d3fb40826X|数据盘对应的KMS密钥的ID，N的取值范围：1~16。

 |
|DataDisk.N.Size|Integer|否|100|数据盘N的磁盘大小，N的取值范围：1~16，内存单位为GiB。取值范围：

 -   cloud：5~2000
-   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   ephemeral\_ssd：5~800

 指定该参数后，磁盘大小必须 ≥ 快照大小（快照通过SnapshotId指定）。

 |
|DataDisk.N.SnapshotId|String|否|s-snapshot\*\*\*\*|创建数据盘时使用的快照，N的取值范围：1~16。指定该参数后，DataDisk.N.Size会被忽略，实际创建的磁盘大小为指定快照的大小。

 如果该快照创建于2013年7月15日或之前，调用会被拒绝，返回参数中会提示InvalidSnapshot.TooOld。

 |
|DeploymentSetId|String|否|ds-bp13v7bjnj9gis\*\*\*\*|ECS实例所属的部署集的ID。

 |
|HostName|String|否|Joshu\*\*\*\*|云服务器的主机名。点号（.）或连字符（-）不能作为首尾字符，不能连续使用点号（.）或连字符（-）。另外，不同类型实例的命名要求如下：

 -   Windows实例：主机名长度为2~15，可以包含大小写字母、数字和连字符（-）。不能包含点号（.），不能全是数字。
-   其他类型实例（Linux等）：主机名长度为2~64，可以包含多个点号（.）。两个点号（.）之间为一段，每段可以包含大小写字母、数字和连字符（-）。

 |
|HpcClusterId|String|否|hpc-clusterid|ECS实例所属的EHPC集群的ID。

 |
|ImageId|String|否|centos6u5\_64\_20G\_aliaegis\_20140703.vhd|镜像文件ID，自动创建实例时使用的镜像资源。

 |
|ImageName|String|否|suse11sp3\_64\_20G\_aliaegis\_20150428.vhd|镜像文件名称，同一个地域内镜像名称唯一。如果设置了ImageId， ImageName将被忽略。

 不支持通过ImageName设置镜像市场镜像。

 |
|InstanceDescription|String|否|FinaceDept|ECS实例的描述。长度为2~256个英文或中文字符，不能以 http:// 和 https:// 开头。

 |
|InstanceName|String|否|Joshu\*\*\*\*|使用本伸缩配置自动创建的ECS实例的名称。

 |
|InstanceTypes.N|RepeatList|否|ecs.t1.xsmall|多实例规格参数。如果使用了InstanceTypes.N，InstanceType将被忽略，其中N的取值范围：1~10，即一个伸缩配置内最多可以设置10种实例规格。

 N代表当前伸缩配置中实例规格的优先级，编号为1的实例规格优先级最高，实例规格优先级随着编号的增大依次降低。当无法根据优先级较高的实例规格创建出实例时，弹性伸缩服务会自动选择下一优先级的实例规格来创建实例。

 |
|InternetChargeType|String|否|PayByBandwidth|网络计费类型，取值范围：

 -   PayByBandwidth：按带宽计费。此时InternetMaxBandwidthOut即为所选的固定带宽值。
-   PayByTraffic：按流量计费。此时InternetMaxBandwidthOut只是一个带宽上限，计费以实际产生的网络流量为依据。

 |
|InternetMaxBandwidthOut|Integer|否|50|公网出带宽最大值，单位为Mbps \(Mega bit per second\)，取值范围：

 -   按带宽计费：0~100，如果您没有指定该参数，则出带宽将自动被设置为0Mbps。
-   按流量计费：0~100，如果您没有指定该参数，则会出现报错。

 |
|IoOptimized|String|否|none|是否为I/O优化实例。取值范围：

 -   none：非I/O优化实例。
-   optimized：I/O优化实例。

 |
|KeyPairName|String|否|null|登录ECS实例时使用的密钥对的名称。

 -   对Windows实例，该参数将被忽略，默认为空。
-   对Linux实例，密码登录方式会被初始化成禁止。

 |
|LoadBalancerWeight|Integer|否|50|后端服务器的权重，取值范围：0~100。

 |
|Memory|Integer|否|16|内存大小。

 同时指定CPU和Memory可以定义实例规格范围，例如，CPU=2且Memory=16可以定义配置为2 vCPU和16 GiB的所有实例规格。弹性伸缩会结合IO优化、可用区等因素确定可用实例规格集合，并根据价格排序为您创建价格最低的实例。

 **说明：** 该区间配置效果仅在成本优化模式下且伸缩配置未设置实例规格时生效。

 |
|Override|Boolean|否|true|是否覆盖。取值范围：

 -   true
-   false

 |
|PasswordInherit|Boolean|否|false|是否使用镜像预设的密码。使用该参数时，您需要确保使用的镜像已经设置了密码。

 |
|RamRoleName|String|否|RamRoleTest|ECS实例的RAM角色名称。RAM角色名称由RAM提供和维护，您可调用[ListRoles](~~28713~~)查询可用的RAM角色。创建RAM角色的方法请参见[CreateRole](~~28710~~)。

 |
|ResourceGroupId|String|否|abcd1234abcd\*\*\*\*|ECS实例所属资源组的ID。

 |
|ScalingConfigurationName|String|否|test-modify|伸缩配置的名称，2~40个英文或中文字符，以数字、大小写字母或中文开头，可包含数字、下划线（\_）、连字符（-）或点号（.）。

 在同一地域下同一伸缩组内伸缩配置名称唯一。如果您没有指定该参数，则默认使用伸缩配置的ID。

 |
|SecurityGroupId|String|否|sg-F876F\*\*\*\*|ECS实例所属的安全组的ID，同一个安全组内的ECS实例可以互相访问。

 |
|SecurityGroupIds.N|RepeatList|否|sg-bp18kz60mefs\*\*\*\*|将ECS实例同时加入多个安全组。N的取值范围与实例能够加入安全组上限有关。更多详情，请参见[使用限制](~~25412~~)下的安全组章节。

 **说明：** 不支持同时指定SecurityGroupId和SecurityGroupIds.N。

 |
|SpotPriceLimit.N.InstanceType|String|否|ecs.t1.small|抢占式实例的实例规格，N的取值范围：1~10。SpotStrategy取值为SpotWithPriceLimit时生效。

 |
|SpotPriceLimit.N.PriceLimit|Float|否|0.125|抢占式实例对应的出价，N的取值范围：1~10。SpotStrategy取值为SpotWithPriceLimit时生效。

 |
|SpotStrategy|String|否|NoSpot|后付费实例的抢占策略。取值范围：

 -   NoSpot：普通的按量付费实例。
-   SpotWithPriceLimit：设置上限价格的抢占式实例。
-   SpotAsPriceGo：系统自动出价，跟随当前市场实际价格。

 |
|SystemDisk.Category|String|否|cloud\_efficiency|系统盘的磁盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘

 |
|SystemDisk.Description|String|否|FinanceDept|系统盘的描述。长度为2~256个英文或中文字符，不能以 http:// 和 https:// 开头。

 |
|SystemDisk.DiskName|String|否|cloud\_ssdSystem|系统盘的名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 |
|SystemDisk.Size|Integer|否|50|系统盘的大小，单位：GiB。取值范围：

 -   cloud：40~500
-   cloud\_efficiency：40~500
-   cloud\_ssd：40~500
-   ephemeral\_ssd：40~500

 指定该参数后，系统盘大小必须 ≥ max\{40, ImageSize\}。

 |
|Tags|String|否|“key1”:”value1”|ECS实例的标签。标签以键值对方式传入，最多可以使用5组标签。Key和Value的使用要求如下：

 -   Key最多支持64个字符，不能以aliyun和acs:开头，不能包含 http:// 或者 https:// 。一旦使用标签，Key不允许为空字符串。
-   Value最多支持128个字符，不能以aliyun和acs:开头，不能包含 http:// 或者 https:// 。Value可以为空字符串。

 |
|UserData|String|否|echo hello ecs!|ECS实例的自定义数据，需要以Base64方式编码，编码前的原始数据最多为16KB。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=ModifyScalingConfiguration
&ScalingConfigurationId=asc-****
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

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

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

|指定的KeyPairName不存在。

|
|400

|InvalidNetworkType.ForRAMRole

|RAMRole can’t be used For classic instance.

|经典网络实例不支持RamRoleName参数。

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

|必须指定Tags参数。

|
|400

|InvalidTags.ListSize

|The specified tags list size cannot be more than “5”.

|Tags列表长度超过限制长度。

|
|400

|InvalidUserData.Base64FormatInvalid

|The specified parameter UserData must be base64 encoded.

|UserData不符合Base64编码规范。

|
|400

|InvalidUserData.SizeExceeded

|The specified parameter UserData exceeds the size.

|指定的UserData过长。

|

