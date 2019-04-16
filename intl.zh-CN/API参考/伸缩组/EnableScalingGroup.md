# EnableScalingGroup {#concept_25939_zh .concept}

本文介绍启用伸缩组API操作。

## 描述 {#section_gxd_1x2_sfb .section}

-   启用一个指定的伸缩组。
    -   启用伸缩组成功以后（active 状态），会先把接口中指定的 ECS 实例加入伸缩组。
    -   接口中指定的 ECS 实例成功加入伸缩组后，如果当前 ECS 实例数量仍小于 MinSize，则弹性伸缩服务会自动创建差额的按量付费的 ECS 实例。例：创建伸缩组时，指定 MinSize = 5，在启用伸缩组的 InstanceId.N 参数中指定 2 台已有 ECS 实例，则弹性伸缩在加入 2 台已有 ECS 实例之后，再自动创建 3 台 ECS 实例。
-   当伸缩组为 Inactive 状态，才可以调用该接口。
-   当伸缩组没有生效的伸缩配置时，启动伸缩组时需要传入伸缩配置。
    -   一个伸缩组在同一时刻只能有一个生效的伸缩配置。
    -   如果启动伸缩组之前已经有生效的伸缩配置，在此接口传入新的生效伸缩配置后，原有的伸缩配置会失效。
-   加入的 ECS 实例的限定条件：
    -   加入的 ECS 实例必须与伸缩组在同一个地域。
    -   加入的 ECS 实例的规格（InstanceType）必须与生效伸缩配置的实例规格完全一致。
    -   加入的 ECS 实例必须是 **Running** 状态。
    -   加入的 ECS 实例不能已加入到其它伸缩组中。
    -   加入的 ECS 实例支持包年包月和按量付费两种类型。
    -   如果伸缩组指定 VswitchID，则不支持 Classic 类型的 ECS 实例加入伸缩组，也不支持其他 VPC 的 ECS 实例加入伸缩组。
    -   如果伸缩组没有指定 VswitchID，则不支持 VPC 类型的 ECS 实例加入伸缩组。
-   如果该接口指定的实例数加上当前伸缩组的实例数（Total Capactiy）大于 MaxSize 时，则调用失败。

## 请求参数 { .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：EnableScalingGroup。|
|ScalingGroupId|String|是|伸缩组的 ID。|
|ActiveScalingConfigurationId|String|否|需要在伸缩组内激活的伸缩配置的 ID。|
|InstanceId.N|String|否|启用后需要加入伸缩组的 ECS 实例的 ID。最多可以输入 20 个。|
|LaunchTemplateId|String|否|实例启动模板 ID，用于指定伸缩组从实例启动模板获取启动配置信息。|
|LaunchTemplateVersion|String|否|实例启动模板采用版本，可选值：-   固定的模板版本号
-   Default：始终使用模板默认版本
-   Latest：始终使用模板最新版本

|

## 返回参数 { .section}

