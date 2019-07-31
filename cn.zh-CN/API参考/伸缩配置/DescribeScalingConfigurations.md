# DescribeScalingConfigurations {#doc_api_Ess_DescribeScalingConfigurations .reference}

调用DescribeScalingConfigurations查询现有的伸缩配置。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DescribeScalingConfigurations&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-qingdao|伸缩配置所属伸缩组的地域ID。

 |
|Action|String|否|DescribeScalingConfigurations|系统规定参数，取值：DescribeScalingConfigurations。

 |
|PageNumber|Integer|否|1|伸缩配置列表的页码。起始值：1。

 默认值：1 。

 |
|PageSize|Integer|否|50|分页查询时设置的每页行数。最大值：50。

 默认值：10。

 |
|ScalingConfigurationId.1|String|否|bU5uZHcAgtzwcL4IeDea\*\*\*\*|ScalingConfigurationId.N为待查询伸缩配置的ID，N的取值范围：1～10。查询结果包括生效和失效的伸缩配置，并通过返回参数LifecycleState进行标识。

 |
|ScalingConfigurationName.1|String|否|c1908dd1-690f-4c9b-ab73-350f1f06\*\*\*\*|ScalingConfigurationName.N为待查询伸缩配置的名称，N的取值范围：1～20。查询结果会忽略失效的伸缩配置名称，并且不报错。

 |
|ScalingGroupId|String|否|dE9YbOdCHqaFdFZHXVdD\*\*\*\*|伸缩组的ID，您可以查询该伸缩组下所有的伸缩配置。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|当前页码。

 |
|PageSize|Integer|50|每页行数。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |
|ScalingConfigurations| | |伸缩配置信息的集合。

 |
|Cpu|Integer|2|vCPU个数。

 同时指定CPU和Memory可以定义实例规格范围，例如，CPU=2且Memory=16可以定义配置为2 vCPU和16 GiB的所有实例规格。弹性伸缩会结合IO优化、可用区等因素确定可用实例规格集合，并根据价格排序为您创建价格最低的实例。

 **说明：** 该区间配置效果仅在成本优化模式下且伸缩配置未设置实例规格时生效。

 |
|CreationTime|String|2014-08-14T10:58Z|伸缩配置的创建时间。

 |
|DataDisks| | |数据盘信息的集合。

 |
|Category|String|cloud|数据盘的磁盘种类，取值范围：

 -   cloud：普通云盘。随实例创建的普通云盘的DeleteWithInstance属性为true。
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘

 |
|DeleteWithInstance|Boolean|true|数据盘是否随实例释放，取值范围：

 -   true：释放实例时，该磁盘随实例一起释放。
-   false：释放实例时，该磁盘保留不释放。

 |
|Description|String|FinanceDept|数据盘的描述。

 |
|Device|String|/dev/xvdb|数据盘的挂载点。

 |
|DiskName|String|cloud\_ssdData|数据盘的名称。

 |
|Encrypted|String|false|数据盘是否加密，取值范围：

 -   true：加密
-   false：不加密

 |
|KMSKeyId|String|0e478b7a-4262-4802-b8cb-00d3fb40826X|数据盘对应的KMS密钥的ID。

 |
|Size|Integer|200|数据盘的磁盘大小，内存单位为GiB。取值范围：

 -   cloud：5~2000
-   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   ephemeral\_ssd：5~800

 |
|SnapshotId|String|s-23f2i\*\*\*\*|创建数据盘使用的快照ID。

 |
|DeploymentSetId|String|ds-bp1frxuzdg87zh4p\*\*\*\*|ECS实例所属的部署集的ID。

 |
|HostName|String|LocalHost|云服务器的主机名。

 |
|HpcClusterId|String|hpc-clusterid|ECS实例所属的EHPC集群的ID。

 |
|ImageId|String|centos6u5\_64\_20G\_aliaegis\_20140703.vhd|镜像文件ID，自动创建实例时使用的镜像资源。

 |
|ImageName|String|centos6u5\_64\_20G\_aliaegis\_20140703.vhd|镜像文件名称。

 |
|InstanceDescription|String|FinaceDept|ECS实例的描述。

 |
|InstanceGeneration|String|ecs-3|ECS实例的系列。

 |
|InstanceName|String|fortest|ECS实例的名称。

 |
|InstanceType|String|ecs.t1.xsmall|ECS实例的实例规格。

 |
|InstanceTypes| |ecs.t1.xsmall|ECS实例的实例规格的集合。

 |
|InternetChargeType|String|PayByTraffic|网络计费类型，取值范围：

 -   PayByBandwidth：按带宽计费。此时InternetMaxBandwidthOut即为所选的固定带宽值。
