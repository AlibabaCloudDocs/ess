# EnableScalingGroup {#doc_api_Ess_EnableScalingGroup .reference}

调用EnableScalingGroup启用一个伸缩组。

## 接口说明 {#description .section}

启用一个指定的伸缩组。

-   启用伸缩组成功以后（Active状态），会先把接口中指定的ECS实例加入伸缩组。
-   接口中指定的ECS实例成功加入伸缩组后，如果当前ECS实例数量仍小于MinSize，则弹性伸缩服务会自动创建差额的按量付费的ECS实例。例如：创建伸缩组时，指定MinSize为5，在启用伸缩组的InstanceId.N参数中指定2台已有ECS实例，则弹性伸缩在加入2台已有ECS实例之后，再自动创建3台ECS实例。

    当伸缩组处于Inactive状态时，才可以调用该接口。


当伸缩组没有生效的伸缩配置时，启动伸缩组时需要传入伸缩配置。

-   一个伸缩组在同一时刻只能有一个生效的伸缩配置。
-   如果启动伸缩组之前已经有生效的伸缩配置，在此接口传入新的生效伸缩配置后，原有的伸缩配置会失效。

    手动加入的ECS实例的限定条件：

-   加入的ECS实例必须与伸缩组在同一个地域。
-   加入的ECS实例的规格（InstanceType）必须与生效伸缩配置的实例规格完全一致。
-   加入的ECS实例必须处于Running状态。
-   加入的ECS实例不能已加入到其它伸缩组中。
-   加入的ECS实例支持包年包月和按量付费两种类型。
-   如果伸缩组指定VswitchID，则不支持Classic类型的ECS实例加入伸缩组，也不支持其他VPC的ECS实例加入伸缩组。
-   如果伸缩组没有指定VswitchID，则不支持VPC类型的ECS实例加入伸缩组。

    如果该接口指定的实例数加上当前伸缩组的实例数（Total Capactiy）大于MaxSize，则调用失败。


## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=EnableScalingGroup&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ScalingGroupId|String|是|dmIDKNcyWfzncX9MWX1\*\*\*\*|伸缩组的ID。

 |
|Action|String|否|EnableScalingGroup|系统规定参数，取值：EnableScalingGroup。

 |
|ActiveScalingConfigurationId|String|否|cGsGHrdMBa3DcDrrBVcc\*\*\*\*|需要在伸缩组内激活的伸缩配置的ID。

 |
|InstanceId.1|String|否|i-283vv\*\*\*\*|InstanceId.N为启用后需要加入伸缩组的ECS实例的ID，N的取值范围：1～20。

 |
|LaunchTemplateId|String|否|lt-m5e3ofjr1zn1aw7\*\*\*\*|实例启动模板的ID，用于指定伸缩组从实例启动模板获取启动配置信息。

 |
|LaunchTemplateVersion|String|否|Default|实例启动模板的版本，取值范围：

 -   固定的模板版本号
-   Default：始终使用模板默认版本
-   Latest：始终使用模板最新版本

 |
|LoadBalancerWeight.1|Integer|否|50|LoadBalancerWeight.N为对应ECS实例后端服务器的权重，N的取值范围：1～20，该参数取值范围：0~100。

 默认值：50。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=EnableScalingGroup
&ScalingGroupId=dmIDKNcyWfzncX9MWX1****
&InstanceId.1=i-283vv****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<EnableScalingGroupResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</EnableScalingGroupResponse>
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

|指定的伸缩组在该用户账号下不存在。

|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|用户并未向弹性伸缩完整授权Open API接口。

|
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|指定的伸缩组处于deleting状态。

|
|404

|InvalidScalingConfigurationId.NotFound

|The specified scaling configuration does not exist.

|指定的伸缩配置不存在指定的伸缩组中。

|
|400

|InvalidScalingConfigurationId.InstanceTypeMismatch

|The specified scaling configuration and existing active scaling configuration have different instance type.

|指定的伸缩配置的实例规格与当前生效的伸缩配置的实例规格不匹配。

|
|400

|MissingActiveScalingConfiguration

|An active scaling configuration for the specified scaling group is not supplied.

|伸缩组中未指定生效的伸缩配置。

|
|404

|InvalidInstanceId.NotFound

|Instance “XXX” does not exist.

|指定的ECS实例在该用户账号下不存在。

|
|400

|InvalidInstanceId. RegionMismatch

|Instance “XXX” and the specified scaling group are not in the same Region.

|指定的ECS实例与伸缩组所处的地域不匹配。

|
|400

|InvalidInstanceId. InstanceTypeMismatch

|Instance “XXX” and existing active scaling configuration have different instance type.

|指定的 ECS 实例与伸缩配置的实例规格不匹配。

|
|400

|IncorrectInstanceStatus

|The current status of instance “XXX” does not support this action.

|指定的ECS实例为非running状态。

|
|400

|InvalidInstanceId. NetworkTypeMismatch

|The network type of instance “XXX” does not support this action.

|指定的ECS实例的网络类型与伸缩组的网络类型不匹配。

|
|400

|InvalidInstanceId.VPCMismatch

|Instance “XXX” and the specified scaling group are not in the same VPC.

|指定的伸缩组与添加的ECS实例不在同一个VPC当中。

|
|400

|InvalidInstanceId.InUse

|Instance “XXX” is already attached to another scaling group.

|指定的ECS实例已加入其它伸缩组。

|
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|指定的负载均衡实例未处于active状态。

|
|400

|IncorrectLoadBalancerHealthCheck

|The current health check type of specified load balancer does not support this action.

|指定的负载均衡实例未开启健康检查。

|
|400

|InvalidLoadBalancerId.IncorrectInstanceNetworkType

|The network type of the instance in specified Load Balancer does not support this action.

|指定的负载均衡实例含有的ECS实例的网络类型与伸缩组的网络类型不匹配。

|
|400

|InvalidLoadBalancerId.VPCMismatch

|The specified virtual switch and the instance in specified Load Balancer are not in the same VPC.

|指定的伸缩组的负载均衡实例含有的ECS实例与VSwitchId不在同一个VPC当中。

|
|400

|IncorrectDBInstanceStatus

|The current status of DB instance “XXX” does not support this action.

|指定的RDS实例未处于running状态。

|
|400

|IncorrectCapacity.MaxSize

|To attach the instances, the total capacity will be greater than the max size.

|加入的 ECS 实例数使得Total Capacity超过MaxSize。

|
|400

|LaunchTemplateVersionSet.NotFound

|The specific version of launch template is not exist.

|实例启动模板指定版本不存在。

|
|400

|LaunchTemplateSet.NotFound

|The specified launch template set is not found.

|指定实例启动模板不存在。

|
|400

|TemplateMissingParameter.ImageId

|The input parameter "ImageId" that is mandatory for processing this request is not supplied.

|实例启动模板指定版本缺少镜像信息。

|
|400

|TemplateMissingParameter.InstanceTypes

|The input parameter "InstanceTypes" that is mandatory for processing this request is not supplied.

|实例启动模板指定版本缺少实例规格信息。

|
|400

|TemplateMissingParameter.SecurityGroup

|The input parameter "SecurityGroup" that is mandatory for processing this request is not supplied.

|实例启动模板指定版本缺少安全组信息。

|
|400

|TemplateVersion.NotNumber

|The input parameter "LaunchTemplateVersion" is supposed to be a string representing the version number.

|指定实例启动模板固定版本号为非数字。

|

