# API概览

弹性伸缩提供了丰富的API接口。本文列出了所有可调用的API接口及相关描述，供您查阅。

## 伸缩组

|API|描述|
|---|--|
|[CreateScalingGroup](/cn.zh-CN/API参考/伸缩组/CreateScalingGroup.md)|调用CreateScalingGroup创建一个伸缩组。|
|[ModifyScalingGroup](/cn.zh-CN/API参考/伸缩组/ModifyScalingGroup.md)|调用ModifyScalingGroup修改一个伸缩组。|
|[EnableScalingGroup](/cn.zh-CN/API参考/伸缩组/EnableScalingGroup.md)|调用EnableScalingGroup启用一个伸缩组。|
|[DisableScalingGroup](/cn.zh-CN/API参考/伸缩组/DisableScalingGroup.md)|调用DisableScalingGroup停用一个伸缩组。|
|[SetGroupDeletionProtection](/cn.zh-CN/API参考/伸缩组/SetGroupDeletionProtection.md)|调用SetGroupDeletionProtection为伸缩组开启或关闭删除保护。|
|[DeleteScalingGroup](/cn.zh-CN/API参考/伸缩组/DeleteScalingGroup.md)|调用DeleteScalingGroup删除一个伸缩组。|
|[DescribeScalingGroups](/cn.zh-CN/API参考/伸缩组/DescribeScalingGroups.md)|调用DescribeScalingGroups查询伸缩组。|
|[DescribeScalingInstances](/cn.zh-CN/API参考/伸缩组/DescribeScalingInstances.md)|调用DescribeScalingInstances查询伸缩组内ECS实例的列表，并列出ECS实例的信息。|
|[DescribeScalingActivities](/cn.zh-CN/API参考/伸缩组/DescribeScalingActivities.md)|调用DescribeScalingActivities查询伸缩活动。|
|[DescribeScalingActivityDetail](/cn.zh-CN/API参考/伸缩组/DescribeScalingActivityDetail.md)|调用DescribeScalingActivityDetail查询一个伸缩活动的详细信息。|
|[AttachLoadBalancers](/cn.zh-CN/API参考/伸缩组/AttachLoadBalancers.md)|调用AttachLoadBalancers添加一个或多个负载均衡实例。|
|[DetachLoadBalancers](/cn.zh-CN/API参考/伸缩组/DetachLoadBalancers.md)|调用DetachLoadBalancers移除一个或多个负载均衡实例。|
|[AttachDBInstances](/cn.zh-CN/API参考/伸缩组/AttachDBInstances.md)|调用AttachDBInstances添加一个或多个RDS实例。|
|[DetachDBInstances](/cn.zh-CN/API参考/伸缩组/DetachDBInstances.md)|调用DetachDBInstances移除一个或多个RDS实例。|
|[AttachVServerGroups](/cn.zh-CN/API参考/伸缩组/AttachVServerGroups.md)|调用AttachVServerGroups添加负载均衡实例下的一个或者多个虚拟服务器组。|
|[DetachVServerGroups](/cn.zh-CN/API参考/伸缩组/DetachVServerGroups.md)|调用DetachVServerGroups移除一个或者多个虚拟服务器组。|
|[SuspendProcesses](/cn.zh-CN/API参考/伸缩组/SuspendProcesses.md)|调用SuspendProcesses暂停伸缩组中的指定流程。|
|[ResumeProcesses](/cn.zh-CN/API参考/伸缩组/ResumeProcesses.md)|调用ResumeProcesses恢复伸缩组中被暂停的流程。|

## 伸缩配置

|API|描述|
|---|--|
|[CreateScalingConfiguration](/cn.zh-CN/API参考/伸缩配置/CreateScalingConfiguration.md)|调用CreateScalingConfiguration创建一个伸缩配置。|
|[DescribeScalingConfigurations](/cn.zh-CN/API参考/伸缩配置/DescribeScalingConfigurations.md)|调用DescribeScalingConfigurations查询现有的伸缩配置。|
|[DeleteScalingConfiguration](/cn.zh-CN/API参考/伸缩配置/DeleteScalingConfiguration.md)|调用DeleteScalingConfiguration删除一个伸缩配置。|
|[ModifyScalingConfiguration](/cn.zh-CN/API参考/伸缩配置/ModifyScalingConfiguration.md)|调用ModifyScalingConfiguration修改一个伸缩配置。|

