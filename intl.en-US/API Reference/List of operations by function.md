# List of operations by function

The following tables list the API operations available for use in Auto Scaling.

## Scaling groups

|Operation|Description|
|---------|-----------|
|[CreateScalingGroup](/intl.en-US/API Reference/Scaling group/CreateScalingGroup.md)|Creates a scaling group.|
|[ModifyScalingGroup](/intl.en-US/API Reference/Scaling group/ModifyScalingGroup.md)|Modifies a scaling group.|
|[EnableScalingGroup](/intl.en-US/API Reference/Scaling group/EnableScalingGroup.md)|Enables a scaling group.|
|[DisableScalingGroup](/intl.en-US/API Reference/Scaling group/DisableScalingGroup.md)|Disables a scaling group.|
|[SetGroupDeletionProtection](/intl.en-US/API Reference/Scaling group/SetGroupDeletionProtection.md)|Enables or disables deletion protection for a scaling group.|
|[DeleteScalingGroup](/intl.en-US/API Reference/Scaling group/DeleteScalingGroup.md)|Deletes a scaling group.|
|[DescribeScalingGroups](/intl.en-US/API Reference/Scaling group/DescribeScalingGroups.md)|Queries scaling groups.|
|[DescribeScalingInstances](/intl.en-US/API Reference/Scaling group/DescribeScalingInstances.md)|Queries the list of Elastic Compute Service \(ECS\) instances in a scaling group and lists details about the instances.|
|[DescribeScalingActivities](/intl.en-US/API Reference/Scaling group/DescribeScalingActivities.md)|Queries scaling activities.|
|[DescribeScalingActivityDetail](/intl.en-US/API Reference/Scaling group/DescribeScalingActivityDetail.md)|Queries detailed information about a scaling activity.|
|[AttachLoadBalancers](/intl.en-US/API Reference/Scaling group/AttachLoadBalancers.md)|Associates one or more Server Load Balancer \(SLB\) instances with a scaling group.|
|[DetachLoadBalancers](/intl.en-US/API Reference/Scaling group/DetachLoadBalancers.md)|Disassociates one or more SLB instances from a scaling group.|
|[AttachDBInstances](/intl.en-US/API Reference/Scaling group/AttachDBInstances.md)|Associates one or more ApsaraDB RDS instances with a scaling group.|
|[DetachDBInstances](/intl.en-US/API Reference/Scaling group/DetachDBInstances.md)|Disassociates one or more ApsaraDB RDS instances from a scaling group.|
|[AttachVServerGroups](/intl.en-US/API Reference/Scaling group/AttachVServerGroups.md)|Adds one or more vServer groups of an SLB instance to a scaling group.|
|[DetachVServerGroups](/intl.en-US/API Reference/Scaling group/DetachVServerGroups.md)|Removes one or more vServer groups.|
|[SuspendProcesses](/intl.en-US/API Reference/Scaling group/SuspendProcesses.md)|Suspends the specified processes in a scaling group.|
|[ResumeProcesses](/intl.en-US/API Reference/Scaling group/ResumeProcesses.md)|Resumes the suspended processes in a scaling group.|

## Scaling configurations

|Operation|Description|
|---------|-----------|
|[CreateScalingConfiguration](/intl.en-US/API Reference/Scaling configuration/CreateScalingConfiguration.md)|Creates a scaling configuration.|
|[DescribeScalingConfigurations](/intl.en-US/API Reference/Scaling configuration/DescribeScalingConfigurations.md)|Queries scaling configurations.|
|[DeleteScalingConfiguration](/intl.en-US/API Reference/Scaling configuration/DeleteScalingConfiguration.md)|Deletes a scaling configuration.|
|[ModifyScalingConfiguration](/intl.en-US/API Reference/Scaling configuration/ModifyScalingConfiguration.md)|Modifies a scaling configuration.|

## Scaling rules

|Operation|Description|
|---------|-----------|
|[CreateScalingRule](/intl.en-US/API Reference/Scaling rule/CreateScalingRule.md)|Creates a scaling rule.|
|[ModifyScalingRule](/intl.en-US/API Reference/Scaling rule/ModifyScalingRule.md)|Modifies a scaling rule.|
|[DescribeScalingRules](/intl.en-US/API Reference/Scaling rule/DescribeScalingRules.md)|Queries all scaling rules in a scaling group and lists information about the scaling rules.|
|[DeleteScalingRule](/intl.en-US/API Reference/Scaling rule/DeleteScalingRule.md)|Deletes a scaling rule.|

## Scaling tasks

|Operation|Description|
|---------|-----------|
|[ExecuteScalingRule](/intl.en-US/API Reference/Trigger task/ExecuteScalingRule.md)|Executes a scaling rule.|
|[AttachInstances](/intl.en-US/API Reference/Trigger task/AttachInstances.md)|Adds ECS instances to a scaling group.|
|[RemoveInstances](/intl.en-US/API Reference/Trigger task/RemoveInstances.md)|Deletes ECS instances in a scaling group.|
|[DetachInstances](/intl.en-US/API Reference/Trigger task/DetachInstances.md)|Removes one or more ECS instances from a scaling group.|

## Scheduled tasks

