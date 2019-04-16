# DescribeScalingConfigurations {#concept_25945_zh .concept}

查询伸缩配置的信息。

## 描述 {#section_qcc_fgk_sfb .section}

查询时可以指定伸缩组ID来查询该伸缩组下的所有伸缩配置。

伸缩配置具有以下几种状态（LifecycleState）：

-   Active：生效状态，伸缩组会采用处于生效状态的伸缩配置自动创建ECS实例。
-   Inacitve：失效状态，该伸缩配置存在于伸缩组中，但伸缩组不会采用处于失效状态的伸缩配置自动创建ECS实例。

## 请求参数 {#section_blm_ggk_sfb .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：DescribeScalingConfigurations。|
|RegionId|String|是|伸缩配置所属伸缩组的地域ID。|
|ScalingGroupId|String|否|伸缩组的ID。|
|ScalingConfigurationId.N|String|否|伸缩配置的ID，最多可以输入10个。查询结果包括生效和失效的伸缩配置的ID，并通过返回参数`LifecycleState`进行标识。|
|ScalingConfigurationName.N|String|否|伸缩配置的名称，最多可以输入10个。查询结果会忽略失效的伸缩配置的名称，并且不报错。|
|PageNumber|Integer|否|伸缩配置列表的页码，起始值为1，默认值为1。|
|PageSize|Integer|否|分页查询时设置的每页行数，最大值50行，默认值为10。|

## 返回参数 {#section_dbx_3gk_sfb .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|伸缩配置总数。|
|PageNumber|Integer|当前页码。|
|PageSize|Integer|每页行数。|
|ScalingConfigurations|ScalingConfigurationSetType|伸缩配置信息组成的集合。|

ScalingConfigurationSetType是由ScalingConfigurationItemType类型组成的集合。

|名称|类型|描述|
|:-|:-|:-|
|ScalingConfiguration|ScalingConfigurationItemType|伸缩配置信息。|

ScalingConfigurationItemType类型的属性如下表所示。

|名称|类型|描述|
|:-|:-|:-|
|ScalingConfigurationId|String|伸缩配置的ID。|
|ScalingConfigurationName|String|伸缩配置的显示名称。|
|ScalingGroupId|String|伸缩配置所属的伸缩组ID。|
|ImageId|String|镜像文件ID。|
|InstanceType|String|实例的资源规则。|
|SecurityGroupId|String|安全组ID。|
|InternetChargeType|String|网络计费类型。|
|InternetMaxBandwidthIn|Integer|公网入带宽最大值，单位为Mbps\(Mega bit per second\)。|
|InternetMaxBandwidthOut|Integer|公网出带宽最大值，单位为Mbps\(Mega bit per second\)。|
|SystemDisk.Category|String|系统盘的磁盘种类。|
|DataDisks|DataDiskSetType|数据盘信息的集合。|
|LifecycleState|String|伸缩配置在伸缩组中生效状态。|
|CreationTime|String|伸缩配置的创建时间。|

DataDiskSetType是由DataDiskItemType类型组成的集合。

|名称|类型|描述|
|:-|:-|:-|
|DataDisk|DataDiskItemType|数据盘信息。|

DataDiskItemType类型的属性如下表所示。

|名称|类型|描述|
|:-|:-|:-|
|Size|Integer|磁盘大小。|
|Category|String|磁盘种类。|
|SnapshotId|String|创建数据盘使用的快照ID。|
|Device|String|数据盘挂载点。|

## 示例 {#section_mnz_tgk_sfb .section}

请求示例

```
http://ess.aliyuncs.com/?Action=CreateScalingConfiguration
&RegionId=cn-qingdao
&PageSize=50
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
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
            <InternetChargeType>PayByBandwidth</InternetChargeType>
            <InternetMaxBandwidthIn>200</InternetMaxBandwidthIn>
            <InternetMaxBandwidthOut>0</InternetMaxBandwidthOut>
            <LifecycleState>Active</LifecycleState>
            <ScalingConfigurationId>bU5uZHcAgtzwcL4IeDeavqTS</ScalingConfigurationId>
            <ScalingConfigurationName>c1908dd1-690f-4c9b-ab73-350f1f06e84f</ScalingConfigurationName>
            <ScalingGroupId>dE9YbOdCHqaFdFZHXVdDjQCB</ScalingGroupId>
            <SecurityGroupId>sg-280ih3w4b</SecurityGroupId>
            <SystemDiskCategory>cloud</SystemDiskCategory>
            <DataDisks>
            <DataDisk>
                <Size>200</Size>
                <Category>cloud</Category>
                <SnapshotId>s-280s7ngih</SnapshotId>
                <Device>/dev/xvdb</Device>
            </DataDisk>
            </DataDisks>
        </ScalingConfiguration>
    </ScalingConfigurations>
</DescribeScalingConfigurationsResponse>
```

`JSON` 格式

```
{
    "RequestId": "67E4324F-CE14-4C2C-9D60-5422641DB76F",
    "TotalCount": 1,
    "PageNumber": 1,
    "PageSize": 1,
    "ScalingConfigurations": {
    "ScalingConfiguration": [
      {
        "ScalingConfigurationId": "eqkz17cfW3clcPExOtLNVlD",
        "SecurityGroupId": "sg-28oewzxvg",
        "CreationTime": "2014-08-18T21:07Z",
        "SystemDiskCategory": "cloud",
        "InternetMaxBandwidthIn": 200,
        "InternetMaxBandwidthOut": 0,
        "LifecycleState": "Inactive",
        "InternetChargeType": "PayByBandwidth",
        "ImageId": "rhel5u7_64_20G_aliaegis_20131231.vhd",
        "InstanceType": "ecs.s2.small",
        "ScalingConfigurationName": "LxVdcOqPBV",
        "ScalingGroupId": "dRsEAGdvbjR5c4SVc2bqLubj",
        “DataDisks”:{
              “DataDisk”:[{
                “Size”:200,
                “Category”: cloud,
                “SnapshotId”: s-280s7ngih,
                “Device”:” /dev/xvdb”
               }]
         }
      }
    ]
  }
}
```

## 错误码 {#section_g4g_xgk_sfb .section}

对于所有接口的通用性错误，请参考 [客户端错误](intl.zh-CN/API参考/错误代码/客户端错误.md#) 或 [服务器端错误](intl.zh-CN/API参考/错误代码/服务器端错误.md#)。

