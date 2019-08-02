# DescribeScalingRules {#doc_api_Ess_DescribeScalingRules .reference}

调用DescribeScalingRules查询伸缩组下的伸缩规则，并列出伸缩规则的信息。

## 接口说明 {#description .section}

您可以通过指定伸缩组ID来查询该伸缩组下的所有伸缩规则，查询时可以输入伸缩规则ID、伸缩规则名称、伸缩规则唯一标识符、伸缩规则类型进行过滤。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DescribeScalingRules&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-qingdao|伸缩规则所属伸缩组的地域ID。

 |
|Action|String|否|DescribeScalingRules|系统规定参数，取值：DescribeScalingRules。

 |
|PageNumber|Integer|否|1|伸缩规则列表的页码，起始值：1。

 默认值：1。

 |
|PageSize|Integer|否|50|分页查询时设置的每页行数，最大值：50。

 默认值：10。

 |
|ScalingGroupId|String|否|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组的ID。

 |
|ScalingRuleAri.1|String|否|ari:acs:ess:cn-qingdao:1344371:scalingRule/eMKWG8SRNb9dBLAjweNI1Ik|ScalingRuleAri.N为待查询伸缩规则的唯一标识符，N的取值范围：1～10。

 |
|ScalingRuleId.1|String|否|eMKWG8SRNb9dBLAjweN\*\*\*\*|ScalingRuleId.N为待查询伸缩规则的ID，N的取值范围：1～10。

 |
|ScalingRuleName.1|String|否|eMKWG8SRNb9dBLAjweN\*\*\*\*|ScalingRuleName.N为待查询伸缩规则的名称，N的取值范围：1～10。

 |
|ScalingRuleType|String|否|SimpleScalingRule|伸缩规则的类型，取值范围：

 -   SimpleScalingRule：简单伸缩规则。根据调整方式（AdjustmentType）和调整值（AdjustmentValue）调整ECS实例数量。
-   TargetTrackingScalingRule：目标追踪伸缩规则。根据预定义监控（MetricName）项动态计算需要扩缩容的ECS实例数量，尽量将预定义监控项的指标值维持在目标值（TargetValue）附近。
-   StepScalingRule： 步进伸缩规则，根据阈值和指标值提供分步扩展方式。
-   PredictiveScalingRule：预测伸缩规则，基于机器学习能力分析伸缩组的历史监控数据预测未来监控指标值，并支持自动创建定时任务设置伸缩组边界。

 默认值：SimpleScalingRule。

 |
|ShowAlarmRules|Boolean|否|false|是否返回伸缩规则关联的云监控报警任务，取值范围：

 -   true：返回伸缩规则关联的云监控报警任务。
-   false：不返回伸缩规则关联的云监控报警任务。

 默认值：false。

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
|ScalingRules| | |伸缩规则信息组成的集合。

 |
|AdjustmentType|String|QuantityChangeInCapacity|伸缩规则的调整方式，取值范围：

 -   QuantityChangeInCapacity：增加或减少指定数量的ECS实例。
-   PercentChangeInCapacity：增加或减少指定比例的ECS实例。
-   TotalCapacity： 将当前伸缩组的ECS实例数量调整到指定数量。

 |
|AdjustmentValue|Integer|1|伸缩规则的调整值。

 |
|Alarms| | |伸缩规则关联的云监控报警任务。仅在ShowAlarmRules参数为true时返回伸缩规则关联的云监控报警任务，否则返回空列表。

 |
|AlarmTaskId|String|asg-bp18p2yfxow2dloq\*\*\*\*\_1f9458d1-70e1-4bee-8c7f-7a47695b\*\*\*\*|伸缩规则关联的报警任务的ID。

 |
|AlarmTaskName|String|event-notified\*\*\*\*|伸缩规则关联的报警任务的名称。

 |
|ComparisonOperator|String|\>=|伸缩规则关联的报警任务使用的监控项统计值与阈值比较符，取值范围：

 -   <=：统计值小于等于阈值。
