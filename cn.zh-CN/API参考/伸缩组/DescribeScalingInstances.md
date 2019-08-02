# DescribeScalingInstances {#doc_api_Ess_DescribeScalingInstances .reference}

调用DescribeScalingInstances查询伸缩组内ECS实例的列表，并列出ECS实例的信息。

## 接口说明 {#description .section}

您可以通过指定伸缩组ID查询该伸缩组内ECS实例的列表，查询时可以指定伸缩配置ID、健康状态、生命周期状态、创建类型进行过滤。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DescribeScalingInstances&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-qingdao|伸缩组所属地域的ID。

 |
|Action|String|否|DescribeScalingInstances|系统规定参数，取值：DescribeScalingInstances。

 |
|CreationType|String|否|AutoCreated|ECS实例的创建类型，取值范围：

 -   AutoCreated：伸缩组根据伸缩配置和伸缩规则自动创建的ECS实例。
-   Attached：不是通过弹性伸缩服务创建，而是手工添加到伸缩组中的ECS实例。

 |
|HealthStatus|String|否|Healthy|ECS实例在伸缩组中的健康状态，未处于运行中（Running）状态的ECS实例会被判定为不健康的ECS实例，取值范围：

 -   Healthy：健康的ECS实例。
-   Unhealthy：不健康的ECS实例。

 弹性伸缩会自动移出伸缩组中不健康的ECS实例。弹性伸缩会停止和释放自动创建的ECS实例，但不会停止和释放手工添加的ECS实例。

 |
|InstanceId.1|String|否|i-281vv\*\*\*\*|InstanceId.N为ECS实例的ID，N的取值范围：1～20。返回查询结果时忽略失效的InstanceId，并且不报错。

 |
|LifecycleState|String|否|InService|ECS实例在伸缩组中的生命周期状态，取值范围：

 -   InService：已成功加入伸缩组并正常提供服务。
-   Pending：正在加入伸缩组但还未完成相关配置，包括创建实例、加入负载均衡、添加RDS访问名单等过程。
-   Removing：正在移出伸缩组。

 |
|PageNumber|Integer|否|1|ECS实例列表的页码，起始值：1。

 默认值：1。

 |
|PageSize|Integer|否|10|分页查询时设置的每页行数，最大值：50。

 默认值：10。

 |
|ScalingConfigurationId|String|否|asc-\*\*\*\*|关联伸缩配置的ID。

 |
|ScalingGroupId|String|否|asg-\*\*\*\*|伸缩组的ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|当前页码。

 |
|PageSize|Integer|10|每页行数。

 |
|RequestId|String|E481B3F5-F290-4F3E-AB40-F980FB8E098A|请求ID。

 |
|ScalingInstances| | |ECS实例信息组成的集合。

 |
|CreationTime|String|2019-03-06T08:06Z|加入伸缩组的时间。

 |
|CreationType|String|AutoCreated|ECS实例的创建类型，取值范围：

 -   AutoCreated：伸缩组根据伸缩配置和伸缩规则自动创建的ECS实例。
-   Attached：不是通过弹性伸缩服务创建，而是手工添加到伸缩组中的ECS实例。

 |
|HealthStatus|String|Healthy|在伸缩组中的健康状态，取值范围：

 -   Healthy：健康的ECS实例。
-   Unhealthy：不健康的ECS实例。

 |
|InstanceId|String|i-283vv\*\*\*\*|ECS实例的ID。

 |
|LaunchTemplateId|String|lt-m5e3ofjr1zn1aw7\*\*\*\*|实例启动模板的ID。

 |
|LaunchTemplateVersion|String|1|实例启动模板的版本。

 |
|LifecycleState|String|InService|在伸缩组中的生命周期状态，取值范围：

 -   InService：已成功加入伸缩组并正常提供服务。
-   Pending：正在加入伸缩组但还未完成相关配置，包括创建实例、加入负载均衡、添加RDS访问名单等过程。
-   Removing：正在移出伸缩组。

 |
|LoadBalancerWeight|Integer|1|负载均衡实例权重。

 |
|ScalingConfigurationId|String|asg-\*\*\*\*|关联伸缩配置的ID。

 |
|ScalingGroupId|String|asg-\*\*\*\*|所属伸缩组的ID。

 |
|WarmupState|String|NoNeedWarmup|实例的预热状态，取值范围：

 -   NoNeedWarmup：不需要预热
-   WaitingForInstanceWarmup：等待预热结束
-   InstanceWarmupFinish：预热结束

 |
|TotalCount|Integer|1|ECS实例的总数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ess.aliyuncs.com/?Action=DescribeScalingInstances
&RegionId=cn-qingdao
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeScalingInstancesResponse>
      <RequestId>DFF8797F-5B73-4BD7-A7D0-03479C458F7A</RequestId>
  <TotalCount>1</TotalCount>
      <PageNumber>1</PageNumber>
      <PageSize>10</PageSize>
      <ScalingInstances>
            <ScalingInstance>
                  <CreationTime>2014-08-15T17:37Z</CreationTime>
                  <CreationType>AutoCreated</CreationType>
                  <HealthStatus>Healthy</HealthStatus>
                  <InstanceId>i-283vv****</InstanceId>
                  <LifecycleState>InService</LifecycleState>
                  <ScalingConfigurationId>cGsGHrdMBa3DcDrrBVcc****</ScalingConfigurationId>
                  <ScalingGroupId>dBCYxE26IHKcGq1xPcT****</ScalingGroupId>
            </ScalingInstance>
      </ScalingInstances>
</DescribeScalingInstancesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":50,
	"RequestId":"13305F2D-A4C2-4E6B-B7C7-0F2150842EA3",
	"ScalingInstances":{
		"ScalingInstance":[
			{
				"CreationTime":"2014-08-14T10:59Z",
				"ScalingConfigurationId":"bU5uZHcAgtzwcL4IeDe****",
				"CreationType":"AutoCreated",
				"HealthStatus":"Healthy",
				"ScalingGroupId":"dE9YbOdCHqaFdFZHXVdD****",
				"InstanceId":"i-28sov****",
				"LifecycleState":"InService"
			}
		]
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

