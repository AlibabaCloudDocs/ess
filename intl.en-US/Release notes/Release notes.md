# Release notes

This topic describes the release notes of Auto Scaling.

## July 2020

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Support for updating images in scaling configurations|You can create an update image task to replace images in scaling configurations in batches.|2020-07-02|All regions|[Replace images in multiple scaling configurations at a time](/intl.en-US/Scaling Group/Instance Configuration Source/Replace images in multiple scaling configurations at a time.md)|

## May 2020

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Auto Scaling service linked role|When the Auto Scaling service is activated, a service linked role named AliyunServiceRoleForAutoScaling is automatically created for Auto Scaling.|2020-05-06|All regions|[Grant permissions to Auto Scaling]()|

## April 2020

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Rolling update|Rolling update tasks can be used to update the configurations of ECS instances in batches.|2020-04-26|Some regions|[Rolling update](/intl.en-US/Scaling Group/Rolling update.md)|

## March 2020

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|System monitoring event-triggered tasks|System monitoring event-triggered tasks support more monitoring metrics.|2020-03-17|All regions|[Event-triggered tasks for system monitoring](/intl.en-US/Automatic Scaling/Alarm tasks/Event-triggered tasks for system monitoring.md)|
|Optimization for creating scaling groups|Configuration items for creating a scaling group are optimized. You can select an existing instance as the template source and add tags for a scaling group.|2020-03-11|All regions|[Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md)|

## December 2019

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Suspension and resumption of processes for a scaling group|You can suspend or resume processes for a scaling group to implement fine-grained control of scaling operations.|2019-12-03|All regions|-   [Suspend a scaling process](/intl.en-US/Scaling Group/Scaling group/Suspend a scaling process.md)
-   [Resume a scaling process](/intl.en-US/Scaling Group/Scaling group/Resume a scaling process.md) |

## October 2019

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Support for ECS instance health status|You can call an API operation to set the health status of an ECS instance.|2019-10-25|All regions|[SetInstanceHealth](/intl.en-US/API Reference/Instance/SetInstanceHealth.md)|
|Expected number of ECS instances|You can set an expected number of ECS instances for a scaling group. This allows Auto Scaling to flexibly execute parallel scaling activities.|2019-10-22|All regions|[Expected number of instances](/intl.en-US/Scaling Group/Scaling group/Expected number of instances.md)|

## September 2019

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Support for creating a scaling configuration from an existing instance|You can call an API operation to specify an instance as the template source when you create a scaling group. Auto Scaling obtains the configuration information of the instance and automatically creates a scaling configuration.|2019-09-24|All regions|[CreateScalingGroup](/intl.en-US/API Reference/Scaling group/CreateScalingGroup.md)|

## August 2019

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Support for associating a lifecycle hook with an OOS template|You can associate a lifecycle hook with an OOS template. When the lifecycle hook is triggered, Auto Scaling automatically uses the associated OOS template.|2019-08-14|All regions|[Create a lifecycle hook](/intl.en-US/Scaling Group/Lifecycle hooks/Create a lifecycle hook.md)|

## July 2019

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Support for mixed instance allocation in the cost optimization policy|When you set the multi-zone scaling policy to cost optimization policy, pay-as-you-go instances and preemptible instances are created based on the specified capacity.|2019-07-02|All regions|[Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md)|

## May 2019

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Step scaling rule|You can create a step scaling rule and implement fine-grained scaling control based on the size of the alert breach.|2019-05-20|All regions|[Create a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Create a scaling rule.md)|
|Multiple security groups|An automatically created instances can be added to multiple security groups.|2019-05-15|All regions|[Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md)|
|Query of the endpoint information|You can call an API operation to query regions that support Auto Scaling.|2019-05-05|All regions|[DescribeRegions](/intl.en-US/API Reference/Region/DescribeRegions.md)|