## 伸缩规则

|API|描述|
|---|--|
|[CreateScalingRule](/cn.zh-CN/API参考/伸缩规则/CreateScalingRule.md)|调用CreateScalingRule创建一条伸缩规则。|
|[ModifyScalingRule](/cn.zh-CN/API参考/伸缩规则/ModifyScalingRule.md)|调用ModifyScalingRule修改一条伸缩规则。|
|[DescribeScalingRules](/cn.zh-CN/API参考/伸缩规则/DescribeScalingRules.md)|调用DescribeScalingRules查询伸缩组下的伸缩规则，并列出伸缩规则的信息。|
|[DeleteScalingRule](/cn.zh-CN/API参考/伸缩规则/DeleteScalingRule.md)|调用DeleteScalingRule删除一条伸缩规则。|

## 触发任务

|API|描述|
|---|--|
|[ExecuteScalingRule](/cn.zh-CN/API参考/触发任务/ExecuteScalingRule.md)|调用ExecuteScalingRule执行一条伸缩规则。|
|[AttachInstances](/cn.zh-CN/API参考/触发任务/AttachInstances.md)|调用AttachInstances为伸缩组添加ECS实例。|
|[RemoveInstances](/cn.zh-CN/API参考/触发任务/RemoveInstances.md)|调用RemoveInstances从一个伸缩组里移出ECS实例。|
|[DetachInstances](/cn.zh-CN/API参考/触发任务/DetachInstances.md)|调用DetachInstances从一个伸缩组分离一台或多台ECS实例。|

## 定时任务

|API|描述|
|---|--|
|[CreateScheduledTask](/cn.zh-CN/API参考/定时任务/CreateScheduledTask.md)|调用CreateScheduledTask创建一个定时任务。|
|[ModifyScheduledTask](/cn.zh-CN/API参考/定时任务/ModifyScheduledTask.md)|调用ModifyScheduledTask修改一个定时任务的信息。|
|[DescribeScheduledTasks](/cn.zh-CN/API参考/定时任务/DescribeScheduledTasks.md)|调用DescribeScheduledTasks查询定时任务的信息。|
|[DeleteScheduledTask](/cn.zh-CN/API参考/定时任务/DeleteScheduledTask.md)|调用DeleteScheduledTask删除一个定时任务。|

## 报警任务

|API|描述|
|---|--|
|[CreateAlarm](/cn.zh-CN/API参考/报警任务/CreateAlarm.md)|调用CreateAlarm创建一个报警任务。|
|[DescribeAlarms](/cn.zh-CN/API参考/报警任务/DescribeAlarms.md)|调用DescribeAlarms查询报警任务的信息。|
|[ModifyAlarm](/cn.zh-CN/API参考/报警任务/ModifyAlarm.md)|调用ModifyAlarm修改一个报警任务。|
|[EnableAlarm](/cn.zh-CN/API参考/报警任务/EnableAlarm.md)|调用EnableAlarm启用一个报警任务。|
|[DisableAlarm](/cn.zh-CN/API参考/报警任务/DisableAlarm.md)|调用DisableAlarm停用一个报警任务。|
|[DeleteAlarm](/cn.zh-CN/API参考/报警任务/DeleteAlarm.md)|调用DeleteAlarm删除一个报警任务。|

## 生命周期挂钩

