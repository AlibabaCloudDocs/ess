# 伸缩组FAQ

本文汇总了使用伸缩组时的常见问题。

-   伸缩组设置FAQ
    -   [弹性伸缩服务一定要搭配负载均衡、云监控、RDS才能使用吗？](#section_s08_me8_us6)
    -   [一个伸缩组最多可以添加多少台ECS实例？](#section_012_swz_wv6)
    -   [我能添加已经创建的ECS实例吗？](#section_5pc_nm8_9h7)
    -   [我能添加已经创建的包年包月ECS实例吗？](#section_dxu_nq9_etn)
    -   [ECS实例是否可以加入到多个伸缩组中？](#section_v7t_w23_hr0)
    -   [我能控制如何移出ECS实例吗？](#section_w54_0xc_xg1)
    -   [停用伸缩组后，会释放已经自动添加到伸缩组的ECS实例吗？](#section_z1p_h7c_abl)
-   伸缩配置FAQ
    -   [一个伸缩组可以添加多种规格的ECS实例吗？](#section_nok_06f_7lk)
    -   [在伸缩组内可以配置8核或者16核的ECS实例吗？](#section_yac_v6f_yyk)
    -   [使用弹性伸缩自动创建ECS实例时，如何指定数据盘的容量？](#section_ipn_53q_9d6)
    -   [如果弹性伸缩动态调整ECS实例的数量，如何保证使用镜像市场镜像时能正常弹出ECS实例？](#section_0af_02b_s62)
    -   [镜像市场镜像是否支持批量购买？](#section_0bk_5ek_5hj)
    -   [如果镜像市场已不存在之前使用的镜像，如何保证使用该镜像正常弹出ECS实例？](#section_uaf_q73_ltq)
    -   [为什么伸缩组创建ECS实例时出现云市场镜像不可用报错？](#section_6tm_x8s_o62)
    -   [1个product code能否支持不同地域的镜像？](#section_h4w_acv_igz)
    -   [购买了100个product code同样值的镜像，是否支持在所有的地域可用？](#section_83p_ke7_gfu)
-   伸缩活动FAQ
    -   [提交工单时，我需要提供哪些弹性伸缩信息？](#section_xrn_c52_zke)
    -   [为什么伸缩组创建ECS实例时出现资源报错？](#section_c99_9lu_isv)
    -   [如何避免单实例规格库存不足导致扩容失败？](#section_brg_xys_xgb)
    -   [伸缩组内ECS实例开启了释放保护，为什么仍然被自动释放了？](#section_ty9_oli_yc4)
    -   [如何保证手动添加的ECS实例不会被移出伸缩组？](#section_7ji_np8_vy4)
    -   [伸缩组自动增加或者减少ECS实例后，弹性伸缩会自动从RDS实例或者Memcache实例的IP白名单中添加或者移除ECS实例吗？](#section_p3y_qln_5h0)
    -   [怎样阻止伸缩组内手动添加的ECS实例被自动移除？](#section_wwv_wqt_7er)
    -   [弹性伸缩是否能够自动升降ECS的CPU、内存和带宽？](#section_k5y_xa2_ykd)
    -   [从伸缩组内移出并释放ECS实例后，ECS实例的数据会保留吗？](#section_t03_8tt_d7y)
    -   [如何删除通过弹性伸缩创建的实例？](#section_0dg_bhr_74x)
    -   [弹性伸缩自动创建多台ECS实例时，部分创建失败时如何处理？](#section_4hk_err_pwe)
-   伸缩组内ECS实例FAQ
    -   [弹性伸缩自动创建的实例如何查看密码并进行登录？](#section_3db_mu8_l7z)
    -   [弹性伸缩自动创建的ECS实例的密码为什么和我自定义镜像中的密码不一致？](#section_leh_e9v_f9z)
    -   [怎么将数据同步到伸缩组内的ECS实例？](#section_pwt_1d0_d2i)
    -   [为什么弹出的实例中/etc/hosts新增的127.0.0.1被重置清除了？](#section_gkh_sb6_dxh)
-   关联负载均衡实例FAQ
    -   [伸缩组关联负载均衡实例有什么作用？](#section_z3p_c1m_gwo)
    -   [伸缩组如何使用负载均衡实例？](#section_w8e_ln5_36d)
    -   [弹性伸缩创建ECS实例后，新实例会自动加入到负载均衡实例吗？](#section_032_8qb_jdq)
    -   [弹性伸缩新创建的ECS实例是否可以添加至多台负载均衡实例？](#section_ix6_1fd_tfx)
    -   [我可以修改伸缩组内ECS实例在负载均衡实例中的权重吗？](#section_kng_0nf_mh2)
    -   [我的负载均衡实例为公网类型，创建伸缩配置时ECS实例是否需要配置公网带宽？](#section_stl_1q2_qt9)
    -   [为什么创建伸缩组时出现负载均衡实例健康检查报错？](#section_v4m_d6k_9zp)
    -   [如何判断新创建的ECS实例可用于处理访问流量？](#section_zx2_7xq_n1e)
    -   [为什么负载均衡的7层HTTP监听超时超过60秒？](#section_vj3_piv_qog)
-   关联RDS实例FAQ
    -   [伸缩组关联RDS实例有什么作用？](#section_zjm_20i_w3g)
    -   [伸缩组如何使用RDS实例？](#section_w0t_tvt_ooi)

## 弹性伸缩服务一定要搭配负载均衡、云监控、RDS才能使用吗？

不是。弹性伸缩是开放灵活的平台，您可以不搭配负载均衡、云监控、RDS，但是搭配这些产品可以增强弹性伸缩的服务能力。您可以：

-   搭配负载均衡一起部署，详细信息请参见[什么是负载均衡](/cn.zh-CN/产品简介/什么是负载均衡.md)。
-   搭配云数据库RDS一起部署，详细信息请参见[什么是云数据库RDS](/cn.zh-CN/云数据库 RDS 简介/什么是云数据库RDS.md)。
-   通过云监控触发弹性扩张和收缩活动，详细信息请参见[报警任务概述](/cn.zh-CN/自动伸缩/报警任务/报警任务概述.md)。

## 一个伸缩组最多可以添加多少台ECS实例？

弹性伸缩相关的数量限制，请参见[使用限制](/cn.zh-CN/产品简介/使用限制.md)。

## 我能添加已经创建的ECS实例吗？

能。但待添加的ECS实例需要满足以下条件：

-   ECS实例必须与伸缩组在同一个地域。更多信息，请参见[地域和可用区](https://help.aliyun.com/document_detail/40654.html)。
-   ECS实例必须处于**运行中**状态，详细信息请参见[实例生命周期介绍](/cn.zh-CN/实例/实例生命周期介绍.md)。
-   ECS实例不能已添加到其它伸缩组中。

## 我能添加已经创建的包年包月ECS实例吗？

能。弹性伸缩支持自动创建按量付费或者抢占式实例，同时支持添加已经创建的包年包月和按量付费实例。

## ECS实例是否可以加入到多个伸缩组中？

不支持。

## 我能控制如何移出ECS实例吗？

能。您可以为伸缩组配置移出策略，移出策略支持两级，可以自动筛选最早伸缩配置对应的实例、最早创建的实例或最新创建的实例，详细信息请参见[创建伸缩组](/cn.zh-CN/伸缩组/伸缩组/创建伸缩组.md)。

## 停用伸缩组后，会释放已经自动添加到伸缩组的ECS实例吗？

在控制台或者调用接口停用伸缩组后，不会自动释放伸缩组内的ECS实例，详细信息请参见[停用伸缩组](/cn.zh-CN/伸缩组/伸缩组/停用伸缩组.md)。

## 一个伸缩组可以添加多种规格的ECS实例吗？

可以。一个伸缩配置支持多选ECS实例规格，弹性扩张的成功率更高，但存在上限，详细信息请参见[使用限制](/cn.zh-CN/产品简介/使用限制.md)。

## 在伸缩组内可以配置8核或者16核的ECS实例吗？

可以。如果当前可选实例规格不能满足需求，您可以[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm)申请使用更多ECS实例规格。

## 使用弹性伸缩自动创建ECS实例时，如何指定数据盘的容量？

创建伸缩配置时，在存储中指定数据盘的容量即可，具体操作请参见[创建伸缩配置](/cn.zh-CN/伸缩组/组内实例配置信息来源/创建伸缩配置.md)。

## 如果弹性伸缩动态调整ECS实例的数量，如何保证使用镜像市场镜像时能正常弹出ECS实例？

如果您需要弹出N台同类型的镜像，您需要提前购买N个镜像市场的镜像。

## 镜像市场镜像是否支持批量购买？

暂不支持批量购买。

## 如果镜像市场已不存在之前使用的镜像，如何保证使用该镜像正常弹出ECS实例？

建议您选择镜像市场中的其它可用镜像。

## 为什么伸缩组创建ECS实例时出现云市场镜像不可用报错？

如果弹出以下报错，说明伸缩配置中使用了镜像市场中的第三方镜像。

```
Fail to create Instance into scaling group("The specified image is from the image market. You have not bought it or your quota has been exceeded.").
```

弹性伸缩服务不能自动创建镜像市场的第三方镜像，您需要先到[云市场](https://market.aliyun.com/software)购买镜像，购买成功后再回到弹性伸缩服务中创建ECS实例即可。

## 1个product code能否支持不同地域的镜像？

支持，前提是该地域已经支持该商品镜像。

## 购买了100个product code同样值的镜像，是否支持在所有的地域可用？

目前镜像市场的镜像已经具备地域属性，请您购买需要使用的地域镜像。

## 提交工单时，我需要提供哪些弹性伸缩信息？

[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm)时，您可以提供伸缩组的活动ID（ScalingActivityId）或者相关日志，便于快速排查。

查看伸缩活动的操作，请参见[查看伸缩活动详情](/cn.zh-CN/监控/伸缩活动/查看伸缩活动详情.md)。

## 为什么伸缩组创建ECS实例时出现资源报错？

如果弹出以下报错，可能是因为ECS资源不足，建议您更换可用区再试。

```
Fail to create Instance into scaling group("The resource is out of usage".).
```

```
Fail to create Instance into scaling group(The specified region is in resource control, please try later.").
```

## 如何避免单实例规格库存不足导致扩容失败？

建议您在创建伸缩组时设置多可用区（选择不同可用区下的虚拟交换机即可），并在创建伸缩配置时选择多实例规格，当某个ECS实例规格在某个可用区没有库存时，弹性伸缩服务会自动切换到有库存的实例规格及可用区进行扩容，具体操作请参见[创建伸缩组](/cn.zh-CN/伸缩组/伸缩组/创建伸缩组.md)和[创建伸缩配置](/cn.zh-CN/伸缩组/组内实例配置信息来源/创建伸缩配置.md)。

## 伸缩组内ECS实例开启了释放保护，为什么仍然被自动释放了？

在弹性伸缩自动创建一台ECS实例后，如果您在ECS控制台的实例列表页面或者调用[ModifyInstanceAttribute](/cn.zh-CN/API参考/实例/ModifyInstanceAttribute.md)为ECS实例开启了释放保护，并不能阻止弹性伸缩自动释放实例。

您可以将伸缩组内的ECS实例转为保护状态，避免被自动释放，具体操作请参见[实例转为保护状态](/cn.zh-CN/实例管理/ECS实例/实例转为保护状态.md)。

## 如何保证手动添加的ECS实例不会被移出伸缩组？

您可以将伸缩组内的ECS实例转为保护状态，避免被自动释放，具体操作请参见[实例转为保护状态](/cn.zh-CN/实例管理/ECS实例/实例转为保护状态.md)。

## 伸缩组自动增加或者减少ECS实例后，弹性伸缩会自动从RDS实例或者Memcache实例的IP白名单中添加或者移除ECS实例吗？

会从RDS实例的IP白名单中添加或者移除ECS实例，不会从Memcache实例的IP白名单中添加或者移除ECS实例。

## 怎样阻止伸缩组内手动添加的ECS实例被自动移除？

假设您需要保证100台手动添加的ECS实例不会被自动移出伸缩组，请做如下配置：

-   将最小实例数设置为大于等于100。
-   将一级移出策略设置为**最早伸缩配置对应的实例**。

由于您手动添加的ECS实例不是通过伸缩配置创建的，所以这些ECS实例不会遵循任何伸缩配置。伸缩组会优先挑选、移出并释放自动创建的ECS实例，当伸缩组内自动创建的ECS实例被全部移除后，才会挑选、移除并保留您手动添加的ECS实例。

**说明：** 如果您想阻止伸缩组自动移除您手动添加的ECS实例，请不要停止ECS实例，否则弹性伸缩会认定该ECS实例不健康，并将不健康的ECS实例自动移出伸缩组。

## 弹性伸缩是否能够自动升降ECS的CPU、内存和带宽？

弹性伸缩根据您设置的策略自动伸缩计算资源，能够在业务增长时自动增加ECS实例，并在业务下降时自动减少ECS实例。但弹性伸缩不支持纵向扩张，即无法自动升降ECS的CPU、内存和带宽。

## 从伸缩组内移出并释放ECS实例后，ECS实例的数据会保留吗？

不会。弹性伸缩会自动释放ECS实例，您需要确保伸缩组内的ECS实例没有保存应用的状态信息或者重要数据，例如，会话记录（session）、数据库和日志等。如果您的应用需要保存状态信息，建议将状态信息保存到独立的状态服务器（例如ECS）、数据库（例如RDS）或者日志服务（例如日志服务）。

## 如何删除通过弹性伸缩创建的实例？

您可以在伸缩组的ECS实例列表中删除自动创建的ECS实例，具体操作请参见[手动移出ECS实例](/cn.zh-CN/实例管理/ECS实例/手动移出ECS实例.md)。

## 弹性伸缩自动创建多台ECS实例时，部分创建失败时如何处理？

弹性伸缩会保持ECS实例级事务的完整性，而非伸缩活动级事务的完整性。您可以在控制台查看伸缩活动的完成情况，具体操作请参见[查看伸缩活动详情](/cn.zh-CN/监控/伸缩活动/查看伸缩活动详情.md)。

例如，需要自动创建20台ECS实例，19台创建成功，1台创建失败，则创建成功的19台ECS实例加入伸缩组，不会重新尝试创建剩余的1台ECS实例，伸缩活动完成，但是状态显示为**警告**。

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1364621061/p64066.png)

## 弹性伸缩自动创建的实例如何查看密码并进行登录？

由于伸缩配置不支持设置统一的自定义密码，如果使用Linux操作系统，推荐您为伸缩配置指定SSH密钥对。

如果您不使用SSH密钥对登录实例，则需要在控制台重置密码后（重启后生效）才能登录。

## 弹性伸缩自动创建的ECS实例的密码为什么和我自定义镜像中的密码不一致？

创建ECS实例时，实例登录密码不使用自定义镜像中的密码。为了保证安全性，推荐您为伸缩配置指定SSH密钥对。

如果您不使用SSH密钥对登录实例，则需要在控制台重置密码后（重启后生效）才能登录。

## 怎么将数据同步到伸缩组内的ECS实例？

创建伸缩配置时，您可以通过ECS自定义镜像模板来创建实例。在ECS实例运行过程中，如果需要做系统内部数据同步，建议您自定义安装rsync进行同步。

## 为什么弹出的实例中/etc/hosts新增的127.0.0.1被重置清除了？

如果您在修改/etc/hosts后创建自定义镜像，通过该自定义镜像自动创建ECS实例时，会还原到系统默认设置，所以会被清除。如果需要保留/etc/hosts设置，您可以尝试在rc.local中添加相关脚本代码，检测/etc/hosts中是否存在相关信息，若不存在则自动添加。

## 伸缩组关联负载均衡实例有什么作用？

负载均衡实例可以根据转发策略将访问流量分发至ECS实例，为伸缩组关联负载均衡实例有利于扩展应用的服务能力和增强应用的可用性。更多负载均衡介绍，请参见[什么是负载均衡](/cn.zh-CN/产品简介/什么是负载均衡.md)。

## 伸缩组如何使用负载均衡实例？

如果创建伸缩组时关联了负载均衡实例，伸缩组会自动将加入伸缩组的云服务器ECS实例添加到该负载均衡实例中。一台负载均衡实例可以关联至多个伸缩组，加入负载均衡实例的ECS实例权重默认是50。更多负载均衡后端服务器介绍，请参见[添加ECS实例作为默认服务器](/cn.zh-CN/用户指南/后端服务器/默认服务器组/添加默认服务器.md)。

## 弹性伸缩创建ECS实例后，新实例会自动加入到负载均衡实例吗？

会，但是您需要预先为伸缩组关联负载均衡实例。

## 弹性伸缩新创建的ECS实例是否可以添加至多台负载均衡实例？

可以。伸缩组支持关联多台负载均衡实例，但存在上限，详细信息请参见[使用限制](/cn.zh-CN/产品简介/使用限制.md)。

如果需要关联更多负载均衡实例，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm)。

## 我可以修改伸缩组内ECS实例在负载均衡实例中的权重吗？

可以，具体操作请参见[编辑后端服务器的权重](/cn.zh-CN/用户指南/后端服务器/默认服务器组/编辑后端服务器的权重.md)。

负载均衡实例中后端服务器的权重分配按比例计算，而非数字。假设您有两台ECS实例，50和50的权重效果100和100是一致的，比例均为1:1。一般情况下，弹性伸缩组后端ECS实例所承载的业务和ECS实例的规格应该都是一样的。弹性伸缩服务中配置的负载均衡默认设置ECS实例权重均为50。

## 我的负载均衡实例为公网类型，创建伸缩配置时ECS实例是否需要配置公网带宽？

ECS实例可以不配置公网带宽。但为了方便管理ECS实例，建议您在创建伸缩配置时选择至少1Mbit/s公网带宽。

## 为什么创建伸缩组时出现负载均衡实例健康检查报错？

如果弹出以下报错，说明该负载均衡实例未开启健康检查。

```
The current health check type of load balancer "xxxx" does not support this action.
```

关联至伸缩组的负载均衡实例必须已经开启健康检查，具体操作请参见[配置健康检查](/cn.zh-CN/用户指南/健康检查/配置健康检查.md)。

## 如何判断新创建的ECS实例可用于处理访问流量？

如果弹性伸缩在伸缩组里配置了负载均衡，负载均衡检查您后端的ECS端口正常之后，才会将请求转发给新的实例。

## 为什么负载均衡的7层HTTP监听超时超过60秒？

问题现象：负载均衡响应HTTP转发请求时，单次HTTP监听的超时时间大约为60秒。然而，当负载均衡实例上配置了多台ECS实例时，ECS实例配置的超时时间都大于60秒，或者直接返回504错误。

问题原因：负载均衡的HTTP监听超时时间是保证请求在允许的时间内能返回的最后一条防线，总超时时间与配置的ECS实例数量有关。

在负载均衡实例上配置了多台ECS实例时，如果第一台ECS实例访问超时，会自动轮询第二台ECS实例，如果第二台ECS实例仍然超时，则轮询第三台ECS实例，直至所有ECS实例轮询完毕。假设一台负载均衡实例上配置了3台ECS实例，则实际发生的HTTP请求超时时间会变成大约180秒。

另外，不排除其他服务会限制负载均衡超时时间设置。建议您避免依赖负载均衡监听超时设置，而是直接在ECS实例部署的应用上设置监听超时时间。

## 伸缩组关联RDS实例有什么作用？

RDS是一种稳定可靠、可弹性伸缩的在线数据库服务，为伸缩组关联RDS实例可以增强数据的安全性和可靠性，根据自定义的备份策略防止数据丢失和误删除。更多RDS介绍，请参见[什么是云数据库RDS](/cn.zh-CN/云数据库 RDS 简介/什么是云数据库RDS.md)。

## 伸缩组如何使用RDS实例？

如果创建伸缩组时添加了RDS实例，ECS实例加入伸缩组后，伸缩组会自动该ECS实例的内网IP添加到RDS实例的访问白名单中，允许ECS实例内网通信。伸缩组支持关联多台RDS实例。更多RDS实例白名单信息，请参见[设置白名单](/cn.zh-CN/RDS MySQL 数据库/快速入门/设置白名单.md)。

