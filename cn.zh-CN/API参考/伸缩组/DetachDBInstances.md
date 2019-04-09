# DetachDBInstances {#doc_api_1163787 .reference}

移除一个或多个 RDS 实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=DetachDBInstances)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DBInstance.N|RepeatList|是|rm-bp12cy3\*\*\*\*|RDS 实例 ID，单次最多支持移除 5 个 RDS 实例。

 |
|ScalingGroupId|String|是|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组 ID。

 |
|Action|String|否|DetachDBInstances|操作接口名，系统规定参数，取值：DetachDBInstances。

 |
|ForceDetach|Boolean|否|false|是否移除 RDS 实例 IP 白名单中属于伸缩组内实例的私网 IP：

 -   true：移除
-   false：不移除

 默认值：false

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DetachDBInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&DBInstance.1=rm-bp12cy3****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DetachDBInstancesResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DetachDBInstancesResponse>

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

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|账号下不存在指定的伸缩组。

|
|400

|InvalidDBInstanceId.NotFound

|DB instance "%s" does not exist.

|不存在指定的 RDS 实例。

|

