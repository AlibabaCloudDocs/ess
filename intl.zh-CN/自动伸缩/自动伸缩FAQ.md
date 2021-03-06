# 自动伸缩FAQ

本章节汇总了使用自动触发任务时的常见问题。

-   [我能设置周期性任务吗？](#section_3s6_peo_yf6)
-   [弹性伸缩中的报警任务触发条件有哪些？](#section_vmd_inq_1ug)
-   [如何设置报警任务触发条件？](#section_aah_1sk_dyk)
-   [如何使用报警任务删除通过弹性伸缩创建的实例？](#section_isj_t30_bbm)
-   [弹性伸缩是否可以根据云监控中的自定义报警项进行动态伸缩？](#section_1ag_12s_rjg)
-   [报警任务和定时任务之间有执行优先级吗？](#section_kql_ahe_ij5)
-   [弹性伸缩支持自动伸缩数据盘吗？](#section_1gg_n38_ldi)

## 我能设置周期性任务吗？

可以，详细信息请参见[创建定时任务](/intl.zh-CN/自动伸缩/定时任务/创建定时任务.md)。

## 弹性伸缩中的报警任务触发条件有哪些？

报警任务可以关联CPU、内存利用率、系统平均负载、内网出入流量等监控项统计信息，自动增加或减少ECS实例。

## 如何设置报警任务触发条件？

在使用报警任务之前，您需要在ECS实例中安装新版本的云监控Agent，具体操作请参见[云监控Java版本插件安装]()。

创建报警任务时，您需要根据实际业务情况选择使用的触发条件，具体操作请参见[创建报警任务](/intl.zh-CN/自动伸缩/报警任务/创建报警任务.md)。

## 如何使用报警任务删除通过弹性伸缩创建的实例？

在创建报警任务时选择删除实例的报警触发规则即可，具体操作请参见[创建伸缩规则](/intl.zh-CN/伸缩组/伸缩规则/创建伸缩规则.md)和[创建报警任务](/intl.zh-CN/自动伸缩/报警任务/创建报警任务.md)。

## 弹性伸缩是否可以根据云监控中的自定义报警项进行动态伸缩？

可以，详细信息请参见[自定义监控报警任务](/intl.zh-CN/自动伸缩/报警任务/自定义监控报警任务.md)。

## 报警任务和定时任务之间有执行优先级吗？

报警任务和定时任务不会同时触发，而且任务间相互独立，没有相对优先级。

如果报警任务失败，但仍然满足报警任务触发条件，待当前伸缩活动结束后报警任务仍会被执行。

您可以为定时任务设置重试时间，避免被拒绝执行后无法再次触发，详细操作请参见[创建定时任务](/intl.zh-CN/自动伸缩/定时任务/创建定时任务.md)。

## 弹性伸缩支持自动伸缩数据盘吗？

不支持。弹性伸缩只支持自动增加或减少伸缩组内ECS实例的数量，不支持自动提升或降低单台ECS实例的数据盘数量、大小等配置。

