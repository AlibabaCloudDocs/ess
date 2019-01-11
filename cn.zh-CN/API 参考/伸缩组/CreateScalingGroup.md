# CreateScalingGroup {#concept_25936_zh .concept}

创建一个伸缩组（CreateScalingGroup）。伸缩组是具有相同应用场景的 ECS 实例集合，伸缩组有最大 ECS 实例数、最小 ECS 实例数、移出策略、冷却时间、关联的负载均衡实例和关联的 RDS 实例等属性。

## 描述 {#section_ayt_bdb_kgb .section}

-   伸缩组、关联的负载均衡实例和关联的 RDS 实例必须在同一个地域。更多详情，请参阅 [地域与可用区](../../../../../intl.zh-CN/通用参考/地域和可用区.md#)。

-   您最多能创建 20 个伸缩组。

-   伸缩组创建成功后，伸缩组不会立即生效。您需要启用伸缩组（`EnableScalingGroup`）后，才能触发伸缩活动和接受伸缩规则。

-   如果在伸缩组中指定了负载均衡实例：

    -   指定的负载均衡实例必须是 **运行中**（**active**） 状态。
    -   伸缩组自动将加入伸缩组的 ECS 实例添加到指定的负载均衡实例中。
    -   指定的负载均衡实例所有配置的监听端口必须开启健康检查，否则创建失败。
    -   加入负载均衡实例的 ECS 实例权重默认为 50。
-   如果在伸缩组中指定了 RDS 实例：

    -   指定的 RDS 实例必须是 **运行中**（**running**）状态。
    -   伸缩组自动将加入伸缩组的 ECS 实例的内网 IP 添加到指定的 RDS 实例的访问白名单当中。
    -   指定的 RDS 实例访问白名单的 IP 数不能超过上限值。更多详情，请参阅 *RDS* [设置白名单](../../../../../intl.zh-CN/用户指南/数据安全性/设置白名单.md#)。

## 请求参数 {#section_lt4_vd2_sfb .section}

|名称|类型|是否必选|描述|
|--|--|----|--|
|Action|String|是|系统规定参数。取值：CreateScalingGroup|
|RegionId|String|是|伸缩组所属的地域 ID。更多详情，请参阅 [地域与可用区](../../../../../intl.zh-CN/通用参考/地域和可用区.md#)。|
|MaxSize|Integer|是|伸缩组内 ECS 实例台数的最大值，取值范围：\[0, 1000\]。 当伸缩组内 ECS 实例数大于 MaxSize 时，弹性伸缩会自动移出 ECS 实例。|
|MinSize|Integer|是|伸缩组内 ECS 实例台数的最小值，取值范围：\[0, 1000\] 。当伸缩组内 ECS 实例数小于 MinSize 时，弹性伸缩会自动创建 ECS 实例。|
|ScalingGroupName|String|否| 伸缩组的显示名称，不能与您当前地域下的伸缩组重名。长度为 \[2, 40\] 个英文或中文字符，以数字、大小字母或中文开头，可包含数字、下划线（\_）、连字符（-）和小数点（.）。

 默认值：伸缩组 ID

 |
|DefaultCooldown|Integer|否| 一次伸缩活动（添加或移出 ECS 实例）结束后的一段冷却时间。取值范围：\[0, 86400\]，单位：秒。 

 默认值：300

 冷却时间内，该伸缩组不执行其它的伸缩活动。目前，仅针对 [云监控](../../../../../intl.zh-CN/产品简介/产品概述.md#) 报警任务触发的伸缩活动有效。

 |
|RemovalPolicy.N|String|否| 移出 ECS 实例的伸缩组策略，更多详情，请参阅 [移出策略](../../../../../intl.zh-CN/用户指南/管理伸缩组的伸缩活动/实现自动伸缩/移出策略.md#)。N的取值范围 \[1,2\]。取值范围：

 -   OldestInstance：移出最早加入伸缩组的 ECS 实例
-   NewestInstance：移出最新加入伸缩组的 ECS 实例
-   OldestScalingConfiguration：移出最早伸缩配置创建的 ECS 实例

 默认值：OldestScalingConfiguration 和 OldestInstance

 |
|LoadBalancerIds|String|否|负载均衡实例 ID。取值可以由多台负载均衡实例 ID 组成一个 JSON 数组，格式为 \["lb-idx", "lb-idy", … "lb-idz"\]，最多支持 5 个 ID，ID 之间用半角逗号（,）隔开。|
|VServerGroup.N.LoadBalancerId|String|否|虚拟服务器组所属负载均衡实例的ID。|
|VServerGroup.N.VServerGroupAttribute.M.VServerGroupId|String|否|虚拟服务器组ID。|
|VServerGroup.N.VServerGroupAttribute.M.Port|Integer|否|弹性伸缩将ECS实例添加到虚拟服务器组时使用的端口号，取值范围：1-65535。|
|VServerGroup.N.VServerGroupAttribute.M.Weight|Integer|否|弹性伸缩将ECS实例添加到虚拟服务器组时设置的权重，取值范围：0-100。默认值：50。

|
|DBInstanceIds|String|否|RDS 实例 ID。取值可以由多台 RDS 实例 ID 组成一个 JSON 数组，格式为 \["rm-idx", "rm-idy", … "rm-idz"\]，最多支持 8 个 ID，ID 之间用半角逗号（,）隔开。|
|VSwitchId|String|否|创建 VPC 类型的伸缩组时，指定的虚拟交换机 ID。|
|VSwitchIds.N|String|否| 一台或多台虚拟交换机 ID，N 的取值范围为 \[1, 5\]。如果您使用了 VSwitchIds.N 参数，VSwitchId 参数将被忽略。

 -   虚拟交换机可以来自多个可用区。
-   虚拟交换机的优先级按照数字升序排序，1 表示最高优先级。当优先级较高的虚拟交换机所在可用区无法创建 ECS 实例时，自动选择下一优先级的虚拟交换机创建 ECS 实例。

 |
|ScalingPolicy|String|否|指定伸缩组的回收模式，可选值：-   recycle：伸缩组的回收模式为停机回收模式
-   release：伸缩组的回收模式为释放模式

关于被移出实例的动作，请参阅 [RemoveInstances](intl.zh-CN/API 参考/触发任务/移出ECS实例.md#)。

|
|MultiAZPolicy|String|否| 多可用区伸缩组 ECS 实例扩缩容策略。取值范围：

 -   PRIORITY：根据您定义的虚拟交换机（VSwitchIds.N）扩缩容。当优先级较高的虚拟交换机所在可用区无法创建 ECS 实例时，自动使用下一优先级的虚拟交换机创建 ECS 实例。
-   COST\_OPTIMIZED：按 vCPU 单价从低到高进行尝试创建。当伸缩配置设置了抢占式计费方式的多实例规格时，优先创建对应抢占式计费实例。当抢占式计费实例由于库存等原因无法创建时，自动尝试以按量付费的方式创建。

**说明：** COST\_OPTIMIZED 仅在伸缩配置设置了多实例规格或者选用了抢占式实例的情况下生效。

-   BALANCE：在伸缩组指定的多可用区之间均匀分配 ECS 实例。如果由于库存不足等原因可用区之间变得不平衡，您可以通过 API RebalanceInstance 平衡资源。

 默认值：PRIORITY

 |
|LaunchTemplateId|String|否|实例启动模板 ID，用于指定伸缩组从实例启动模板获取启动配置信息。|
|LaunchTemplateVersion|String|否|实例启动模板采用版本，可选值：-   固定的模板版本号
-   Default：始终使用模板默认版本
-   Latest：始终使用模板最新版本

|

## 返回参数 {#section_zt4_vd2_sfb .section}

|名称|类型|描述|
|--|--|--|
|ScalingGroupId|String|伸缩组 ID|

## 示例 {#section_b54_vd2_sfb .section}

请求示例

```language-shell
http://ess.aliyuncs.com/?Action=CreateScalingGroup
&RegionId=cn-qingdao
&MaxSize=20
&MinSize=2
&LoadBalancerId=147b46d767c-cn-qingdao-cm5-a01
&DBInstanceId.1=rdszzzyyunybaeu
&DBInstanceId.2=rdsia3u3yia3u3y
&<公共请求参数>

```

正常返回示例

`XML` 格式

```language-xml
<CreateScalingGroupResponse>
    <ScalingGroupId>dP8VqSd9ENXPc0ciVmbcrBT1</ScalingGroupId>
    <RequestId>536E9CAD-DB30-4647-AC87-AA5CC38C5382</RequestId>
</CreateScalingGroupResponse>

```

`JSON` 格式

```language-json
{
	"RequestId": "536E9CAD-DB30-4647-AC87-AA5CC38C5382",
	"ScalingGroupId": "dP8VqSd9ENXPc0ciVmbcrBT1"
}


```

## 错误码 {#section_f54_vd2_sfb .section}

以下为 CreatScalingGroup 接口的特有错误码。对于所有接口的通用性错误，请参考 [客户端错误](intl.zh-CN/API 参考/错误代码/客户端错误.md#) 或 [服务器端错误](intl.zh-CN/API 参考/错误代码/服务器端错误.md#)。

 

|错误码|错误信息|HttpCode|描述|
|---|----|--------|--|
|IncorrectDBInstanceStatus|The current status of DB instance “XXX” does not support this action.|400|指定的 RDS 实例必须是 **运行中** 状态。|
|IncorrectLoadBalancerHealthCheck|The current health check type of specified load balancer does not support this action.|400|指定的负载均衡实例必须开启健康检查。|
|IncorrectLoadBalancerStatus|The current status of the specified load balancer does not support this action.|400|指定的负载均衡实例必须是启用状态。|
|IncorrectVSwitchStatus|The current status of virtual switch does not support this operation.|400|虚拟交换机不可用，无法创建 ECS 实例。|
|InvalidDBInstanceId. RegionMismatch|DB instance “XXX” and the specified scaling group are not in the same Region.|400|指定的 RDS 实例与伸缩组必须在同一地域。|
|InvalidLoadBalancerId.IncorrectAddressType|The current address type of specified load balancer does not support this action.|400|指定虚拟交换机后，负载均衡实例为私网类型。更多详情，请参阅 [负载均衡实例](../../../../../intl.zh-CN/产品简介/什么是负载均衡.md#)。|
|InvalidLoadBalancerId.IncorrectInstanceNetworkType|The network type of the instance in specified Load Balancer does not support this action.|400|指定的负载均衡实例内搭载的 ECS 实例的网络类型与伸缩组的网络类型必须一致。|
|InvalidLoadBalancerId.RegionMismatch|The specified Load Balancer and the specified scaling group are not in the same Region.|400|指定的负载均衡实例与伸缩组必须在同一地域。|
|InvalidLoadBalancerId.VPCMismatch|The specified virtual switch and the instance in specified Load Balancer are not in the same VPC.|400|伸缩组内的负载均衡实例搭载的 ECS 实例与虚拟交换机应该在同一个 VPC 中。|
|InvalidParameter|The specified value of parameter "ScalingPolicy" is not valid.|400|指定的回收模式参数不存在。|
|InvalidParameter.Conflict|The value of parameter <parameter name" and parameter <parameter name" are conflict.|400|指定的 MinSize 不能大于 MaxSize。|
|InvalidScalingGroupName.Duplicate|The specified value of parameter <parameter name" is duplicated.|400|伸缩组名已存在。|
|QuotaExceeded.DBInstanceSecurityIP|Security IP quota exceeded in DB instance “XXX”.|400|指定的 RDS 实例访问白名单的 IP 个数达到上限。|
|QuotaExceeded.PrivateIpAddress|Private IP address quota exceeded in the specified virtual switch.|400|虚拟交换机无法再分配多余的私有 IP 地址。|
|QuotaExceeded.ScalingGroup|Scaling group quota exceeded.|400|用户的伸缩组使用个数达到上限。|
|QuotaExceeded.VPCInstance|Instance quota exceeded in the specified VPC.|400|该 VPC 内的实例数超过数量限制。|
|InvalidDBInstanceId.NotFound|DB instance “XXX” does not exist.|404|指定的 RDS 实例不存在。|
|InvalidLoadBalancerId.NotFound|The specified Load Balancer does not exist.|404|指定的负载均衡实例不存在。|
|InvalidRegionId.NotFound|The specified region does not exist.|404|指定的地域不存在。|
|InvalidVSwitchId.NotFound|The specified virtual switch does not exist.|404|指定的虚拟交换机不存在。|
|LaunchTemplateVersionSet.NotFound|The specific version of launch template is not exist.|400|实例启动模板指定版本不存在。|
|LaunchTemplateSet.NotFound|The specified launch template set is not found.|400|指定实例启动模板不存在。|
|TemplateMissingParameter.ImageId|The input parameter "ImageId" that is mandatory for processing this request is not supplied.|400|实例启动模板指定版本缺少镜像信息。|
|TemplateMissingParameter.InstanceTypes|The input parameter "InstanceTypes" that is mandatory for processing this request is not supplied.|400|实例启动模板指定版本缺少实例规格信息。|
|TemplateMissingParameter.SecurityGroup|The input parameter "SecurityGroup" that is mandatory for processing this request is not supplied.|400|实例启动模板指定版本缺少安全组信息。|
| TemplateVersion.NotNumber|The input parameter "LaunchTemplateVersion" is supposed to be a string representing the version number.|400|指定实例启动模板固定版本号为非数字。|

