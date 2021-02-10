# DescribeScalingInstances

调用DescribeScalingInstances查询伸缩组内ECS实例的列表，并列出ECS实例的信息。

## 接口说明

您可以通过指定伸缩组ID查询该伸缩组内ECS实例的列表，查询时可以指定伸缩配置ID、健康状态、生命周期状态、创建类型进行过滤。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DescribeScalingInstances&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeScalingInstances|系统规定参数。取值：DescribeScalingInstances |
|RegionId|String|是|cn-hangzhou|伸缩组所属地域的ID。 |
|ScalingGroupId|String|否|asg-bp1igpak5ft1flyp\*\*\*\*|伸缩组的ID。 |
|ScalingConfigurationId|String|否|asc-bp1i65jd06v04vdh\*\*\*\*|关联伸缩配置的ID。 |
|HealthStatus|String|否|Healthy|ECS实例在伸缩组中的健康状态，未处于运行中（Running）状态的ECS实例会被判定为不健康的ECS实例，取值范围：

 -   Healthy：健康的ECS实例。
-   Unhealthy：不健康的ECS实例。

 弹性伸缩会自动移出伸缩组中不健康的ECS实例，并释放自动创建的ECS实例。

 是否释放手动添加的ECS实例由其托管状态决定。如果实例生命周期未托管给伸缩组，只移出实例但不释放。如果实例生命周期托管给伸缩组，移出并释放实例。

 **说明：** 请确保账号可用额度充足。如果账号欠费，所有后付费的ECS实例（包括按量付费实例和抢占式实例）都会停机，甚至被释放。欠费后伸缩组内ECS实例状态变化，请参见[欠费说明](~~170589~~)。 |
|LifecycleState|String|否|InService|ECS实例在伸缩组中的生命周期状态，取值范围：

 -   InService：已成功加入伸缩组并正常提供服务。
-   Pending：加入中。ECS实例加入伸缩组时包括加入负载均衡实例的后端服务器、RDS实例的访问白名单等过程。
-   Pending:Wait：加入挂起中。如果伸缩组内创建了适用于弹性扩张活动的生命周期挂钩，ECS实例在加入伸缩组时被挂起并等待挂钩超时时间结束。
-   Protected：保护中。ECS实例正常提供服务，但弹性伸缩不管理ECS实例的生命周期，而是由您手动管理。
-   Standby：备用中。ECS实例不提供服务，负载均衡权重被置为零，且弹性伸缩不管理ECS实例的生命周期，而是由您手动管理。
-   Stopped：停用中。ECS实例已停机，不提供服务。
-   Removing：移出中。ECS实例移出伸缩组时包括移出负载均衡实例的后端服务器、RDS实例的访问白名单等过程。
-   Removing:Wait：移出挂起中。如果伸缩组内创建了适用于弹性收缩活动的生命周期挂钩，ECS实例在移出伸缩组时被挂起并等待挂钩超时时间结束。 |
|CreationType|String|否|AutoCreated|ECS实例的创建方式，取值范围：

 -   AutoCreated：弹性伸缩根据实例配置信息来源自动创建的ECS实例。
-   Attached：不是通过弹性伸缩服务创建，而是由您手动添加到伸缩组中的ECS实例。 |
|PageNumber|Integer|否|1|ECS实例列表的页码，起始值：1。

 默认值：1 |
|PageSize|Integer|否|10|分页查询时设置的每页行数，最大值：50。

 默认值：10 |
|InstanceId.N|RepeatList|否|i-bp109k5j3dum1ce6\*\*\*\*|InstanceId.N为ECS实例的ID，N的取值范围：1～20。返回查询结果时忽略失效的InstanceId，并且不报错。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|当前页码。 |
|PageSize|Integer|10|每页行数。 |
|RequestId|String|B13527BF-1FBD-4334-A512-20F5E9D3FB4D|请求ID。 |
|ScalingInstances|Array of ScalingInstance| |ECS实例信息组成的集合。 |
|ScalingInstance| | | |
|CreatedTime|String|2020-05-18T03:11:39Z|ECS实例加入伸缩组的时间，精确到秒。 |
|CreationTime|String|2020-05-18T03:11Z|ECS实例加入伸缩组的时间，精确到分钟。 |
|CreationType|String|AutoCreated|ECS实例的创建方式，取值范围：

 -   AutoCreated：弹性伸缩根据实例配置信息来源自动创建的ECS实例。
-   Attached：不是通过弹性伸缩服务创建，而是由您手动添加到伸缩组中的ECS实例。 |
|Entrusted|Boolean|true|手动添加实例到伸缩组时，是否将实例托管给伸缩组，托管状态的手动添加实例，在移除伸缩组（不包括手动移除）时，将执行释放操作。取值范围：

 -   true：将实例托管给伸缩组。
-   false：不将实例托管给伸缩组。 |
|HealthStatus|String|Healthy|ECS实例在伸缩组中的健康状态，未处于运行中（Running）状态的ECS实例会被判定为不健康的ECS实例，取值范围：

 -   Healthy：健康的ECS实例。
