# API使用须知 {#concept_25925_zh .concept}

为保证正常调用弹性伸缩OpenAPI，请在开始调用弹性伸缩OpenAPI前阅读本文所述事项。

## 权限要求 {#section_bsy_hk2_sfb .section}

在调用弹性伸缩OpenAPI之前，您需要在阿里云官网开通弹性伸缩服务，并在弹性伸缩控制台将OpenAPI权限授予弹性伸缩，具体授权操作请参见[使用RAM角色](../../../../cn.zh-CN/用户指南/角色/使用 RAM 角色.md#)。

## 未授权异常 {#section_ccb_zn2_sfb .section}

弹性伸缩借助阿里云RAM（Resource Access Management）服务，通过ECS OpenAPI为您伸缩ECS实例资源。如果不符合条件，将出现下列异常。

|HttpCode|错误码|错误信息|描述|
|:-------|:--|:---|--|
|403|Forbidden.Unsubscribed|Do not have permission to access this API.|您未开通弹性伸缩服务，无权调用该API接口。|
|403|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|您未向弹性伸缩授予完整的OpenAPI接口权限。|

