# ModifyScalingRule {#concept_25949_zh .concept}

本文介绍修改伸缩规则API操作。

## 描述 {#section_xrd_hjk_sfb .section}

修改伸缩规则的属性。

## 请求参数 {#section_xbk_3jk_sfb .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：ModifyScalingRule。|
|ScalingRuleId|String|是|伸缩规则的ID。|
|AdjustmentType|String|否|伸缩规则的调整方式。可选值：-   QuantityChangeInCapacity：增加或减少指定数量的ECS实例。
-   PercentChangeInCapacity： 增加或减少指定比例的ECS实例。
-   TotalCapacity： 将当前伸缩组的ECS实例数量调整到指定数量。

|
|AdjustmentValue|Integer|否|伸缩规则的调整值。任何情况下，单次调整的ECS实例台数都不能超过500。不同调整方式对应的取值范围：-   QuantityChangeInCapacity：\[-500, 500\]
-   PercentChangeInCapacity：\[-100, 10000\]
-   TotalCapacity：\[0, 1000\]

|
|ScalingRuleName|String|否|伸缩规则的显示名称，2-40 个英文或中文字符，以数字、大小字母或中文开头，可包含数字，"\_"、"-"或”.”。同一用户账号同一地域同一伸缩组内唯一。如果没有指定该参数，默认值为ScalingRuleId。

|
|Cooldown|Integer|否|伸缩规则的冷却时间。取值范围：\[0, 86400\]，单位：秒。默认值为：空。|

## 返回参数 {#section_s1t_4jk_sfb .section}

|名称|类型|描述|
|:-|:-|:-|
|ScalingRuleId|String|伸缩规则的ID，由系统生成，全局唯一。|
|ScalingRuleAri|String|伸缩规则的唯一标识符。|

## 示例 {#section_ymk_qjk_sfb .section}

请求示例

```
http://ess.aliyuncs.com/?Action=ModifyScalingRule
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&AdjustmentType=QuantityChangeInCapacity
&AdjustmentValue=-10
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ModifyScalingRuleResponse>
    <ScalingRuleAri>ari:acs:ess:cn-qingdao:1344371:scalingrule/eMKWG8SRNb9dBLAjweNI1Ik</ScalingRuleAri>
    <ScalingRuleId>eMKWG8SRNb9dBLAjweNI1Ik</ScalingRuleId>
    <RequestId>570C84F4-A434-488A-AFA1-1E3213682B33</RequestId>
</ModifyScalingRuleResponse>
```

`JSON` 格式

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368",
    "ScalingRuleId": "eMKWG8SRNb9dBLAjweNI1Ik",
    "ScalingRuleAri":"ari:acs:ess:cn-qingdao:1344371:scalingrule/eMKWG8SRNb9dBLAjweNI1Ik"
}
```

## 错误码 { .section}

对于所有接口的通用性错误，请参考[客户端错误](cn.zh-CN/API 参考/错误代码/客户端错误.md#)或[服务器端错误](cn.zh-CN/API 参考/错误代码/服务器端错误.md#)。

|HttpCode|错误码|错误信息|描述|
|--------|:--|:---|:-|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|指定的伸缩组在该用户账号下不存在。|
|400|InvalidScalingRuleName.Duplicate|The specified value of parameter <parameter name\> is duplicated.|伸缩规则名字已存在。|
|400|QuotaExceeded.ScalingRule|Scaling rule quota exceeded in the specified scaling group.|用户的伸缩规则使用个数达到上限。|