[公共参数](intl.zh-CN/API参考/公共参数.md#)。

## 示例 { .section}

请求示例

```
http://ess.aliyuncs.com/?Action=EnableScalingGroup 
&ScalingGroupId=dmIDKNcyWfzncX9MWX1bwFV
&InstanceId.1=i-283vvyytn
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
< EnableScalingGroupResponse>
    <RequestId>6469DCD0-13AC-487E-85A0-CE4922908FDE</RequestId>
</ EnableScalingGroupResponse>
```

`JSON` 格式

```
{
    "RequestId": "6469DCD0-13AC-487E-85A0-CE4922908FDE"
}
```

## 错误码 {#section_ky5_mdb_kgb .section}

关于所有接口的通用性错误，请参考 [客户端错误](intl.zh-CN/API参考/错误代码/客户端错误.md#) 或 [服务器端错误](intl.zh-CN/API参考/错误代码/服务器端错误.md#)。

|HttpCode|错误码|错误信息|描述|
|:-------|:--|:---|--|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|指定的伸缩组在该用户账号下不存在。|
|403|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|用户并未向弹性伸缩完整授权 Open API 接口。|
|400|IncorrectScalingGroupStatus|The current status of the specified scaling group does not support this action.|指定的伸缩组为 deleting 状态。|
|404|InvalidScalingConfigurationId.NotFound|The specified scaling configuration does not exist.|指定的伸缩配置不存在指定的伸缩组中。|
|400|InvalidScalingConfigurationId.InstanceTypeMismatch|The specified scaling configuration and existing active scaling configuration have different instance type.|指定的伸缩配置的实例规格与当前生效的伸缩配置的实例规格不匹配。|
|400|MissingActiveScalingConfiguration|An active scaling configuration for the specified scaling group is not supplied.|伸缩组中未指定生效的伸缩配置。|
|404|InvalidInstanceId.NotFound|Instance “XXX” does not exist.|指定的 ECS 实例在该用户账号下不存在。|
|400|InvalidInstanceId. RegionMismatch|Instance “XXX” and the specified scaling group are not in the same Region.|指定的 ECS 实例与伸缩组所处的地域不匹配。|
|400|InvalidInstanceId. InstanceTypeMismatch|Instance “XXX” and existing active scaling configuration have different instance type.|指定的 ECS 实例与伸缩配置的实例规格不匹配。|
|400|IncorrectInstanceStatus|The current status of instance “XXX” does not support this action.|指定的ECS实例为非running状态。|
|400|InvalidInstanceId. NetworkTypeMismatch|The network type of instance “XXX” does not support this action.|指定的ECS实例的网络类型与伸缩组的网络类型不匹配。|
|400|InvalidInstanceId.VPCMismatch|Instance “XXX” and the specified scaling group are not in the same VPC.|指定的伸缩组与添加的 ECS 实例不在同一个 VPC 当中。|
|400|InvalidInstanceId.InUse|Instance “XXX” is already attached to another scaling group.|指定的 ECS 实例已加入其它伸缩组。|
|400|IncorrectLoadBalancerStatus|The current status of the specified load balancer does not support this action.|指定的负载均衡实例为非 active 状态。|
|400|IncorrectLoadBalancerHealthCheck|The current health check type of specified load balancer does not support this action.|指定的负载均衡实例未开启健康检查。|
|400|InvalidLoadBalancerId.IncorrectInstanceNetworkType|The network type of the instance in specified Load Balancer does not support this action.|指定的负载均衡实例含有的 ECS 实例的网络类型与伸缩组的网络类型不匹配。|
|400|InvalidLoadBalancerId.VPCMismatch|The specified virtual switch and the instance in specified Load Balancer are not in the same VPC.|指定的伸缩组的负载均衡实例含有的 ECS 实例与 VSwitchId 不在同一个 VPC 当中。|
|400|IncorrectDBInstanceStatus|The current status of DB instance “XXX” does not support this action.|指定的 RDS 实例为非 running 状态。|
|400|IncorrectCapacity.MaxSize|To attach the instances, the total capacity will be greater than the max size.|加入的 ECS 实例数使得 Total Capacity 超过 MaxSize。|
|400|LaunchTemplateVersionSet.NotFound|The specific version of launch template is not exist.|实例启动模板指定版本不存在。|
|400|LaunchTemplateSet.NotFound|The specified launch template set is not found.|指定实例启动模板不存在。|
|400|TemplateMissingParameter.ImageId|The input parameter "ImageId" that is mandatory for processing this request is not supplied.|实例启动模板指定版本缺少镜像信息。|
|400|TemplateMissingParameter.InstanceTypes|The input parameter "InstanceTypes" that is mandatory for processing this request is not supplied.|实例启动模板指定版本缺少实例规格信息。|
|400|TemplateMissingParameter.SecurityGroup|The input parameter "SecurityGroup" that is mandatory for processing this request is not supplied.|实例启动模板指定版本缺少安全组信息。|
|400| TemplateVersion.NotNumber|The input parameter "LaunchTemplateVersion" is supposed to be a string representing the version number.|指定实例启动模板固定版本号为非数字。|

