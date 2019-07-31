# AttachDBInstances {#doc_api_Ess_AttachDBInstances .reference}

调用AttachDBInstances添加一个或多个RDS实例。

## 接口说明 {#description .section}

由于存在使用限制，向伸缩组添加RDS实例时需要满足以下条件：

-   RDS实例与伸缩组必须属于同一账号。
-   RDS实例必须处于未锁定状态，关于锁定策略，请参见[RDS使用须知](~~41872~~)。
-   RDS实例必须处于运行中状态。
-   添加RDS实例后，RDS IP白名单的default分组中包含的IP不能超过1000条，关于IP白名单，请参见[设置白名单](~~26198~~)。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=AttachDBInstances&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DBInstance.N|RepeatList|是|rm-bp12cy3\*\*\*\*|RDS实例的ID，单次最多支持添加5个RDS实例。

 |
|ScalingGroupId|String|是|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组的ID。

 |
|Action|String|否|AttachDBInstances|系统规定参数，取值：AttachDBInstances。

 |
|ForceAttach|Boolean|否|false|是否把当前伸缩组内实例的私网IP全部添加到RDS实例IP白名单中：

 -   true：添加
-   false：不添加

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

|QuotaExceeded.RDS

|"RDS" quota exceeded.

|伸缩组中RDS实例超出配额限制。

|
|400

|InvalidDBInstanceId.NotFound

|The specified value of parameter "%s" is not valid.

|不存在指定的RDS实例。

|
|400

|IncorrectDBInstanceStatus

|The current status of DB instance "%s" does not support this action.

|当前RDS实例状态不支持该操作。

|
|400

|QuotaExceeded.DBInstanceSecurityIP

|Security IP quota exceeded in DB instance "%s".

|RDS实例后端IP白名单个数超出配额。

|
|400

|InvalidInstanceIds.PrivateIpNotFound

|Can not find all private ips of instances in specific scaling group.

|无法获取组内RDS实例的私网IP。

|

