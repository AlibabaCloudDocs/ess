# CreateScalingRule {#concept_25948_zh .concept}

本文介绍创建伸缩规则API操作。

## 描述 {#section_hrj_j3k_sfb .section}

伸缩规则（Scaling Rule）定义了具体的扩张或收缩操作，例如加入或移出N个实例。

如果执行伸缩规则会造成伸缩组的ECS实例数低于MinSize或高于MaxSize，则弹性伸缩会自动调整需要加入或移出的ECS实例数，使得伸缩组的ECS实例数调整到MinSize或MaxSize，但伸缩规则的设定值不会变化。

-   例：某个伸缩组，MaxSize = 3，当前实例数Total Capacity =2，伸缩规则指定“加3台ECS实例”，则在实际执行过程中只会加1台ECS实例，但伸缩规则的设定值仍然3。
-   例：某个伸缩组，MinSize = 2，当前实例数Total Capacity = 3，伸缩规则指定“减去5台ECS实例”，则在实际执行过程中只会减1台ECS实例，但伸缩规则的设定值仍然5。

根据传入参数创建伸缩规则。

-   当AdjustmentType是TotalCapacity时，表示将当前伸缩组的ECS实例数量调整到指定数量，对应的AdjustmentValue值必须大于等于0。
-   当AdjustmentType是QuantityChangeInCapacity或PercentChangeInCapacity，对应的AdjustmentValue值为正数表示增加实例、为负数表示减少实例。
-   当AdjustmentType是PercentChangeInCapacity，弹性伸缩服务以伸缩组当前实例数（Total Capacity） \* AdjusmentValue/100，并使用四舍五入原则来确认增加或减少的ECS实例个数。
-   当伸缩规则指定了冷却时间（Cooldown），则执行该伸缩规则的伸缩活动完成后，会以伸缩规则中指定的冷却时间对伸缩组进行冷却处理，如果伸缩规则未指定冷却时间，则以伸缩组指定的冷却时间（DefaultCooldown）为准。
-   一个伸缩组内最多只能创建50条伸缩规则。
-   返回的伸缩规则唯一标识符（ScalingRuleAri），主要可以被以下接口所使用：
    -   在执行伸缩规则（ExecuteScalingRule）的ScalingRuleAri参数中指定，用户可以手工执行该伸缩规则。
    -   在创建定时任务（CreateScheduledTask）的ScheduledAction参数中指定，用户可以定时执行该伸缩规则。

## 请求参数 {#section_q54_l3k_sfb .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：CreateScalingRule。|
|ScalingGroupId|String|是|伸缩规则所属的伸缩组ID。|
|AdjustmentType|String|是|伸缩规则的调整方式。可选值：-   QuantityChangeInCapacity：增加或减少指定数量的ECS实例。
-   PercentChangeInCapacity：增加或减少指定比例的ECS实例。
-   TotalCapacity： 将当前伸缩组的ECS实例数量调整到指定数量。

|
|AdjustmentValue|Integer|是|伸缩规则的调整值。任何情况下，单次调整的ECS实例台数都不能超过500。不同调整方式对应的取值范围：-   QuantityChangeInCapacity：\[-500, 500\]
-   PercentChangeInCapacity：\[-100, 10000\]
-   TotalCapacity：\[0, 1000\]

|
|ScalingRuleName|String|否|伸缩规则的显示名称，2-40 个英文或中文字符，以数字、大小字母或中文开头，可包含数字，“\_”、“-”或“.”。同一用户账号同一地域同一伸缩组内唯一。如果没有指定该参数，默认值为ScalingRuleId。|
|Cooldown|Integer|否|伸缩规则的冷却时间。取值范围：\[0, 86400\]，单位：秒。默认值为：空。|

## 返回参数 {#section_vjr_t3k_sfb .section}

|名称|类型|描述|
|:-|:-|:-|
|ScalingRuleId|String|伸缩规则的ID，由系统生成，全局唯一。|
|ScalingRuleAri|String|伸缩规则的唯一标识符。|

## 示例 {#section_jyh_v3k_sfb .section}

请求示例

```
http://ess.aliyuncs.com/?Action=CreateScalingRule
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&AdjustmentType=QuantityChangeInCapacity
&AdjustmentValue=-10
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateScalingRuleResponse>   
    <ScalingRuleAri>ari:acs:ess:cn-qingdao:1344371:scalingrule/eMKWG8SRNb9dBLAjweNI1Ik</ScalingRuleAri>
    <ScalingRuleId>eMKWG8SRNb9dBLAjweNI1Ik</ScalingRuleId>
    <RequestId>570C84F4-A434-488A-AFA1-1E3213682B33</RequestId>
</CreateScalingRuleResponse>
```

`JSON` 格式

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368",
    "ScalingRuleId": "eMKWG8SRNb9dBLAjweNI1Ik",
    "ScalingRuleAri":"ari:acs:ess:cn-qingdao:1344371:scalingrule/eMKWG8SRNb9dBLAjweNI1Ik"
}
```

## 错误码 {#section_ltm_y3k_sfb .section}

对于所有接口的通用性错误，请参考[客户端错误](cn.zh-CN/API 参考/错误代码/客户端错误.md#)或[服务器端错误](cn.zh-CN/API 参考/错误代码/服务器端错误.md#)。

|HttpCode|错误码|错误信息|描述|
|--------|:--|:---|:-|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|指定的伸缩组在该用户账号下不存在。|
|400|InvalidScalingRuleName.Duplicate|The specified value of parameter <parameter name\> is duplicated.|伸缩规则名字已存在。|
|400|QuotaExceeded.ScalingRule|Scaling rule quota exceeded in the specified scaling group.|用户的伸缩规则使用个数达到上限。|