## April 2019

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Predictive scaling rule|You can create a predictive scaling rule. With predictive scaling rules, Auto Scaling adjusts the upper and lower limits for instances in a scaling group based on historical monitoring data.|2019-04-18|All regions|[t220151.md\#](/intl.en-US/Scaling Group/Scaling rule/Scaling rule overview.md)|
|Support for the DiskName, DiskDescription, and Encrypted parameters in scaling configurations|You can set the disk name, disk description, and encryption for a scaling configuration.|2019-04-04|All regions|[Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md)|

## January 2019

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Target tracking scaling rule|You can create a target tracking scaling rule. With target tracking scaling rules, Auto Scaling adjusts the number of ECS instances based on the specified target values.|2019-01-11|All regions|[Create a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Create a scaling rule.md)|

## December 2018

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Support for changing VSwitches|You can change the VSwitches associated with a scaling group.|2018-12-28|All regions|[Modify a scaling group](/intl.en-US/Scaling Group/Scaling group/Modify a scaling group.md)|
|Cost optimization policy|The multi-zone scaling policy supports the cost optimization policy.|2018-12-16|All regions|-   [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md)
-   [Reduce costs by configuring a cost optimization policy](/intl.en-US/Best practices/Reduce costs by configuring a cost optimization policy.md) |
|VServer groups|You can specify VServer groups for SLB instances in a scaling group.|2018-12-07|All regions|[Use SLB in Auto Scaling](/intl.en-US/Instance Management/SLB instance/Use SLB in Auto Scaling.md)|

## November 2018

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|No Fees for Stopped Instances \(VPC-Connected\)|After this feature is enabled, ECS instances that you remove from a scaling group are stopped and not charged for resources allocated to them.|2018-11-28|All regions|-   [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md)
-   [CreateScalingGroup](/intl.en-US/API Reference/Scaling group/CreateScalingGroup.md)
-   [RemoveInstances](/intl.en-US/API Reference/Trigger task/RemoveInstances.md) |

## October 2018

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Enhanced whitelists of ApsaraDB for RDS instances|You can add internal IP addresses of the ECS instances in a scaling group to the enhanced whitelists of the associated ApsaraDB for RDS instances.|2018-10-19|All regions|[Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md)|

## September 2018

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Auto Scaling released in the UK \(London\) region|Auto Scaling is available in the UK \(London\) region.|2018-09-30|All regions|[What is Auto Scaling?](/intl.en-US/Product Introduction/What is Auto Scaling?.md)|
|Shutdown and reclaim mode|You can configure the shutdown and reclaim mode for a scaling group.|2018-09-13|All regions|[Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md)|
|Launch template|You can specify a launch template as the instance configuration source for a scaling group.|2018-09-01|All regions|[Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md)|

## August 2018

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Cron expressions for scheduled tasks|You can use a cron expression to specify the recurrence for a scheduled task.|2018-08-20|All regions|[Create a scheduled task](/intl.en-US/Automatic Scaling/Scheduled tasks/Create a scheduled task.md)|
|Notifications for scheduled task expiration|You can configure an expiration notification for scheduled tasks.|2018-08-20|All regions|[Create an event notification](/intl.en-US/Monitoring/Event notification/Create an event notification.md)|

## July 2018

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Modification of information about data disks and preemptible instances|You can modify information about data disks and the price limits of preemptible instances in scaling configurations.|2018-07-27|All regions|[Modify a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Modify a scaling configuration.md)|
|Association with ApsaraDB for RDS instances|You can associate or dissociate ApsaraDB for RDS instances with or from a scaling group.|2018-07-11|All regions|[Modify a scaling group](/intl.en-US/Scaling Group/Scaling group/Modify a scaling group.md)|
|Association with SLB instances|You can associate or dissociate SLB instances with or from a scaling group.|2018-07-04|All regions|[Modify a scaling group](/intl.en-US/Scaling Group/Scaling group/Modify a scaling group.md)|

## June 2018

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Modification of scaling configurations|You can modify existing scaling configurations.|2018-06-27|All regions|[Modify a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Modify a scaling configuration.md)|
|Lifecycle hooks|When an ECS instance is automatically created or removed from a scaling group, lifecycle hooks can be used to put the instance into the wait state. This allows you to perform operations on the instance.|2018-06-01|All regions|[Create a lifecycle hook](/intl.en-US/Scaling Group/Lifecycle hooks/Create a lifecycle hook.md)|

## April 2018

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Scaling activity notification|When a scaling activity of a specified type occurs in a scaling group, Auto Scaling sends notifications to Cloud Monitor or Message Service.|2018-04-20|All regions|[Event notification overview](/intl.en-US/Monitoring/Event notification/Event notification overview.md)|

## March 2018

|Feature|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Protected state|You can put ECS instances in a scaling group into the protected state. Instances in the protected state are not released or removed from the scaling group during scale-in events.|2018-03-28|All regions|[Put an ECS instance into the Protected state](/intl.en-US/Instance Management/ECS instance/Put an ECS instance into the Protected state.md)|
|Standby state|You can put ECS instances in a scaling group into the standby state and manage the lifecycle of the ECS instances.|2018-03-15|All regions|[Put an ECS instance into the Standby state](/intl.en-US/Instance Management/ECS instance/Put an ECS instance into the Standby state.md)|

## 2015

|Service|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Auto Scaling|Auto Scaling is released.|2015-08-27|Some regions|[What is Auto Scaling?](/intl.en-US/Product Introduction/What is Auto Scaling?.md)|

## 2014

|Service|Description|Released on|Released in|Reference|
|-------|:----------|:----------|-----------|:--------|
|Auto Scaling|Auto Scaling is released for internal preview.|2014-10-15|Some regions|[What is Auto Scaling?](/intl.en-US/Product Introduction/What is Auto Scaling?.md)|
