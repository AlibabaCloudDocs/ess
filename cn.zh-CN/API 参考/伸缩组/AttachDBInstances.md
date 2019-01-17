# AttachDBInstances {#concept_85379_zh .concept}

添加一个或多个 RDS 实例。

## 描述 {#section_upc_k2k_sfb .section}

由于存在使用限制，向伸缩组添加 RDS 实例时需要满足以下条件：

-   RDS 实例与伸缩组必须属于同一账号。
-   RDS 实例必须处于 **未锁定** 状态，关于锁定策略，请参考 [RDS使用须知](../../../../../cn.zh-CN/产品简介/RDS使用须知.md#)。
-   RDS 实例必须处于 **运行中** 状态。
-   添加 RDS 实例后，RDS IP 白名单的 default 分组中包含的 IP 不能超过 1000 条，关于 IP 白名单，请参考 [设置白名单](../../../../../cn.zh-CN/用户指南/数据安全性/设置白名单.md#)。

## 请求参数 { .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：`AttachDBInstances`。|
|ScalingGroupId|String|是|伸缩组 Id。|
|DBInstance.N|String|是|RDS 实例 Id，单次最多支持添加 5 个 RDS 实例。|
|ForceAttach|Boolean|否|是否把当前伸缩组内实例的私网 IP 全部添加到 RDS 实例 IP 白名单中： -    `true`：添加
-    `false`：不添加

默认值：`false`。|

## 返回参数 { .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|请求 Id，由系统生成。|

## 示例 { .section}

请求示例

```
http://ess.aliyuncs.com/?Action=AttachDBInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&DBInstance.1=rm-bp12cy39261
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<AttachDBInstancesResponse>
    <RequestId>DD0309B7-2613-4792-9B86-275906695253</RequestId>
</AttachDBInstancesResponse>
```

`JSON` 格式

```
{
    "RequestId": "DD0309B7-2613-4792-9B86-275906695253"
}
```

## 错误码 { .section}

关于所有接口的通用性错误，请参考 [客户端错误](cn.zh-CN/API 参考/错误代码/客户端错误.md#) 或 [服务器端错误](cn.zh-CN/API 参考/错误代码/服务器端错误.md#)。

|HttpCode|错误码|错误信息|描述|
|--------|:--|:---|:-|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|账号下不存在指定的伸缩组。|
|400|QuotaExceeded.RDS|"RDS" quota exceeded.|伸缩组中 RDS 实例超出配额限制。|
|400|InvalidDBInstanceId.NotFound|The specified value of parameter "%s" is not valid.|不存在指定的 RDS 实例。|
|400|IncorrectDBInstanceStatus|The current status of DB instance "%s" does not support this action.|当前 RDS 实例状态不支持该操作。|
|400|QuotaExceeded.DBInstanceSecurityIP|Security IP quota exceeded in DB instance "%s".|RDS 实例后端 IP 白名单个数超出配额。|
|400|InvalidInstanceIds.PrivateIpNotFound|Can not find all private ips of instances in specific scaling group.|无法获取组内 RDS 实例的私网 IP。|