|Operation|Description|
|---------|-----------|
|[CreateScheduledTask](/intl.en-US/API Reference/Scheduled tasks/CreateScheduledTask.md)|Creates a scheduled task.|
|[ModifyScheduledTask](/intl.en-US/API Reference/Scheduled tasks/ModifyScheduledTask.md)|Modifies a scheduled task.|
|[DescribeScheduledTasks](/intl.en-US/API Reference/Scheduled tasks/DescribeScheduledTasks.md)|Queries scheduled tasks.|
|[DeleteScheduledTask](/intl.en-US/API Reference/Scheduled tasks/DeleteScheduledTask.md)|Deletes a scheduled task.|

## Event-triggered tasks

|Operation|Description|
|---------|-----------|
|[CreateAlarm](/intl.en-US/API Reference/Alarm tasks/CreateAlarm.md)|Creates an event-triggered task.|
|[DescribeAlarms](/intl.en-US/API Reference/Alarm tasks/DescribeAlarms.md)|Queries event-triggered tasks.|
|[ModifyAlarm](/intl.en-US/API Reference/Alarm tasks/ModifyAlarm.md)|Modifies an event-triggered task.|
|[EnableAlarm](/intl.en-US/API Reference/Alarm tasks/EnableAlarm.md)|Enables an event-triggered task.|
|[DisableAlarm](/intl.en-US/API Reference/Alarm tasks/DisableAlarm.md)|Disables an event-triggered task.|
|[DeleteAlarm](/intl.en-US/API Reference/Alarm tasks/DeleteAlarm.md)|Deletes an event-triggered task.|

## Lifecycle hooks

|Operation|Description|
|---------|-----------|
|[CreateLifecycleHook](/intl.en-US/API Reference/Lifecycle Hook/CreateLifecycleHook.md)|Creates one or more lifecycle hooks in a scaling group.|
|[ModifyLifecycleHook](/intl.en-US/API Reference/Lifecycle Hook/ModifyLifecycleHook.md)|Modifies a lifecycle hook.|
|[DescribeLifecycleHooks](/intl.en-US/API Reference/Lifecycle Hook/DescribeLifecycleHooks.md)|Queries lifecycle hooks.|
|[RecordLifecycleActionHeartbeat](/intl.en-US/API Reference/Lifecycle Hook/RecordLifecycleActionHeartbeat.md)|Extends the timeout period of an ECS instance and keeps the instance in the wait state.|
|[DescribeLifecycleActions](/intl.en-US/API Reference/Lifecycle Hook/DescribeLifecycleActions.md)|Queries the lifecycle actions that correspond to a scaling activity.|
|[CompleteLifecycleAction](/intl.en-US/API Reference/Lifecycle Hook/CompleteLifecycleAction.md)|Takes a scaling activity out of the wait state in advance.|
|[DeleteLifecycleHook](/intl.en-US/API Reference/Lifecycle Hook/DeleteLifecycleHook.md)|Deletes a lifecycle hook.|

## Event notifications

|Operation|Description|
|---------|-----------|
|[CreateNotificationConfiguration](/intl.en-US/API Reference/Event notification/CreateNotificationConfiguration.md)|Creates an event notification.|
|[DeleteNotificationConfiguration](/intl.en-US/API Reference/Event notification/DeleteNotificationConfiguration.md)|Deletes an event notification.|
|[DescribeNotificationConfigurations](/intl.en-US/API Reference/Event notification/DescribeNotificationConfigurations.md)|Queries event notifications.|
|[DescribeNotificationTypes](/intl.en-US/API Reference/Event notification/DescribeNotificationTypes.md)|Queries the types of event notifications.|
|[ModifyNotificationConfiguration](/intl.en-US/API Reference/Event notification/ModifyNotificationConfiguration.md)|Modifies an event notification.|

## Instances

|Operation|Description|
|---------|-----------|
|[EnterStandby](/intl.en-US/API Reference/Instance/EnterStandby.md)|Puts ECS instances in a scaling group into the standby state.|
|[ExitStandby](/intl.en-US/API Reference/Instance/ExitStandby.md)|Changes the state of ECS instances in a scaling group from standby to running.|
|[RebalanceInstances](/intl.en-US/API Reference/Instance/RebalanceInstances.md)|Rebalances the distribution of ECS instances in a scaling group across multiple zones.|
|[SetInstancesProtection](/intl.en-US/API Reference/Instance/SetInstancesProtection.md)|Enables or disables protection for one or more ECS instances in a scaling group.|
|[SetInstanceHealth](/intl.en-US/API Reference/Instance/SetInstanceHealth.md)|Sets the health status of ECS instances in a scaling group.|

## Regions

|Operation|Description|
|---------|-----------|
|[DescribeRegions](/intl.en-US/API Reference/Region/DescribeRegions.md)|Queries the regions where Auto Scaling is available.|

## Tags

|Operation|Description|
|---------|-----------|
|[TagResources](/intl.en-US/API Reference/Tag management/TagResources.md)|Creates and adds tags to specified Auto Scaling resources.|
|[ListTagResources](/intl.en-US/API Reference/Tag management/ListTagResources.md)|Queries the tags that are added to one or more Auto Scaling resources.|
|[UntagResources](/intl.en-US/API Reference/Tag management/UntagResources.md)|Removes tags from the specified Auto Scaling resources. After a tag is removed, the tag is automatically deleted if it is not added to other resources.|
|[ListTagKeys](/intl.en-US/API Reference/Tag management/ListTagKeys.md)|Queries the tag keys of Auto Scaling resources.|
|[ListTagValues](/intl.en-US/API Reference/Tag management/ListTagValues.md)|Queries the tag values of Auto Scaling tag keys.|

