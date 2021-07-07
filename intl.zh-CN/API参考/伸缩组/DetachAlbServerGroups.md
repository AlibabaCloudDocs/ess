# DetachAlbServerGroups

调用DetachAlbServerGroups从伸缩组移出一个或多个ALB服务器组。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DetachAlbServerGroups&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AlbServerGroup.N.AlbServerGroupId|String|是|sgp-ddwb0y0g6y9bjm\*\*\*\*|ALB服务器组的ID。N为ALB服务器组的编号。 |
|AlbServerGroup.N.Port|Integer|是|22|ALB服务器组中ECS实例使用的端口号。N为ALB服务器组的编号。 |
|RegionId|String|是|cn-hangzhou|伸缩组所属地域的ID，如cn-hangzhou、cn-shanghai。更多信息，请参见[地域和可用区](~~40654~~)。 |
|ScalingGroupId|String|是|asg-bp18p2yfxow2dloq\*\*\*\*|伸缩组的ID。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多信息，请参见[如何保证幂等性](~~25965~~)。 |
|ForceDetach|Boolean|否|false|是否将从待移出ALB服务器组中移出已有的ECS实例。

 -   true：移出，并返回`ScalingActivityId`，您可以通过查看该伸缩活动ID来确定已有实例是否移出成功。
-   false：不移出。

 默认值：false |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|ScalingActivityId|String|asa-2ze6wxj8vsohn6j9\*\*\*\*|移出ALB服务器组，并移出该ALB服务器组内的ECS实例时，伸缩活动的ID。仅当`ForceDetach`取值为`true`时，返回该参数。 |

## 示例

请求示例

```
http(s)://ess.aliyuncs.com/?Action=DetachAlbServerGroups
&AlbServerGroup.1.AlbServerGroupId=sgp-ddwb0y0g6y9bjm****
&AlbServerGroup.1.Port=22
&RegionId=cn-hangzhou
&ScalingGroupId=asg-bp18p2yfxow2dloq****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DetachAlbServerGroups>  
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <ScalingActivityId>asa-2ze6wxj8vsohn6j9****</ScalingActivityId>
</DetachAlbServerGroups>
```

`JSON`格式

```
{
  "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
  "ScalingActivityId":"asa-2ze6wxj8vsohn6j9****"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ess)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|400

|AlbServerGroup.NotAttached

|The ALB ServerGroups are not attached to specific ScalingGroup.

|当前ALB服务器组未添加到伸缩组中。 |

