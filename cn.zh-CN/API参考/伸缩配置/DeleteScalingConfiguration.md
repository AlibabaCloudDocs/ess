# DeleteScalingConfiguration {#doc_api_1163510 .reference}

删除一个指定的伸缩配置。

## 描述 {#description .section}

伸缩配置在伸缩组中属于生效状态，则该伸缩配置不允许删除。

**某个伸缩配置创建的任意一个ECS实例仍存在于伸缩组中，则该伸缩配置不允许删除。**

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=DeleteScalingConfiguration)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ScalingConfigurationId|String|是|eOs27Kb0oXvQcUYjEGel\*\*\*\*|伸缩配置 ID。

 |
|Action|String|否|DeleteScalingConfiguration|操作接口名，系统规定参数，取值：DeleteScalingConfiguration。

 |

## 返回参数 {#resultMapping .section}

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

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ess)

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

|指定的伸缩配置为非inactive状态。

|
|400

|InstanceInUse

|You cannot delete a scaling configuration or scaling group while there is an instance associated with it.

|指定的伸缩配置还有关联的ECS实例未被删除。

|

