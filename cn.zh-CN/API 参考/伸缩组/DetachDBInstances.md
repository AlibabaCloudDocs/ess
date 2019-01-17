# DetachDBInstances {#concept_85380_zh .concept}

移除一个或多个RDS实例。

## 请求参数 {#section_mpm_v2k_sfb .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：`DetachDBInstances`。|
|ScalingGroupId|String|是|伸缩组 Id。|
|DBInstance.N|String|是|RDS 实例 Id，单次最多支持移除 5 个 RDS 实例。|
|ForceDetach|Boolean|否|是否移除 RDS 实例 IP 白名单中属于伸缩组内实例的私网 IP： -    `true`：移除
-    `false`：不移除

默认值：`false`。|

## 返回参数 { .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|请求Id，由系统生成。|

## 示例 { .section}

请求示例

```
http://ess.aliyuncs.com/?Action=DetachDBInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&DBInstance.1=rm-bp12cy39261
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DetachDBInstancesResponse>
    <RequestId>DD0309B7-2613-4792-9B86-275906695253</RequestId>
</DetachDBInstancesResponse>
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
|400|InvalidDBInstanceId.NotFound|DB instance "%s" does not exist.|不存在指定的 RDS 实例。|

