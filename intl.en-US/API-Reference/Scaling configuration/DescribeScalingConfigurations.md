# DescribeScalingConfigurations {#concept_25945_zh .concept}

This operation queries scaling configuration information.

## Description {#section_qcc_fgk_sfb .section}

You can query all scaling configurations in a scaling group by specifying the scaling group ID.

Scaling configuration states \(LifecycleState\) can be set to either of the following:

-   Active: Scaling groups use scaling configurations in the active status to automatically create ECS instances.
-   Inactive: The scaling configuration is inactive in a scaling group. The scaling group will not use scaling configurations in inactive state to automatically create ECS instances.

## Request parameters {#section_blm_ggk_sfb .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|Operation interface, required. The parameter value is `DescribeScalingConfigurations`.|
|RegionId|String|Yes|Region ID of the scaling group of a scaling configuration.|
|ScalingGroupId|String|No|Scaling group ID.|
|Scalingconfigurationid. N|String|No|ID of a scaling configuration. A maximum of 10 values can be entered. IDs of active and inactive scaling configurations are displayed in the query result, and can be differentiated by `LifecycleState`.|
|ScalingConfigurationName.N|String|No|Name of a scaling configuration. A maximum of 10 values can be entered. Invalid scaling configuration names are neglected in the query result and no error is reported.|
|PageNumber|Integer|No|Page number of the scaling configuration list. The initial value and default value are both 1.|
|PageSize|Integer|No|When querying by page, this parameter indicates the number of lines per page. Maximum value: 50; default value: 10.|

## Response parameters {#section_dbx_3gk_sfb .section}

|Name|Type|Description|
|:---|:---|:----------|
|TotalCount|Integer|Total number of scaling configurations|
|PageNumber|Integer|Current page number|
|PageSize|Integer|Number of lines per page|
|ScalingConfigurations|ScalingConfigurationSetType|Scaling configuration information set|

ScalingConfigurationSetType is a set of ScalingConfigurationItemTypes.

|Name|Type|Description|
|:---|:---|:----------|
|ScalingConfiguration|ScalingConfigurationItemType|Scaling configuration information|

Attributes of the ScalingConfigurationItemType are listed as follows.

|Name|Type|Description|
|:---|:---|:----------|
|ScalingConfigurationId|String|ID of a scaling configuration|
|ScalingConfigurationName|String|Name shown for a scaling configuration|
|ScalingGroupId|String|ID of the scaling group of a scaling configuration|
|ImageId|String|ID of an image file|
|InstanceType|String|Resource rule of an instance|
|SecurityGroupId|String|ID of a security group|
|InternetChargeType|String|Network billing type|
|InternetMaxBandwidthIn|Integer|Maximum incoming bandwidth from the public network, measured in Mbps \(Mega bit per second\)|
|InternetMaxBandwidthOut|Integer|Maximum outgoing bandwidth from the public network, measured in Mbps \(Mega bit per second\)|
|SystemDisk.Category|String|Category of the system disk|
|DataDisks|DataDiskSetType|Data disk information set|
|LifecycleState|String|Scaling configuration status in a scaling group|
|CreationTime|String|Time when a scaling configuration is created|

DataDiskSetType is a set of DataDiskItemTypes.

|Name|Type|Description|
|:---|:---|:----------|
|DataDisk|DataDiskItemType|Data disk information|

Attributes of the DataDiskItemType are listed as follows.

|Name|Type|Description|
|:---|:---|:----------|
|Size|Integer|Disk capacity|
|Category|String|Disk category|
|SnapshotId|String|ID of the snapshot used for creating the data disk|
|Device|String|Data disk attaching point|

## Request example {#section_mnz_tgk_sfb .section}

```
http://ess.aliyuncs.com/?Action=CreateScalingConfiguration
&RegionId=cn-qingdao
&PageSize=50
&<Public Request Parameters>
```

## Response example { .section}

XML format:

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

JSON format:

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

## Error code {#section_g4g_xgk_sfb .section}

For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