-   PayByTraffic：按流量计费。此时InternetMaxBandwidthOut只是一个带宽上限，计费以实际产生的网络流量为依据。

 |
|InternetMaxBandwidthIn|Integer|200|公网入带宽最大值，单位为Mbps \(Mega bit per second\)，取值范围：1~200。

 |
|InternetMaxBandwidthOut|Integer|0|公网出带宽最大值，单位为Mbps \(Mega bit per second\)，取值范围：

 -   按带宽计费：0~100，如果您没有指定该参数，则出带宽将自动被设置为0Mbps。
-   按流量计费：0~100，如果您没有指定该参数，则会出现报错。

 |
|IoOptimized|String|none|是否为I/O优化实例。

 |
|KeyPairName|String|fortest|登录ECS实例时使用的密钥对的名称。

 |
|LifecycleState|String|Active|伸缩配置在伸缩组中的状态，取值范围：

 -   Active：生效状态。伸缩组会使用处于生效状态的伸缩配置自动创建ECS实例。
-   Inacitve：失效状态。处于失效状态的伸缩配置存在于伸缩组中，但伸缩组不会使用此类伸缩配置自动创建ECS实例。

 |
|LoadBalancerWeight|Integer|1|后端服务器的权重，取值范围：0~100。

 |
|Memory|Integer|16|内存大小。

 同时指定CPU和Memory可以定义实例规格范围，例如，CPU=2且Memory=16可以定义配置为2 vCPU和16 GiB的所有实例规格。弹性伸缩会结合IO优化、可用区等因素确定可用实例规格集合，并根据价格排序为您创建价格最低的实例。

 **说明：** 该区间配置效果仅在成本优化模式下且伸缩配置未设置实例规格时生效。

 |
|PasswordInherit|Boolean|true|是否使用镜像预设的密码。

 |
|RamRoleName|String|RamRoleTest|ECS实例的RAM角色名称。RAM角色名称由RAM提供和维护，您可调用[ListRoles](~~28713~~)查询可用的RAM角色。创建RAM角色的方法请参见[CreateRole](~~28710~~)。

 |
|ResourceGroupId|String|abcd1234abcd\*\*\*\*|ECS实例所属资源组的ID。

 |
|ScalingConfigurationId|String|bU5uZHcAgtzwcL4IeDea\*\*\*\*|伸缩配置的ID。

 |
|ScalingConfigurationName|String|c1908dd1-690f-4c9b-ab73-350f1f06\*\*\*\*|伸缩配置的名称。

 |
|ScalingGroupId|String|sg-280ih\*\*\*\*|伸缩配置所属伸缩组的ID。

 |
|SecurityEnhancementStrategy|String|Active|是否开启安全加固。取值范围：

 -   Active：启用安全加固，只对公共镜像生效。
-   Deactive：不启用安全加固，对所有镜像类型生效。

 |
|SecurityGroupId|String|sg-280ih\*\*\*\*|ECS实例所属的安全组的ID，同一个安全组内的ECS实例可以互相访问。

 |
|SecurityGroupIds| |sg-bp18kz60mefs\*\*\*\*|ECS实例所属的多个安全组的ID，同一个安全组内的ECS实例可以互相访问。

 |
|SpotPriceLimit| | |抢占式实例信息的集合。

 |
|InstanceType|String|ecs.t1.xsmall|抢占式实例的实例规格。

 |
|PriceLimit|Float|0.125|抢占式实例对应的出价。

 |
|SpotStrategy|String|NoSpot|后付费实例的抢占策略。取值范围：

 -   NoSpot：普通的按量付费实例。
-   SpotWithPriceLimit：设置上限价格的抢占式实例。
-   SpotAsPriceGo：系统自动出价，跟随当前市场实际价格。

 |
|SystemDiskCategory|String|cloud|系统盘的磁盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘

 |
|SystemDiskDescription|String|FinanceDept|系统盘的描述。

 |
|SystemDiskName|String|cloud\_ssdSystem|系统盘的名称。

 |
|SystemDiskSize|Integer|100|系统盘的磁盘大小。

 |
|Tags| | |标签信息的集合。

 |
|Key|String|binary|标签键。

 |
|Value|String|alterTable|标签值。

 |
|UserData|String|echo hello ecs!|ECS实例的自定义数据。

 |
|TotalCount|Integer|1|伸缩配置的总数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=DescribeScalingConfigurations
&RegionId=cn-qingdao
&<公共请求参数>

```

正常返回示例

`XML` 格式

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

`JSON` 格式

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
				"DataDisk":{
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

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