-   <：统计值小于阈值。
-   \>：统计值大于阈值。
-   \>=：统计值大于等于阈值。

 |
|Dimensions| | |伸缩规则关联的报警任务的维度信息。

 |
|DimensionKey|String|scaling\_group|监控项关联的维度信息键值，取值范围：

 -   scaling\_group：伸缩组ID。
-   userId：用户账号ID。

 |
|DimensionValue|String|asg-bp18p2yfxow2dloq\*\*\*\*|监控项关联的维度信息属性值。

 |
|EvaluationCount|Integer|3|伸缩规则关联的报警任务到达报警状态需要连续满足阈值表达式的次数。

 |
|MetricName|String|CpuUtilization|伸缩规则关联的报警任务监控项名称。

 |
|Statistics|String|Average|伸缩规则关联的报警任务的统计方式，取值范围：

 -   Average：统计平均值。
-   Maximum：统计最大值。
-   Minimum：统计最小值。

 |
|Threshold|Float|50|伸缩规则关联的报警任务的报警阈值。

 |
|Cooldown|Integer|20|伸缩规则的冷却时间，仅适用于简单伸缩规则。 取值范围：0~86400，单位：秒。

 |
|DisableScaleIn|Boolean|true|是否禁用缩容，仅适用于目标追踪伸缩规则，取值范围：

 -   true：禁用缩容。
-   false：允许缩容。

 |
|EstimatedInstanceWarmup|Integer|300|实例预热时间。

 |
|InitialMaxSize|Integer|100|伸缩组实例数的上限，和PredictiveValueBehavior结合使用。

 |
|MaxSize|Integer|2|伸缩组最大实例数。

 |
|MetricName|String|CpuUtilization|预定义监控项，适用于目标追踪伸缩规则和预测规则。

 目标追踪伸缩规则取值范围：

 -   CpuUtilization：平均CPU使用率
-   ClassicInternetRx：经典网络公网入流量平均值
-   ClassicInternetTx：经典网络公网出流量平均值
-   VpcInternetRx：VPC网络公网入流量平均值
-   VpcInternetTx：VPC网络公网出流量平均值
-   IntranetRx：内网入流量平均值
-   IntranetTx ：内网出流量平均值

 预测规则取值范围：

 -   CpuUtilization：平均CPU使用率
-   IntranetRx：内网入流量平均值
-   IntranetTx ：内网出流量平均值

 |
|MinAdjustmentMagnitude|Integer|1|伸缩规则最小调整实例数，仅当伸缩规则类型为SimpleScalingRule或StepScalingRule，且AdjustmentType为PercentChangeInCapacity时生效。

 |
|MinSize|Integer|1|伸缩组最小实例数。

 |
|PredictiveScalingMode|String|PredictAndScale|预测规则的模式，取值范围：

 -   PredictAndScale：产生预测结果并创建预测任务。
-   PredictOnly：产生预测结果，但不会创建预测任务。

 |
|PredictiveTaskBufferTime|Integer|30|预测规则自动创建的预测任务默认均在整点执行，您可以设置预启动时间提前执行预测任务，预先准备资源。取值范围：0~60，单位：分钟。

 |
|PredictiveValueBehavior|String|MaxOverridePredictiveValue|预测规则最大值处理方式，取值范围：

 -   MaxOverridePredictiveValue：初始最大值会覆盖预测值。预测值大于初始最大值时，预测任务的最大值采用初始最大值。
-   PredictiveValueOverrideMax：预测值会覆盖初始最大值。预测值大于初始最大值时， 预测任务的最大值采用预测值。
-   PredictiveValueOverrideMaxWithBuffer：预测值会附加一定比例。预测值会按照PredictiveValueBuffer比例增加，当增加后的值大于初始最大值时，会采用增加后的值。

 |
