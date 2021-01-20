# DescribeAlarms

调用DescribeAlarms查询报警任务的信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DescribeAlarms&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeAlarms|系统规定参数。取值：DescribeAlarms |
|RegionId|String|是|cn-qingdao|报警任务所属地域的ID。 |
|ScalingGroupId|String|否|asg-bp18p2yfxow2dloq\*\*\*\*|报警任务关联的伸缩组的ID。 |
|AlarmTaskId|String|否|asg-bp1hvbnmkl10vll5\*\*\*\*\_f95ce797-dc2e-4bad-9618-14fee7d1\*\*\*\*|报警任务ID。 |
|State|String|否|OK|报警任务的状态。取值范围：

 -   ALARM：报警，已满足报警条件。
-   OK：正常，尚未满足报警条件。
-   INSUFFICIENT\_DATA：数据不足，不足以判断是否满足了报警条件。 |
|IsEnable|Boolean|否|true|报警任务是否启用。取值范围：

 -   true：已启用。
-   false：已停用。 |
|MetricType|String|否|system|监控项类型。取值范围：

 -   system：使用云监控系统指标。
-   custom：使用上报到云监控的自定义指标。 |
|MetricName|String|否|CpuUtilization|报警任务的名称。 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。最大值：50。

 默认值：10 |
|PageNumber|Integer|否|1|报警任务列表的页码。起始值：1。

 默认值：1 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AlarmList|Array of Alarm| |报警任务的列表。 |
|Alarm| | | |
|AlarmActions|List|ari:acs:ess:cn-hangzhou:1406926474\*\*\*\*:scalingrule/asr-bp163l21e07uh\*\*\*\*|报警任务关联伸缩规则的唯一标识符的列表。 |
|AlarmTaskId|String|asg-bp1hvbnmkl10vll5\*\*\*\*\_f95ce797-dc2e-4bad-9618-14fee7d1\*\*\*\*|报警任务ID。 |
|ComparisonOperator|String|\>=|监控项统计值与阈值的比较符，用于指定监控项统计值与阈值在什么关系下满足条件。取值范围：

 -   监控项统计值大于等于阈值。取值：\>=
-   监控项统计值小于等于阈值。取值：<=
-   监控项统计值大于阈值。取值：\>
-   监控项统计值小于阈值。取值：< |
|Description|String|Test alarm task.|报警任务的描述。 |
|Dimensions|Array of Dimension| |监控项关联的维度信息。 |
|Dimension| | | |
|DimensionKey|String|device|监控项关联的维度信息键，取值范围：

 -   user\_id：您的账号ID。
-   scaling\_group：被监控的伸缩组。
-   device：网卡设备的类型。
-   state：TCP连接的状态。 |
|DimensionValue|String|eth0|监控项关联的维度信息值，取值范围由维度信息键决定。

 user\_id：由系统自动填充。

 scaling\_group：由系统自动填充。

 device取值范围：

 -   eth0：对于经典网络实例，eth0表示内网网卡。对于VPC实例，只存在eth0一张网卡。
-   eth1：对于经典网络实例，eth1代表外网网卡。

 state取值范围：

 -   TCP\_TOTAL：表示总的TCP连接数。
-   ESTABLISHED：表示已建立的TCP连接数。 |
|Effective|String|Test|**说明：** 该参数正在邀测中，暂未开放使用。 |
|Enable|Boolean|true|报警任务是否启用。取值范围：

 -   true：已启用。
-   false：已停用。 |
|EvaluationCount|Integer|3|触发执行伸缩规则需要满足阈值表达式的次数，例如，CPU使用率平均值3次的统计结果均大于等于80%。 |
|MetricName|String|CpuUtilization|监控项名称。取值范围：

 -   CpuUtilization：CPU使用率（%）。
