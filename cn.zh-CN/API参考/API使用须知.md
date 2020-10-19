# API使用须知

为保证正常调用弹性伸缩OpenAPI，请在开始调用弹性伸缩OpenAPI前阅读本文所述事项。

## 权限要求

在调用弹性伸缩OpenAPI之前，您必须开通弹性伸缩服务，并将OpenAPI调用权限授予弹性伸缩，具体授权操作请参见[管理弹性伸缩服务关联角色](/cn.zh-CN/快速入门/管理弹性伸缩服务关联角色.md)。

## 未授权异常

弹性伸缩借助阿里云RAM（Resource Access Management）服务，通过ECS OpenAPI为您伸缩ECS实例资源。如果不符合条件，将出现下列异常。

|HttpCode|错误码|错误信息|描述|
|:-------|:--|:---|--|
|403|Forbidden.Unsubscribed|Do not have permission to access this API.|您未开通弹性伸缩服务，无权调用该API接口。|
|403|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|您未向弹性伸缩授予完整的OpenAPI接口权限。|