|PredictiveValueBuffer|Integer|50|PredictiveValueBehavior为PredictiveValueOverrideMaxWithBuffer时生效，预测值会按照该比例增加，当增加后的值大于初始最大值时，会采用增加后的值。取值范围：0~100。

 |
|ScalingGroupId|String|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组的ID。

 |
|ScalingRuleAri|String|ari:acs:ess:cn-qingdao:1344371:scalingRule/eMKWG8SRNb9dBLAjweNI1Ik|伸缩规则的唯一标识符。

 |
|ScalingRuleId|String|eMKWG8SRNb9dBLAjweN\*\*\*\*|伸缩规则的ID。

 |
|ScalingRuleName|String|eMKWG8SRNb9dBLAjweN\*\*\*\*|伸缩规则的名称。

 |
|ScalingRuleType|String|SimpleScalingRule|伸缩规则类型，取值范围：

 -   SimpleScalingRule：简单伸缩规则。根据调整方式（AdjustmentType）和调整值（AdjustmentValue）调整ECS实例数量。
-   TargetTrackingScalingRule：目标追踪伸缩规则。根据预定义监控（MetricName）项动态计算需要扩缩容的ECS实例数量，尽量将预定义监控项的指标值维持在目标值（TargetValue）附近。
-   StepScalingRule： 步进伸缩规则，根据阈值和指标值提供分步扩展方式。
-   PredictiveScalingRule：预测伸缩规则，基于机器学习能力分析伸缩组的历史监控数据预测未来监控指标值，并支持自动创建定时任务设置伸缩组边界。

 |
|StepAdjustments| | |步进伸缩规则的分步步骤。

 |
|MetricIntervalLowerBound|Float|1.0|分步步骤的下边界，取值范围：-9.999999E18~9.999999E18。

 |
|MetricIntervalUpperBound|Float|5.0|分步步骤的上边界，取值范围：-9.999999E18~9.999999E18。

 |
|ScalingAdjustment|Integer|1|分步步骤对应的实例扩展数量。

 |
|TargetValue|Float|0.125|目标值。

 |
|TotalCount|Integer|1|伸缩规则总数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DescribeScalingRules
&RegionId=cn-qingdao
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&PageSize=50
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeScalingRulesResponse>
      <PageNumber>1</PageNumber>
      <PageSize>50</PageSize>
      <ScalingRules>
            <ScalingRule>
                  <AdjustmentType>QuantityChangeInCapacity</AdjustmentType>
                  <AdjustmentValue>1</AdjustmentValue>
                  <Cooldown>20</Cooldown>
                  <ScalingGroupId>AG6CQdPU8OKdwLjgZcJ****</ScalingGroupId>
                  <ScalingRuleAri>ari:acs:ess:cn-qingdao:1344371:scalingRule/eMKWG8SRNb9dBLAjweN****</ScalingRuleAri>
                  <ScalingRuleId>eMKWG8SRNb9dBLAjweN****</ScalingRuleId>                                                
                  <ScalingRuleName>eMKWG8SRNb9dBLAjweN****</ScalingRuleName>
            </ScalingRule>
      </ScalingRules>
      <TotalCount>1</TotalCount>
      <RequestId>3306A40D-3412-4101-9F19-5F81E3055DAD</RequestId>
</DescribeScalingRulesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":10,
	"RequestId":"B583BFEF-A779-427A-9B74-262DDD249702",
	"ScalingRules":{
		"ScalingRule":[
			{
				"ScalingRuleAri":"ari:acs:ess:cn-qingdao:1344371:scalingRule/efcqrZdjlookc0UkE3dA****",
				"AdjustmentType":"TotalCapacity",
				"ScalingGroupId":"ccMvs9dcZlE5c9CtrwbX****",
				"AdjustmentValue":5,
				"ScalingRuleName":"KFJoxG****",
				"Cooldown":500,
				"ScalingRuleId":"efcqrZdjlookc0UkE3dA****"
			}
		]
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

