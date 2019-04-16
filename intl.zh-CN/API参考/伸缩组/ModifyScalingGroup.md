# ModifyScalingGroup {#concept_25937_zh .concept}

修改伸缩组的属性。

## 描述 {#section_ld1_pv2_sfb .section}

-   创建伸缩组的属性中，有以下属性不可修改：
    -   RegionId
    -   LoadBalancerId

        **说明：** 如果需要修改负载均衡实例，请使用[AttachLoadBalancers](intl.zh-CN/API参考/伸缩组/AttachLoadBalancers.md#)和[DetachLoadBalancers](intl.zh-CN/API参考/伸缩组/DetachLoadBalancers.md#)接口。

    -   DBInstanceId

        **说明：** 如果需要修改数据库实例，请使用[AttachDBInstances](intl.zh-CN/API参考/伸缩组/AttachDBInstances.md#)和[DetachDBInstances](intl.zh-CN/API参考/伸缩组/DetachDBInstances.md#)接口。

-   当伸缩组为 active 或 inactive 状态，才可以调用该接口。
-   当伸缩组已被指定伸缩配置，而需要再次修改伸缩配置时，修改的伸缩配置的 instancetype 属性要和当前生效的伸缩配置的 instancetyp 属性一致。

    在伸缩组中加入新的伸缩配置，不会影响通过早前的伸缩配置创建并正在运行的 ECS 实例。

-   当伸缩组的 ECS 实例数（Total Capacity）不满足修改后的 MaxSize 或 MinSize，弹性伸缩服务会自动加入或移出 ECS 实例，使得伸缩组的 ECS 实例数等于 MaxSize 或 MinSize。

## 请求参数 { .section}

|名称|类型|是否必选|描述|
|--|--|----|--|
|Action|String|是|操作接口名，系统规定参数，取值：ModifyScalingGroup。|
|ScalingGroupId|String|是|伸缩组的 ID。|
|ScalingGroupName|String|否|伸缩组的显示名称，2-40 个英文或中文字符，以数字、大小字母或中文开头，可包含数字，“\_”，“-”或“.”。同一用户账号同一地域内唯一。|
|ActiveScalingConfigurationId|String|否|伸缩组内生效的伸缩配置 ID。|
|MinSize|Integer|否|伸缩组内 ECS 实例个数的最小值，取值范围：\[0, 100\] 。|
|MaxSize|Integer|否|伸缩组内 ECS 实例个数的最大值，取值范围：\[0, 100\]。|
|DefaultCooldown|Integer|否|伸缩组默认的冷却时间，取值范围：\[0, 86400\]，单位：秒。|
|RemovalPolicy.N|String|否|ECS 实例移出伸缩组的策略。可选值：-   OldestInstance：取最早加入伸缩组的 ECS 实例
-   NewestInstance：取最新加入伸缩组的 ECS 实例。
-   OldestScalingConfiguration：取最早伸缩配置创建的实例。

最多可以输入 2 个。

|
|LaunchTemplateId|String|否|实例启动模板 ID，用于指定伸缩组从实例启动模板获取启动配置信息。|
|LaunchTemplateVersion|String|否|实例启动模板采用版本，可选值：-   固定的模板版本号
-   Default：始终使用模板默认版本
-   Latest：始终使用模板最新版本

|
|VSwitchIds.N|String|否| -   只有当伸缩组网络类型为VPC时，当前参数才生效。
-   多可用区参数，N的取值范围为\[1, 5\]。修改伸缩组时可指定同一VPC下最多5个不同的虚拟交换机。
-   指定虚拟交换机所属的VPC必须和伸缩组所属的VPC相同。
-   虚拟交换机的优先级按照数字排序，1为创建实例的第一优先选择。
-   当优先级较高的虚拟交换机所在可用区无法创建实例时，会自动选择下一优先级的虚拟交换机来创建实例。

 |

## 返回参数 { .section}

[公共参数](intl.zh-CN/API参考/公共参数.md#)。

## 示例 { .section}

请求示例

```
http://ess.aliyuncs.com/?Action=ModifyScalingGroup
&ScalingGroupId=cqS5QbbhmvGLcJbWoDbWLj2V
&ScalingGroupName=ScalingGroup
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
< ModifyScalingGroupResponse>
    <RequestId>6469DCD0-13AC-487E-85A0-CE4922908FDE</RequestId>
</ ModifyScalingGroupResponse>
```

`JSON` 格式

```
"RequestId": "6469DCD0-13AC-487E-85A0-CE4922908FDE"
```

## 错误码 {#section_zhy_ddb_kgb .section}

关于所有接口的通用性错误，请参考 [客户端错误](intl.zh-CN/API参考/错误代码/客户端错误.md#) 或 [服务器端错误](intl.zh-CN/API参考/错误代码/服务器端错误.md#)。

|HttpCode|错误码|错误信息|描述|
|:-------|:--|:---|--|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|指定的伸缩组在该用户账号下不存在。|
|400|InvalidScalingGroupName.Duplicate|The specified value of parameter `<parameter name>` is duplicated.|伸缩组名已存在。|
|404|InvalidScalingConfigurationId.NotFound|The specified scaling configuration does not exist.|指定的伸缩配置不存在指定的伸缩组中。|
|400|InvalidScalingConfigurationId.InstanceTypeMismatch|The specified scaling configuration and existing active scaling configuration have different instance type.|指定的伸缩配置的实例规格与当前生效的伸缩配置的实例规格不匹配。|
|400|InvalidParameter.Conflict|The value of parameter `<parameter name>` and parameter `<parameter name>` are confilict.|指定的 MinSize 大于 MaxSize。|
|400|LaunchTemplateVersionSet.NotFound|The specific version of launch template is not exist.|实例启动模板指定版本不存在。|
|400|LaunchTemplateSet.NotFound|The specified launch template set is not found.|指定实例启动模板不存在。|
|400|TemplateMissingParameter.ImageId|The input parameter "ImageId" that is mandatory for processing this request is not supplied.|实例启动模板指定版本缺少镜像信息。|
|400|TemplateMissingParameter.InstanceTypes|The input parameter "InstanceTypes" that is mandatory for processing this request is not supplied.|实例启动模板指定版本缺少实例规格信息。|
|400|TemplateMissingParameter.SecurityGroup|The input parameter "SecurityGroup" that is mandatory for processing this request is not supplied.|实例启动模板指定版本缺少安全组信息。|
|400| TemplateVersion.NotNumber|The input parameter "LaunchTemplateVersion" is supposed to be a string representing the version number.|指定实例启动模板固定版本号为非数字。|