|API|描述|
|---|--|
|[CreateLifecycleHook](/cn.zh-CN/API参考/生命周期挂钩/CreateLifecycleHook.md)|调用CreateLifecycleHook为伸缩组创建一个或多个生命周期挂钩。|
|[ModifyLifecycleHook](/cn.zh-CN/API参考/生命周期挂钩/ModifyLifecycleHook.md)|调用ModifyLifecycleHook修改一个生命周期挂钩的信息。|
|[DescribeLifecycleHooks](/cn.zh-CN/API参考/生命周期挂钩/DescribeLifecycleHooks.md)|调用DescribeLifecycleHooks查询生命周期挂钩。|
|[RecordLifecycleActionHeartbeat](/cn.zh-CN/API参考/生命周期挂钩/RecordLifecycleActionHeartbeat.md)|调用RecordLifecycleActionHeartbeat延长一个生命周期挂钩触发后被挂起的ECS实例的等待时间。|
|[DescribeLifecycleActions](/cn.zh-CN/API参考/生命周期挂钩/DescribeLifecycleActions.md)|调用DescribeLifecycleActions查看伸缩活动对应的生命周期操作。|
|[CompleteLifecycleAction](/cn.zh-CN/API参考/生命周期挂钩/CompleteLifecycleAction.md)|调用CompleteLifecycleAction提前结束伸缩活动的等待状态。|
|[DeleteLifecycleHook](/cn.zh-CN/API参考/生命周期挂钩/DeleteLifecycleHook.md)|调用DeleteLifecycleHook删除一个生命周期挂钩。|

## 事件通知

|API|描述|
|---|--|
|[CreateNotificationConfiguration](/cn.zh-CN/API参考/事件通知/CreateNotificationConfiguration.md)|调用CreateNotificationConfiguration创建弹性伸缩事件及资源变化通知。|
|[DeleteNotificationConfiguration](/cn.zh-CN/API参考/事件通知/DeleteNotificationConfiguration.md)|调用DeleteNotificationConfiguration删除一条弹性伸缩事件及资源变化通知。|
|[DescribeNotificationConfigurations](/cn.zh-CN/API参考/事件通知/DescribeNotificationConfigurations.md)|调用DescribeNotificationConfigurations查询您创建的弹性伸缩事件及资源变化通知。|
|[DescribeNotificationTypes](/cn.zh-CN/API参考/事件通知/DescribeNotificationTypes.md)|调用DescribeNotificationTypes查询弹性伸缩事件及资源变化通知的类型。|
|[ModifyNotificationConfiguration](/cn.zh-CN/API参考/事件通知/ModifyNotificationConfiguration.md)|调用ModifyNotificationConfiguration修改一条弹性伸缩事件及资源变化通知的信息。|

## 实例

|API|描述|
|---|--|
|[EnterStandby](/cn.zh-CN/API参考/实例/EnterStandby.md)|调用EnterStandby将伸缩组内的ECS实例设置为备用状态。|
|[ExitStandby](/cn.zh-CN/API参考/实例/ExitStandby.md)|调用ExitStandby使伸缩组内处于备用状态的ECS实例进入运行状态。|
|[RebalanceInstances](/cn.zh-CN/API参考/实例/RebalanceInstances.md)|调用RebalanceInstances重新平衡多可用区伸缩组内ECS实例的分布。|
|[SetInstancesProtection](/cn.zh-CN/API参考/实例/SetInstancesProtection.md)|调用SetInstancesProtection保护或者停止保护伸缩组内的一台或者多台ECS实例。|
|[SetInstanceHealth](/cn.zh-CN/API参考/实例/SetInstanceHealth.md)|调用SetInstanceHealth设置伸缩组内ECS实例的健康状态。|

## 地域

|API|描述|
|---|--|
|[DescribeRegions](/cn.zh-CN/API参考/地域/DescribeRegions.md)|调用DescribeRegions查询可以使用弹性伸缩服务的地域。|

## 标签

|API|描述|
|---|--|
|[TagResources](/cn.zh-CN/API参考/标签/TagResources.md)|调用TagResources为指定的弹性伸缩资源列表统一创建并绑定标签。|
|[ListTagResources](/cn.zh-CN/API参考/标签/ListTagResources.md)|调用ListTagResources查询一个或多个弹性伸缩资源已经绑定的标签列表。|
|[UntagResources](/cn.zh-CN/API参考/标签/UntagResources.md)|调用UntagResources为指定的弹性伸缩资源列表统一解绑标签。解绑后，如果该标签没有绑定其他任何资源，会被自动删除。|
|[ListTagKeys](/cn.zh-CN/API参考/标签/ListTagKeys.md)|调用ListTagKeys查询弹性伸缩资源标签键的列表。|
|[ListTagValues](/cn.zh-CN/API参考/标签/ListTagValues.md)|调用ListTagValues查询弹性伸缩资源标签键对应的标签值。|

