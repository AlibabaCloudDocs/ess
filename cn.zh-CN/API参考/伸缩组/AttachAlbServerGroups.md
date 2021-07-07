# AttachAlbServerGroups

调用AttachAlbServerGroups向伸缩组添加一个或多个ALB服务器组。

## 接口说明

向伸缩组添加ALB服务器组时，需要满足以下条件：

-   伸缩组的网络类型必须为VPC，且与ALB服务器组处于同一VPC。
-   ALB服务器组必须处于可用状态。
-   伸缩组支持添加的ALB服务组数量有限，不支持添加超出数量的ALB服务器组。如需查看或手动申请提升配额值，请前往[配额中心](https://quotas.console.aliyun.com/products/ess/quotas)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=AttachAlbServerGroups&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|伸缩组所属地域的ID，如cn-hangzhou、cn-shanghai。更多信息，请参见[地域和可用区](~~40654~~)。 |
|ScalingGroupId|String|是|asg-bp18p2yfxow2dloq\*\*\*\*|伸缩组的ID。 |
|AlbServerGroup.N.AlbServerGroupId|String|是|sgp-ddwb0y0g6y9bjm\*\*\*\*|ALB服务器组的ID。

 N为ALB服务器组的编号。一个伸缩组支持关联的ALB服务器组数量有限，如需查看或手动申请提升配额值，请前往[配额中心](https://quotas.console.aliyun.com/products/ess/quotas)。 |
|AlbServerGroup.N.Port|Integer|是|22|弹性伸缩将ECS实例添加到ALB服务器组后，ECS实例使用的端口号，取值范围：1~65535。

 N为ALB服务器组的编号。

 **说明：** 如果N相同，Port不同，系统会默认向伸缩组关联多个不同Port的该ALB服务器组。 |
|AlbServerGroup.N.Weight|Integer|是|100|弹性伸缩将ECS实例添加到ALB服务器组后，ECS实例作为后端服务器的权重。权重越高，ECS实例将被分配到越多的访问请求。如果权重为0，则ECS实例不会收到访问请求。取值范围：0~100。

 N为ALB服务器组的编号。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多信息，请参见[如何保证幂等性](~~25965~~)。 |
|ForceAttach|Boolean|否|false|是否将当前伸缩组内的ECS实例添加到新增的ALB服务器组。

 -   true：添加，并返回`ScalingActivityId`，您可以通过查看该伸缩活动ID来确定已有实例是否添加成功。
-   false：不添加。

 默认值：false |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|ScalingActivityId|String|asa-2ze6wxj8vsohn6j9\*\*\*\*|添加ALB服务器组，并将伸缩组内的ECS实例添加到该ALB服务器组时，伸缩活动的ID。仅当`ForceAttach`取值为`true`时，返回该参数。 |

## 示例

请求示例

```
http(s)://ess.aliyuncs.com/?Action=AttachAlbServerGroups
&RegionId=cn-hangzhou
&ScalingGroupId=asg-bp18p2yfxow2dloq****
&AlbServerGroup.1.AlbServerGroupId=sgp-ddwb0y0g6y9bjm****
&AlbServerGroup.1.Port=22
&AlbServerGroup.1.Weight=100
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<AttachAlbServerGroupsResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <ScalingActivityId>asa-2ze6wxj8vsohn6j9****</ScalingActivityId>
</AttachAlbServerGroupsResponse>
```

`JSON`格式

```
{
        "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
        "ScalingActivityId": "asa-2ze6wxj8vsohn6j9****"
    }
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|400

|AlbServerGroup.NotExist

|The ServerGroup "%s" do\(es\) not exist.

|账号下不存在指定的ALB服务器组。 |
|400

|AlbServerGroup.AlreadyAttached

|The ALB ServerGroups are already attached.

|当前ALB服务器组已经添加到伸缩组中。 |

