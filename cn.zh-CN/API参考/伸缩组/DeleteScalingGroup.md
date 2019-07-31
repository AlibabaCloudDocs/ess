# DeleteScalingGroup {#doc_api_Ess_DeleteScalingGroup .reference}

调用DeleteScalingGroup删除一个伸缩组。

## 接口说明 {#description .section}

删除一个指定的伸缩组。

ForceDelete属性表示如果伸缩组存在ECS实例或正在进行伸缩活动，是否强制删除伸缩组并移出和释放ECS实例。

-   如果ForceDelete属性为false，并且满足以下两个条件，会先停止伸缩组，然后再删除伸缩组。
    -   伸缩组没有任何伸缩活动正在执行。
    -   伸缩组当前的ECS实例数量（Total Capacity）为0。
-   ForceDelete属性为true时，会先停止伸缩组，拒绝接收新的伸缩活动请求，然后等待已有的伸缩活动完成，最后将伸缩组内所有ECS实例移出伸缩组（用户手工添加的ECS实例会被移出伸缩组，弹性伸缩自动创建的ECS实例会被自动删除）并删除伸缩组。

删除伸缩组，包括删除相关联的伸缩配置、伸缩规则、伸缩活动、伸缩请求的信息。

删除伸缩组，不会删除以下任务或实例：定时任务、云监控报警任务、负载均衡实例、RDS实例。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DeleteScalingGroup&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ScalingGroupId|String|是|dmIDKNcyWfzncX9MWX1\*\*\*\*|伸缩组的ID。

 |
|Action|String|否|DeleteScalingGroup|系统规定参数，取值：DeleteScalingGroup。

 |
|ForceDelete|Boolean|否|false|如伸缩组存在ECS实例或正在进行伸缩活动，是否强制删除伸缩组并移出和释放ECS实例。取值范围：

 -   true：强制删除伸缩组。
-   false：不强制删除伸缩组。

 默认值：false。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DeleteScalingGroup
&ScalingGroupId=dmIDKNcyWfzncX9MWX1****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteScalingGroupResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DeleteScalingGroupResponse>
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

|InstanceInUse

|You cannot delete a scaling configuration or scaling group while there is an instance associated with it.

|指定的伸缩组中存在ECS实例。

|

