# 伸缩组内配置负载均衡实例和RDS实例的FAQ {#concept_38560_zh .concept}

## 为什么选择负载均衡实例？ {#section_h2t_mhk_sfb .section}

伸缩组内配置负载均衡实例有利于扩展应用的服务能力和增强应用的可用性。

## 伸缩组如何使用负载均衡实例？ {#section_w5w_4hk_sfb .section}

如果创建伸缩组时添加了负载均衡实例，伸缩组会自动将加入伸缩组的云服务器ECS实例添加到该负载均衡实例中。一台负载均衡实例可以加入多个伸缩组，加入负载均衡实例的ECS实例权重默认是50。更多详情，请参见[添加默认服务器](../../../../cn.zh-CN/后端服务器/默认服务器组/添加默认服务器.md#)。

## 为什么选择RDS实例？ {#section_ddf_rhk_sfb .section}

伸缩组内配置RDS实例可以增强数据的安全性和可靠性，根据自定义的备份策略可以防止数据丢失和误删除。

## 伸缩组如何使用RDS实例？ {#section_lbc_thk_sfb .section}

如果创建伸缩组时添加了RDS实例，伸缩组会自动将加入伸缩组的ECS实例的内网IP添加到指定的RDS实例的访问白名单中，允许ECS实例内网通信。一台RDS实例可以加入多个伸缩组。更多详情，请参见[设置白名单](../../../../cn.zh-CN/用户指南/数据安全性/设置白名单.md#)。

如问题还未解决，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm)。

