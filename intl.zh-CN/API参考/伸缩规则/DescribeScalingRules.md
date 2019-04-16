# DescribeScalingRules {#concept_25950_zh .concept}

查询伸缩组下的伸缩规则，并列出伸缩规则的属性。

## 描述 {#section_td2_zjk_sfb .section}

您可以通过指定伸缩组ID来查询该伸缩组下的所有伸缩规则，查询时可以输入伸缩规则ID、伸缩规则名称、伸缩规则唯一标识符、伸缩规则类型进行过滤。

## 请求参数 {#section_ilw_zjk_sfb .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：DescribeScalingRules。|
|RegionId|String|是|伸缩规则所属伸缩组的地域ID。|
|ScalingGroupId|String|否|伸缩组的ID。|
|ScalingRuleId.N|String|否|伸缩规则的ID，最多可以输入10个。查询结果会忽略失效的伸缩规则ID，并且不报错。|
|ScalingRuleName.N|String|否|伸缩规则的名称，最多可以输入10个。查询结果会忽略失效的伸缩规则名称，并且不报错。|
|ScalingRuleAri.N|String|否|伸缩规则的唯一标识符，最多可以输入10个。查询结果会忽略失效的伸缩规则唯一标识符，并且不报错。|
|ScalingRuleType|String|否|伸缩规则类型。可选值：-   SimpleScalingRule：简单伸缩规则。根据调整方式（AdjustmentType）和调整值（AdjustmentValue）调整ECS实例数量。
-   TargetTrackingScalingRule：目标追踪伸缩规则。根据预定义监控（MetricName）项动态计算需要扩缩容的ECS实例数量，尽量将预定义监控项的指标值维持在目标值（TargetValue）附近。

。|
|PageNumber|Integer|否|伸缩规则列表的页码，起始值为1，默认值为1。|
|PageSize|Integer|否|分页查询时设置的每页行数，最大值50，默认值为10。|
|ShowAlarmRules|Boolean|否|是否返回伸缩规则关联的云监控报警任务。默认值：false。|

## 返回参数 {#section_pbs_bkk_sfb .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|伸缩规则总数。|
|PageNumber|Integer|当前页码。|
|PageSize|Integer|每页行数。|
|ScalingRules|ScalingRuleSetType|伸缩规则信息组成的集合。|

ScalingRuleSetType是由ScalingRuleItemType类型组成的集合。

|名称|类型|描述|
|:-|:-|:-|
|ScalingRule|ScalingRuleItemType|伸缩规则信息。|

ScalingRuleItemType类型的属性如下表所示。

|名称|类型|描述|
|:-|:-|:-|
|ScalingRuleId|String|伸缩规则的ID。|
|ScalingGroupId|String|伸缩组的ID。|
|ScalingRuleName|String|伸缩规则的名称。|
|Cooldown|Integer|冷却时间。|
|AdjustmentType|String|调整方式。|
|AdjustmentValue|Integer|调整值。|
|ScalingRuleAri|String|伸缩规则的唯一标识符。|
|ScalingRuleType|String|伸缩规则的类型。|
|Alarms|Alarm|伸缩规则关联的云监控报警任务。仅在ShowAlarmRules参数为true时返回伸缩规则关联的云监控报警任务，否则返回空列表。|

Alarm类型的属性如下表所示。

|名称|类型|描述|
|:-|:-|:-|
|AlarmTaskId|String|云监控报警规则的ID 。|
|AlarmTaskName|String|云监控报警规则的名称 。|

## 示例 {#section_as4_3kk_sfb .section}

请求示例

```
http://ess.aliyuncs.com/?Action=DescribeScalingRules
&RegionId=cn-qingdao
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&PageSize=50
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeScalingRulesResponse>
    <PageNumber>1</PageNumber>
    <PageSize>50</PageSize>
    <ScalingRules>
        <ScalingRule>
            <AdjustmentType>QuantityChangeInCapacity</AdjustmentType>
            <AdjustmentValue>1</AdjustmentValue>
            <Cooldown>20</Cooldown>
            <ScalingGroupId>AG6CQdPU8OKdwLjgZcJ2eaQ</ScalingGroupId>
            <ScalingRuleAri>ari:acs:ess:cn-qingdao:1344371:scalingRule/eMKWG8SRNb9dBLAjweNI1Ik</ScalingRuleAri>
            <ScalingRuleId>eMKWG8SRNb9dBLAjweNI1Ik</ScalingRuleId>                                                
            <ScalingRuleName>eMKWG8SRNb9dBLAjweNI1Ik</ScalingRuleName>
        </ScalingRule>
    </ScalingRules>
    <TotalCount>1</TotalCount>
    <RequestId>3306A40D-3412-4101-9F19-5F81E3055DAD</RequestId>
</DescribeScalingRulesResponse>
```

`JSON` 格式

```
{
  "RequestId": "B583BFEF-A779-427A-9B74-262DDD249702",
  "TotalCount": 1,
  "PageNumber": 1,
  "PageSize": 10,
  "ScalingRules": {
    "ScalingRule": [
      {
        "ScalingRuleId": "efcqrZdjlookc0UkE3dA5I0a",
        "ScalingRuleAri": "ari:acs:ess:cn-qingdao:1344371:scalingRule/efcqrZdjlookc0UkE3dA5I0a",
        "Cooldown": 500,
        "ScalingGroupId": "ccMvs9dcZlE5c9CtrwbXzizr",
        "AdjustmentType": "TotalCapacity",
        "ScalingRuleName": "KFJoxGKXXt",
        "AdjustmentValue": 5
      }
    ]
  }
}
```

## 错误码 {#section_ldw_hkk_sfb .section}

对于所有接口的通用性错误，请参考 [客户端错误](intl.zh-CN/API参考/错误代码/客户端错误.md#) 或 [服务器端错误](intl.zh-CN/API参考/错误代码/服务器端错误.md#)。

