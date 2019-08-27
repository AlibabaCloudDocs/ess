# ModifyScalingGroup {#doc_api_Ess_ModifyScalingGroup .reference}

调用ModifyScalingGroup修改一个伸缩组。

## 接口说明 {#description .section}

-   不支持修改以下参数：
    -   RegionId
    -   LoadBalancerId

**说明：** 如果需要修改负载均衡实例，请使用[AttachLoadBalancers](~~85125~~)和[DetachLoadBalancers](~~85141~~)接口。

    -   DBInstanceId

**说明：** 如果需要修改RDS实例，请使用[AttachDBInstances](~~85379~~)和[DetachDBInstances](~~85380~~)接口。

-   当伸缩组的状态为Active或Inactive时才能调用该接口。
-   启用新的伸缩配置不会影响通过早前伸缩配置创建并正在运行的ECS实例。
-   如果修改了MaxSize，导致伸缩组的ECS实例数超过MaxSize，伸缩组会自动移出ECS实例，使得伸缩组的ECS实例数等于MaxSize。
-   如果修改了MinSize，导致伸缩组的ECS实例数低于MinSize，伸缩组会自动加入ECS实例，使得伸缩组的ECS实例数等于MinSize。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=ModifyScalingGroup&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ScalingGroupId|String|是|cqS5QbbhmvGLcJbWoDbW\*\*\*\*|待修改伸缩组的ID。

 |
|Action|String|否|ModifyScalingGroup|系统规定参数。取值：ModifyScalingGroup。

 |
|ActiveScalingConfigurationId|String|否|bU5uZHcAgtzwcL4IeDea\*\*\*\*|伸缩组内生效的伸缩配置的ID。

 |
|DefaultCooldown|Integer|否|600|一次伸缩活动（添加或移出ECS实例）结束后的一段冷却时间。取值范围：0~86400，单位：秒。

 冷却时间内，该伸缩组不执行其它的伸缩活动，仅针对[云监控](~~35170~~)报警任务触发的伸缩活动有效。

 |
|HealthCheckType|String|否|ECS|伸缩组的健康检查方式，取值范围：

 -   NONE：不做健康检查。
-   ECS：对伸缩组内的ECS实例做健康检查。

 |
|LaunchTemplateId|String|否|lt-m5e3ofjr1zn1aw7\*\*\*\*|实例启动模板ID，用于指定伸缩组从实例启动模板获取启动配置信息。

 |
|LaunchTemplateVersion|String|否|Default|实例启动模板的版本，取值范围：

 -   固定的模板版本号
-   Default：始终使用模板默认版本
-   Latest：始终使用模板最新版本

 |
|MaxSize|Integer|否|99|伸缩组内ECS实例台数的最大值，取值范围：0~1000。 当伸缩组内ECS实例数大于MaxSize时，弹性伸缩会自动移出ECS实例。

 |
|MinSize|Integer|否|1|伸缩组内ECS实例台数的最小值，取值范围：0~1000 。当伸缩组内ECS实例数小于MinSize时，弹性伸缩会自动创建ECS实例。

 |
|OnDemandBaseCapacity|Integer|否|30|伸缩组所需要按量实例个数的最小值，取值范围：0~1000。当按量实例个数少于该值时，将优先创建按量实例。

 |
|OnDemandPercentageAboveBaseCapacity|Integer|否|20|伸缩组满足最小按量实例数（OnDemandBaseCapacity）要求后，超出的实例中按量实例应占的比例，取值范围：0～100。

 |
|RemovalPolicy.1|String|否|OldestScalingConfiguration|RemovalPolicy.N指定移出ECS实例的伸缩组策略，N的取值范围：1~2。更多详情，请参见[移出策略](~~25910~~)。取值范围：

 -   OldestInstance：移出最早加入伸缩组的ECS实例
-   NewestInstance：移出最新加入伸缩组的ECS实例
-   OldestScalingConfiguration：移出最早伸缩配置创建的ECS实例

 |
|ScalingGroupName|String|否|Scaling\*\*\*\*|伸缩组的名称，同一地域下伸缩组名称唯一。长度为2~40个英文或中文字符，以数字、大小英文字母或中文开头，可以包含数字、下划线（\_）、连字符（-）和小数点（.）。

 |
|SpotInstancePools|Integer|否|5|指定可用实例规格的个数，伸缩组将按成本最低的多个规格均衡创建抢占式实例。取值范围：0~10。

 |
|SpotInstanceRemedy|Boolean|否|true|是否开启补齐抢占式实例。开启后，当收到抢占式实例将被回收的系统消息时，伸缩组将尝试创建新的实例，替换掉将被回收的抢占式实例。

 |
|VSwitchIds.N|RepeatList|否|vsw-\*\*\*\*|一台或多台虚拟交换机的ID，N的取值范围：1~5。

 只有当伸缩组网络类型为VPC时，当前参数才生效。指定虚拟交换机所属的VPC必须和伸缩组所属的VPC相同。

 虚拟交换机可以来自多个可用区。虚拟交换机的优先级按照数字升序排序，1表示最高优先级。当优先级较高的虚拟交换机所在可用区无法创建ECS实例时，自动选择下一优先级的虚拟交换机创建ECS实例。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=ModifyScalingGroup
&ScalingGroupId=cqS5QbbhmvGLcJbWoDbW****
&ScalingGroupName=Scaling****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyScalingGroupResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyScalingGroupResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述

|
|----------|-----|------|----|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|账号下不存在指定的伸缩组。

|
|400

|InvalidScalingGroupName.Duplicate

|The specified value of parameter <parameter name\> is duplicated.

|伸缩组名已存在。

|
|404

|InvalidScalingConfigurationId.NotFound

|The specified scaling configuration does not exist.

|伸缩组中不存在指定的伸缩配置。

|
|400

|InvalidScalingConfigurationId.InstanceTypeMismatch

|The specified scaling configuration and existing active scaling configuration have different instance type.

|指定的伸缩配置的实例规格与当前生效的伸缩配置的实例规格不匹配。

|
|400

|InvalidParameter.Conflict

|The value of parameter <parameter name\> and parameter <parameter name\> are confilict.

|指定的MinSize大于MaxSize。

|
|400

|LaunchTemplateVersionSet.NotFound

|The specific version of launch template is not exist.

|不存在指定的实例启动模板版本。

|
|400

|LaunchTemplateSet.NotFound

|The specified launch template set is not found.

|不存在指定的实例启动模板。

|
|400

|TemplateMissingParameter.ImageId

|The input parameter "ImageId" that is mandatory for processing this request is not supplied.

|实例启动模板指定版本缺少镜像信息。

|
|400

|TemplateMissingParameter.InstanceTypes

|The input parameter "InstanceTypes" that is mandatory for processing this request is not supplied.

|指定的实例启动模板版本缺少实例规格信息。

|
|400

|TemplateMissingParameter.SecurityGroup

|The input parameter "SecurityGroup" that is mandatory for processing this request is not supplied.

|指定的实例启动模板版本缺少安全组信息。

|
|400

|TemplateVersion.NotNumber

|The input parameter "LaunchTemplateVersion" is supposed to be a string representing the version number.

|指定的实例启动模板固定版本号应该是数字。

|