-   Unhealthy：不健康的ECS实例。

 弹性伸缩会自动移出伸缩组中不健康的ECS实例，并释放自动创建的ECS实例。

 是否释放手动添加的ECS实例由其托管状态决定。如果实例生命周期未托管给伸缩组，只移出实例但不释放。如果实例生命周期托管给伸缩组，移出并释放实例。

 **说明：** 请确保账号可用额度充足。如果账号欠费，所有后付费的ECS实例（包括按量付费实例和抢占式实例）都会停机，甚至被释放。欠费后伸缩组内ECS实例状态变化，请参见[欠费说明](~~170589~~)。 |
|InstanceId|String|i-bp109k5j3dum1ce6\*\*\*\*|ECS实例的ID。 |
|LaunchTemplateId|String|lt-m5e3ofjr1zn1aw7\*\*\*\*|实例启动模板的ID。 |
|LaunchTemplateVersion|String|1|实例启动模板的版本。 |
|LifecycleState|String|InService|ECS实例在伸缩组中的生命周期状态，取值范围：

 -   InService：已成功加入伸缩组并正常提供服务。
-   Pending：加入中。ECS实例加入伸缩组时包括加入负载均衡实例的后端服务器、RDS实例的访问白名单等过程。
-   Pending:Wait：加入挂起中。如果伸缩组内创建了适用于弹性扩张活动的生命周期挂钩，ECS实例在加入伸缩组时被挂起并等待挂钩超时时间结束。
-   Protected：保护中。ECS实例正常提供服务，但弹性伸缩不管理ECS实例的生命周期，而是由您手动管理。
-   Standby：备用中。ECS实例不提供服务，负载均衡权重被置为零，且弹性伸缩不管理ECS实例的生命周期，而是由您手动管理。
-   Stopped：停用中。ECS实例已停机，不提供服务。
-   Removing：移出中。ECS实例移出伸缩组时包括移出负载均衡实例的后端服务器、RDS实例的访问白名单等过程。
-   Removing:Wait：移出挂起中。如果伸缩组内创建了适用于弹性收缩活动的生命周期挂钩，ECS实例在移出伸缩组时被挂起并等待挂钩超时时间结束。 |
|LoadBalancerWeight|Integer|50|负载均衡实例权重。 |
|ScalingConfigurationId|String|asc-bp1i65jd06v04vdh\*\*\*\*|关联伸缩配置的ID。 |
|ScalingGroupId|String|asg-bp1igpak5ft1flyp\*\*\*\*|所属伸缩组的ID。 |
|SpotStrategy|String|SpotWithPriceLimit|抢占式实例的抢占策略。取值范围：

 -   SpotWithPriceLimit：设置上限价格的抢占式实例。
-   SpotAsPriceGo：系统自动出价，跟随当前市场实际价格。 |
|WarmupState|String|NoNeedWarmup|实例的预热状态，取值范围：

 -   NoNeedWarmup：不需要预热。
-   WaitingForInstanceWarmup：等待预热结束。
-   InstanceWarmupFinish：预热结束。 |
|WeightedCapacity|Integer|4|实例规格的权重，即实例规格的单台实例在伸缩组中表示的容量大小。权重越大，满足期望容量所需的本实例规格的实例数量越少。 |
|TotalCount|Integer|1|ECS实例的总数。 |
|TotalSpotCount|Integer|4|当前伸缩组中，运行状态的抢占式实例总数。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=DescribeScalingInstances
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeScalingInstancesResponse>
      <TotalCount>1</TotalCount>
      <PageSize>10</PageSize>
      <RequestId>D66AC79E-8299-4E0B-B681-3063C88E215B</RequestId>
      <PageNumber>1</PageNumber>
      <ScalingInstances>
            <ScalingInstance>
                  <LoadBalancerWeight>50</LoadBalancerWeight>
                  <CreatedTime>2020-12-21T03:11:00Z</CreatedTime>
                  <WarmupState>NoNeedWarmup</WarmupState>
                  <InstanceId>i-m5e3z5l951fibnd9****</InstanceId>
                  <ScalingGroupId>asg-m5e8n5qw4atki7f6****</ScalingGroupId>
                  <HealthStatus>Healthy</HealthStatus>
                  <CreationTime>2020-12-21T03:11Z</CreationTime>
                  <LifecycleState>InService</LifecycleState>
                  <Entrusted>true</Entrusted>
                  <ScalingConfigurationId>asc-m5e9vcoen45jspz7****</ScalingConfigurationId>
                  <CreationType>AutoCreated</CreationType>
            </ScalingInstance>
      </ScalingInstances>
      <TotalSpotCount>0</TotalSpotCount>
</DescribeScalingInstancesResponse>
```

`JSON`格式

```
{
 "TotalCount": 1,
 "PageSize": 10,
 "RequestId": "D66AC79E-8299-4E0B-B681-3063C88E215B",
 "PageNumber": 1,
 "ScalingInstances": {
  "ScalingInstance": [
   {
    "LoadBalancerWeight": 50,
    "CreatedTime": "2020-12-21T03:11:00Z",
    "WarmupState": "NoNeedWarmup",
    "InstanceId": "i-m5e3z5l951fibnd9****",
    "ScalingGroupId": "asg-m5e8n5qw4atki7f6****",
    "HealthStatus": "Healthy",
    "CreationTime": "2020-12-21T03:11Z",
    "LifecycleState": "InService",
    "Entrusted": true,
    "ScalingConfigurationId": "asc-m5e9vcoen45jspz7****",
    "CreationType": "AutoCreated"
   }
  ]
 },
 "TotalSpotCount": 0
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ess)查看更多错误码。

