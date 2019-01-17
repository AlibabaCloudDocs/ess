# DeleteScalingGroup {#concept_25941_zh .concept}

本文介绍删除伸缩组API操作。

## 描述 {#section_u1x_tz2_sfb .section}

删除一个指定的伸缩组。

-   ForceDelete属性表示如果伸缩组存在ECS实例或正在进行伸缩活动，是否强制删除伸缩组并移出和释放ECS实例。
-   如果ForceDelete属性为false，必须满足以下两个条件，才能删除伸缩组：
    -   条件一：伸缩组没有任何伸缩活动正在执行。
    -   条件二：伸缩组当前的ECS实例数量（Total Capacity）为0。
    -   满足以上条件，会先停止伸缩组，然后再删除伸缩组。
-   ForceDelete属性为true时，
    -   先停止伸缩组，拒绝接收新的伸缩活动请求，然后等待已有的伸缩活动完成，最后将伸缩组内所有ECS实例移出伸缩组（用户手工添加的ECS实例会被移出伸缩组，弹性伸缩自动创建的ECS实例会被自动删除）并删除伸缩组。
-   删除伸缩组，包括删除相关联的伸缩配置、伸缩规则、伸缩活动、伸缩请求的信息。
-   删除伸缩组，不会删除以下任务或实例：定时任务、云监控报警任务、负载均衡实例、RDS实例。

## 请求参数 {#section_jrn_11f_sfb .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：DeleteScalingGroup。|
|ScalingGroupId|String|是|伸缩组的ID。|
|ForceDelete|Bool|否|如伸缩组存在ECS实例或正在进行伸缩活动，是否强制删除伸缩组并移出和释放ECS实例。默认值为false，代表不强制删除伸缩组。|

## 返回参数 {#section_et5_g1f_sfb .section}

[公共参数](cn.zh-CN/API 参考/公共参数.md#)。

## 示例 {#section_pvz_51f_sfb .section}

请求示例

```
http://ess.aliyuncs.com/?Action=DeleteScalingGroup
&ScalingGroupId=dmIDKNcyWfzncX9MWX1bwFV
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteScalingGroupResponse>
    <RequestId>6469DCD0-13AC-487E-85A0-CE4922908FDE</RequestId>
</DeleteScalingGroupResponse>
```

`JSON` 格式

```
{
"RequestId": "6469DCD0-13AC-487E-85A0-CE4922908FDE"
}
```

## 错误码 {#section_n4d_n1f_sfb .section}

|HttpCode|错误码|错误信息|描述|
|--------|:--|:---|:-|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|指定的伸缩组在该用户账号下不存在。|
|403|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|用户并未向弹性伸缩完整授权Open API接口。|
|400|InstanceInUse|You cannot delete a scaling configuration or scaling group while there is an instance associated with it.|指定的伸缩组中还有ECS实例。|