-   ClassicInternetRx：经典网络外网入流量（KB/min）。
-   ClassicInternetTx：经典网络外网出流量（KB/min）。
-   VpcInternetRx：VPC网络外网入流量（KB/min）。
-   VpcInternetTx：VPC网络外网出流量（KB/min）。
-   IntranetRx：内网入流量（KB/min）。
-   IntranetTx：内网出流量（KB/min）。
-   LoadAverage：系统平均负载。
-   MemoryUtilization：内存使用率（%）。
-   SystemDiskReadBps：系统盘读BPS（Byte/s）。
-   SystemDiskWriteBps：系统盘写BPS（Byte/s）。
-   SystemDiskReadOps：系统盘读IOPS（次/s）。
-   SystemDiskWriteOps：系统盘写IOPS（次/s）。
-   PackagesNetIn：网卡收包数（个/s）。
-   PackagesNetOut：网卡发包数（个/s）。
-   TcpConnection：TCP连接数（个）。

 更多信息请参见接口说明。 |
|MetricType|String|system|监控项类型。取值范围：

 -   system：使用云监控系统指标。
-   custom：使用上报到云监控的自定义指标。 |
|Name|String|TestAlarmTask|报警任务的名称。 |
|Period|Integer|300|统计监控项数据的周期，单位为秒。取值范围：

 -   60
-   120
-   300
-   900 |
|ScalingGroupId|String|asg-bp18p2yfxow2dloq\*\*\*\*|报警任务关联的伸缩组的ID。 |
|State|String|ALARM|报警任务的状态。取值范围：

 -   ALARM：报警，已满足报警条件。
-   OK：正常，尚未满足报警条件。
-   INSUFFICIENT\_DATA：数据不足，不足以判断是否满足了报警条件。 |
|Statistics|String|Average|统计监控项数据的方法。取值范围：

 -   Average：平均值。
-   Minimum：最小值。
-   Maximum：最大值。 |
|Threshold|Float|80|监控指标的阈值，满足阈值表达式达到指定次数即触发执行伸缩规则。 |
|PageNumber|Integer|1|当前页码。 |
|PageSize|Integer|10|每页行数。 |
|RequestId|String|871C7C53-34A4-45AA-8C14-4B72FA6A\*\*\*\*|请求ID。 |
|TotalCount|Integer|2|报警任务的总数。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=DescribeAlarms
&RegionId=cn-qingdao
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeAlarmsResponse>
  <PageNumber>1</PageNumber>
  <TotalCount>2</TotalCount>
  <PageSize>10</PageSize>
  <AlarmList>
    <Alarm>
      <Period>300</Period>
      <Statistics>Average</Statistics>
      <MetricType>system</MetricType>
      <EvaluationCount>3</EvaluationCount>
      <Name>asg-bp1hvbnmkl10vll5xtt2_f95ce797-dc2e-4bad-9618-14fee7d1****</Name>
      <AlarmTaskId>asg-bp1hvbnmkl10vll5xtt2_f95ce797-dc2e-4bad-9618-14fee7d1****</AlarmTaskId>
      <MetricName>MemoryUtilization</MetricName>
      <Threshold>55</Threshold>
      <State>INSUFFICIENT_DATA</State>
      <Enable>false</Enable>
      <ScalingGroupId>asg-bp1hvbnmkl10vll5****</ScalingGroupId>
      <Dimensions>
        <Dimension>
          <DimensionValue>asg-bp1hvbnmkl10vll5****</DimensionValue>
          <DimensionKey>scaling_group</DimensionKey>
        </Dimension>
        <Dimension>
          <DimensionValue>140692647406****</DimensionValue>
          <DimensionKey>userId</DimensionKey>
        </Dimension>
      </Dimensions>
      <ComparisonOperator>>=</ComparisonOperator>
    </Alarm>
    <Alarm>
      <Period>60</Period>
      <Description>DO NOT EDIT OR DELETE.For TargetTrackingScalingRule scalingRuleAri:ari:acs:ess:cn-hangzhou:140692647406****:scalingrule/asr-bp13jvr9iummzvgk****, scalingRuleName:****-target-tracking-scaling-rule</Description>
      <Statistics>Average</Statistics>
      <MetricType>system</MetricType>
      <EvaluationCount>15</EvaluationCount>
      <AlarmActions>
        <AlarmAction>ari:acs:ess:cn-hangzhou:140692647406****:scalingrule/asr-bp13jvr9iummzvgk****</AlarmAction>
      </AlarmActions>
      <Name>TargetTracking-asr-bp13jvr9iummzvgk****-AlarmLow-3f4730b9-c275-4527-b057-847fa883****</Name>
      <AlarmTaskId>asg-bp18p2yfxow2dloq****_48efb36a-c0b8-4173-b699-bd37c430****</AlarmTaskId>
      <MetricName>CpuUtilization</MetricName>
      <Threshold>56</Threshold>
      <State>ALARM</State>
      <Enable>true</Enable>
      <ScalingGroupId>asg-bp18p2yfxow2dloq****</ScalingGroupId>
      <Dimensions>
        <Dimension>
          <DimensionValue>asg-bp18p2yfxow2dloq****</DimensionValue>
          <DimensionKey>scaling_group</DimensionKey>
        </Dimension>
        <Dimension>
          <DimensionValue>140692647406****</DimensionValue>
          <DimensionKey>userId</DimensionKey>
        </Dimension>
      </Dimensions>
      <ComparisonOperator><</ComparisonOperator>
    </Alarm>
  </AlarmList>
  <RequestId>871C7C53-34A4-45AA-8C14-4B72FA6A****</RequestId>
