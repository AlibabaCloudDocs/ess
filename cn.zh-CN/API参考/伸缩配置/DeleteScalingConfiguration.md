# DeleteScalingConfiguration {#doc_api_Ess_DeleteScalingConfiguration .reference}

调用DeleteScalingConfiguration删除一个伸缩配置。

## 接口说明 {#description .section}

以下情况不能删除伸缩配置：

-   伸缩配置在伸缩组中处于生效状态。
-   伸缩组中仍然存在使用该伸缩配置创建的ECS实例。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DeleteScalingConfiguration&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ScalingConfigurationId|String|是|eOs27Kb0oXvQcUYjEGel\*\*\*\*|待删除伸缩配置的ID。

 |
|Action|String|否|DeleteScalingConfiguration|系统规定参数，取值：DeleteScalingConfiguration。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DeleteScalingConfiguration
&ScalingConfigurationId=eOs27Kb0oXvQcUYjEGel****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteScalingConfigurationResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DeleteScalingConfigurationResponse>
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

|InvalidScalingConfigurationId.NotFound

|The specified scaling configuration does not exist.

|指定的伸缩配置在该用户账号下不存在。

|
|400

|IncorrectScalingConfigurationLifecycleState

|The current lifecycle state of specified scaling configuration does not support this action.

|指定的伸缩配置未处于Inactive状态。

|
|400

|InstanceInUse

|You cannot delete a scaling configuration or scaling group while there is an instance associated with it.

|指定的伸缩配置还有关联的ECS实例未被删除。

|

