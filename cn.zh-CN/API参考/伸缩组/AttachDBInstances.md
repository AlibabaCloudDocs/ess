# AttachDBInstances {#doc_api_1163790 .reference}

添加一个或多个 RDS 实例。

## 描述 {#description .section}

由于存在使用限制，向伸缩组添加 RDS 实例时需要满足以下条件：

-   RDS 实例与伸缩组必须属于同一账号。
-   RDS 实例必须处于 **未锁定** 状态，关于锁定策略，请参考 [RDS使用须知](~~41872~~)。
-   RDS 实例必须处于 **运行中** 状态。
-   添加 RDS 实例后，RDS IP 白名单的 default 分组中包含的 IP 不能超过 1000 条，关于 IP 白名单，请参考 [设置白名单](~~26198~~)。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=AttachDBInstances)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DBInstance.N|RepeatList|是|rm-bp12cy3\*\*\*\*|RDS 实例 ID，单次最多支持添加 5 个 RDS 实例。

 |
|ScalingGroupId|String|是|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组 ID。

 |
|Action|String|否|AttachDBInstances|操作接口名，系统规定参数，取值：AttachDBInstances。

 |
|ForceAttach|Boolean|否|false|是否把当前伸缩组内实例的私网 IP 全部添加到 RDS 实例 IP 白名单中：

 -   true：添加
-   false：不添加

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

http://ess.aliyuncs.com/?Action=AttachDBInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&DBInstance.1=rm-bp12cy3****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AttachDBInstancesResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</AttachDBInstancesResponse>

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

|QuotaExceeded.RDS

|"RDS" quota exceeded.

|伸缩组中 RDS 实例超出配额限制。

|
|400

|InvalidDBInstanceId.NotFound

|The specified value of parameter "%s" is not valid.

|不存在指定的 RDS 实例。

|
|400

|IncorrectDBInstanceStatus

|The current status of DB instance "%s" does not support this action.

|当前 RDS 实例状态不支持该操作。

|
|400

|QuotaExceeded.DBInstanceSecurityIP

|Security IP quota exceeded in DB instance "%s".

|RDS 实例后端 IP 白名单个数超出配额。

|
|400

|InvalidInstanceIds.PrivateIpNotFound

|Can not find all private ips of instances in specific scaling group.

|无法获取组内 RDS 实例的私网 IP。

|