</DescribeAlarmsResponse>
```

`JSON`格式

```
{
	"PageNumber": 1,
	"TotalCount": 2,
	"PageSize": 10,
	"AlarmList": {
		"Alarm": [
			{
				"Period": 300,
				"Statistics": "Average",
				"MetricType": "system",
				"EvaluationCount": 3,
				"Name": "asg-bp1hvbnmkl10vll5xtt2_f95ce797-dc2e-4bad-9618-14fee7d1****",
				"AlarmTaskId": "asg-bp1hvbnmkl10vll5xtt2_f95ce797-dc2e-4bad-9618-14fee7d1****",
				"MetricName": "MemoryUtilization",
				"Threshold": 55,
				"State": "INSUFFICIENT_DATA",
				"Enable": false,
				"ScalingGroupId": "asg-bp1hvbnmkl10vll5****",
				"Dimensions": {
					"Dimension": [
						{
							"DimensionValue": "asg-bp1hvbnmkl10vll5****",
							"DimensionKey": "scaling_group"
						},
						{
							"DimensionValue": "140692647406****",
							"DimensionKey": "userId"
						}
					]
				},
				"ComparisonOperator": ">="
			},
			{
				"Period": 60,
				"Description": "DO NOT EDIT OR DELETE.For TargetTrackingScalingRule scalingRuleAri:ari:acs:ess:cn-hangzhou:140692647406****:scalingrule/asr-bp13jvr9iummzvgk****, scalingRuleName:****-target-tracking-scaling-rule",
				"Statistics": "Average",
				"MetricType": "system",
				"EvaluationCount": 15,
				"AlarmActions": {
					"AlarmAction": [
						"ari:acs:ess:cn-hangzhou:140692647406****:scalingrule/asr-bp13jvr9iummzvgk****"
					]
				},
				"Name": "TargetTracking-asr-bp13jvr9iummzvgk****-AlarmLow-3f4730b9-c275-4527-b057-847fa883****",
				"AlarmTaskId": "asg-bp18p2yfxow2dloq****_48efb36a-c0b8-4173-b699-bd37c430****",
				"MetricName": "CpuUtilization",
				"Threshold": 56,
				"State": "ALARM",
				"Enable": true,
				"ScalingGroupId": "asg-bp18p2yfxow2dloq****",
				"Dimensions": {
					"Dimension": [
						{
							"DimensionValue": "asg-bp18p2yfxow2dloq****",
							"DimensionKey": "scaling_group"
						},
						{
							"DimensionValue": "140692647406****",
							"DimensionKey": "userId"
						}
					]
				},
				"ComparisonOperator": "<"
			}
		]
	},
	"RequestId": "871C7C53-34A4-45AA-8C14-4B72FA6A****"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

