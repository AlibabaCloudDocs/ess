# DisableScalingGroup {#concept_25940_zh .concept}

本文介绍停用伸缩组API操作。

## 描述 {#section_qtb_jy2_sfb .section}

停用一个指定的伸缩组。

-   停用伸缩组之前发生的伸缩活动，会继续完成，而之后触发的伸缩活动会直接拒绝。
-   当伸缩组为Active状态，才可以调用该接口。

## 请求参数 { .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：DisableScalingGroup。|
|ScalingGroupId|String|是|伸缩组的ID。|

## 返回参数 { .section}

[公共参数](cn.zh-CN/API 参考/公共参数.md#)。

## 示例 { .section}

请求示例

```
http://ess.aliyuncs.com/?Action=DisableScalingGroup 
&ScalingGroupId=dmIDKNcyWfzncX9MWX1bwFV
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
< DisableScalingGroupResponse>
    <RequestId>6469DCD0-13AC-487E-85A0-CE4922908FDE</RequestId>
</ DisableScalingGroupResponse>
```

`JSON` 格式

```
{
"RequestId": "6469DCD0-13AC-487E-85A0-CE4922908FDE"
}
```

## 错误码 {#section_ytx_qjb_kgb .section}

关于所有接口的通用性错误，请参考 [客户端错误](cn.zh-CN/API 参考/错误代码/客户端错误.md#) 或 [服务器端错误](cn.zh-CN/API 参考/错误代码/服务器端错误.md#)。

|HttpCode|错误码|错误信息|描述|
|:-------|:--|:---|:-|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|指定的伸缩组在该用户账号下不存在。|

