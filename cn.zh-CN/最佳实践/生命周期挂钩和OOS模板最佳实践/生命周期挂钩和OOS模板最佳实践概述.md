# 生命周期挂钩和OOS模板最佳实践概述

弹性伸缩的生命周期挂钩功能支持选择OOS模板作为通知方式，在挂起实例的同时执行指定的OOS模板中定义的运维操作，实现自动化运维。

## 生命周期挂钩

触发伸缩活动后，弹性伸缩会自动完成扩缩容流程，期间ECS实例的服务状态变化请参见[伸缩组内ECS实例的生命周期](/cn.zh-CN/实例管理/ECS实例/伸缩组内ECS实例的生命周期.md)。

通过生命周期挂钩，您能够在扩缩容流程中挂起ECS实例，执行自定义操作后再使用或者释放ECS实例。例如，在扩容时为ECS实例绑定辅助弹性网卡、将ECS实例添加至Redis实例白名单，在缩容时拷贝日志、清理数据等。

弹性伸缩还支持在挂起ECS实例的同时发送通知，自动执行OOS模板中定义的运维操作。

## OOS模板

运维编排服务（OOS）是阿里云提供的云上自动化运维服务，能够自动化管理和执行任务。您可以通过模板定义执行任务、执行顺序、执行输入和输出，然后执行模板完成一组运维操作。更多说明，请参见[什么是运维编排服务](https://help.aliyun.com/document_detail/120556.html)。

使用OOS模板响应生命周期挂钩通知具有以下优点：

-   OOS模板是运维操作的集合，能够实现更复杂的运维流程。
-   生命周期挂钩通知直接触发运维动作，无需手动解析通知内容。
-   提供公共模板，您无需关心具体实现即可一键完成常用运维操作，更多说明请参见[公共模板](https://help.aliyun.com/document_detail/123171.html)。
-   支持自定义模板，具体操作请参见[创建模板](https://help.aliyun.com/document_detail/120695.html)。

## 自动化运维流程

下图为您展示了通过生命周期挂钩和OOS模板实现自动化运维的流程。

![结合使用](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1394129951/p134069.png)

流程说明如下：

1.  ECS实例被生命周期挂钩挂起，进入挂起中状态。
2.  弹性伸缩自动发送通知，触发执行OOS模板中定义的运维操作。
3.  根据执行结果完成流程：
    -   运维操作执行成功，结束挂起状态并继续伸缩活动，扩容时继续完成扩容流程且ECS实例加入伸缩组，缩容时继续完成缩容流程且ECS实例被移出伸缩组。
    -   运维操作执行失败，结束挂起状态并结束伸缩活动，扩容时ECS实例被释放，缩容时无特殊影响，ECS实例仍会被移出伸缩组。

## 运维实践

本运维实践中为您介绍下表所述OOS公共模板的用法。

|公共模版名称|适用的伸缩活动类型|说明|相关链接|
|------|---------|--|----|
|ACS-ESS-LifeCycleApplyAutoSnapshotPolicy|弹性扩张活动|使用生命周期挂钩应用自动快照策略到磁盘。|[为ECS实例自动应用自动快照策略](/cn.zh-CN/最佳实践/生命周期挂钩和OOS模板最佳实践/为ECS实例自动应用自动快照策略.md)|
|ACS-ESS-LifeCycleRunCommand|弹性扩张活动、弹性收缩活动|使用生命周期挂钩到ECS实例中执行命令。|[在ECS实例中自动执行脚本](/cn.zh-CN/最佳实践/生命周期挂钩和OOS模板最佳实践/在ECS实例中自动执行脚本.md)|
|ACS-ESS-LifeCycleModifyPolarDBIPWhitelist|弹性扩张活动、弹性收缩活动|使用生命周期挂钩设置PolarDB集群的IP白名单。|[将ECS实例自动加入和移出PolarDB集群白名单](/cn.zh-CN/最佳实践/生命周期挂钩和OOS模板最佳实践/将ECS实例自动加入和移出PolarDB集群白名单.md)|
|ACS-ESS-LifeCycleModifyRedisIPWhitelist|弹性扩张活动、弹性收缩活动|使用生命周期挂钩设置Redis实例的IP白名单。|[将ECS实例自动加入和移出Redis实例白名单](/cn.zh-CN/最佳实践/生命周期挂钩和OOS模板最佳实践/将ECS实例自动加入和移出Redis实例白名单.md)|
|ACS-ESS-LifeCycleModifyMongoDBIPWhitelist|弹性扩张活动、弹性收缩活动|使用生命周期挂钩设置MongoDB实例的IP白名单。|[将ECS实例自动加入和移出MongoDB实例白名单](/cn.zh-CN/最佳实践/生命周期挂钩和OOS模板最佳实践/将ECS实例自动加入和移出MongoDB实例白名单.md)|
|ACS-ESS-LifeCycleModifyAnalyticDBIPWhitelist|弹性扩张活动、弹性收缩活动|使用生命周期挂钩设置AnalyticDB集群的IP白名单。|[将ECS实例自动加入和移出AnalyticDB集群白名单](/cn.zh-CN/最佳实践/生命周期挂钩和OOS模板最佳实践/将ECS实例自动加入和移出AnalyticDB集群白名单.md)|
|ACS-ESS-LifeCycleAttachNASFileSystemToInstance|弹性扩张活动|使用生命周期挂钩挂载NAS文件系统到ECS实例。|[为ECS实例挂载NAS文件系统](/cn.zh-CN/最佳实践/生命周期挂钩和OOS模板最佳实践/为ECS实例挂载NAS文件系统.md)|
|ACS-ESS-LifeCycleCreateNetworkInterfaceAndEipAndAttachToInstance|弹性扩张活动|使用生命周期挂钩创建辅助弹性网卡和EIP，并将其绑定到ECS实例。|[为ECS实例自动绑定有EIP的辅助弹性网卡](/cn.zh-CN/最佳实践/生命周期挂钩和OOS模板最佳实践/为ECS实例自动绑定有EIP的辅助弹性网卡.md)|
|ACS-ESS-LifeCycleDetachNetworkInterfaceAndDeleteEip|弹性收缩活动|使用生命周期挂钩为ECS实例解绑和释放辅助弹性网卡和EIP。|[为ECS实例自动释放有EIP的辅助弹性网卡](/cn.zh-CN/最佳实践/生命周期挂钩和OOS模板最佳实践/为ECS实例自动释放有EIP的辅助弹性网卡.md)|
|ACS-ESS-LifeCycleAllocateEipAddressAndAttachToInstance|弹性扩张活动|使用生命周期挂钩创建EIP，并将其绑定到ECS实例。|[为ECS实例自动绑定EIP](/cn.zh-CN/最佳实践/生命周期挂钩和OOS模板最佳实践/为ECS实例自动绑定EIP.md)|
|ACS-ESS-LifeCycleReleaseEipAddressFromInstance|弹性收缩活动|使用生命周期挂钩为ECS实例解绑和释放EIP。|[为ECS实例自动释放EIP]()|

