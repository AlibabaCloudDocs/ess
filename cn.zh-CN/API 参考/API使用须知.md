# API使用须知 {#concept_25925_zh .concept}

在调用弹性伸缩 OpenAPI 之前，需要在阿里云官网先开通弹性伸缩服务，并在弹性伸缩控制台将用户的 OpenAPI 权限授权予弹性伸缩。

具体操作请参见 [操作资源](../../../../../cn.zh-CN//授权管理/操作资源.md#)。

## 前提条件 {#section_bsy_hk2_sfb .section}

在调用弹性伸缩 OpenAPI 之前，需要在阿里云官网先开通弹性伸缩服务，并在弹性伸缩控制台将用户的 OpenAPI 权限授权予弹性伸缩。具体操作请参见 [操作资源](../../../../../cn.zh-CN//授权管理/操作资源.md#)。

## 未授权异常 {#section_ccb_zn2_sfb .section}

弹性伸缩借助阿里云的 RAM（Resource Access Management）服务，通过 ECS OpenAPI 代替用户弹性伸缩 ECS 实例资源。如果不符合条件，将出现下列异常。

|HttpCode|错误码|错误信息|描述|
|:-------|:--|:---|--|
|403|Forbidden.Unsubscribed|Do not have permission to access this API.|用户未开通弹性伸缩，无权调用该 API。|
|403|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|用户并未向弹性伸缩完整授权 Open API 接口。|

