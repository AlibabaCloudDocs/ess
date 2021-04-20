# Release notes

This topic describes the release notes of Auto Scaling.

## February 2021

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Scaling configurations|Weights can be set for instance types.|2021-02-12|All|-   [Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md)
-   [t2039652.md\#]()
-   [CreateScalingConfiguration](/intl.en-US/API Reference/Scaling configuration/CreateScalingConfiguration.md) |

## January 2021

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Scaling configurations|Auto Scaling can automatically generate sequential and unique hostnames.|2021-01-15|All|-   [Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md)
-   [t2043005.md\#]()
-   [CreateScalingConfiguration](/intl.en-US/API Reference/Scaling configuration/CreateScalingConfiguration.md) |

## November 2020

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Scaling configurations|The performance levels of system disks or data disks that are enhanced SSDs \(ESSDs\) can be specified.|2020-11-18|All|-   [Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md)
-   [CreateScalingConfiguration](/intl.en-US/API Reference/Scaling configuration/CreateScalingConfiguration.md) |

## October 2020

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Event-triggered tasks|The statistical methods supported by custom monitoring event-triggered tasks are added.|2020-10-25|All|-   [Create event-triggered tasks](/intl.en-US/Automatic Scaling/Alarm tasks/Create a monitoring task.md)
-   [CreateAlarm](/intl.en-US/API Reference/Alarm tasks/CreateAlarm.md) |

## September 2020

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Modification of scaling configurations|The images specified in scaling configurations can be modified.|2020-09-24|All|[Replace the image in a single scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Replace the image in a single scaling configuration.md)|

## August 2020

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Rolling update|Operation Orchestration Service \(OOS\) packages can be used to install software.|2020-08-20|Some|[Rolling update](/intl.en-US/Scaling Group/Rolling update.md)|
|Expected number of instances|The expected number of instances in a scaling group can be modified when you delete or remove ECS instances from the scaling group.|2020-08-12|All|[Expected number of instances](/intl.en-US/Scaling Group/Scaling group/Expected number of instances.md)|
|Scheduled tasks|The expiration time can be left unspecified. The maximum recurrence period is changed to one year.|2020-08-07|All|[Create a scheduled task](/intl.en-US/Automatic Scaling/Scheduled tasks/Create a scheduled task.md)|

## July 2020

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Modification of scaling groups|Health check can be enabled or disabled for ECS instances in an existing scaling group.|2020-07-30|All|[Modify a scaling group](/intl.en-US/Scaling Group/Scaling group/Modify a scaling group.md)|
|Support for updating images in scaling configurations|Image update tasks can be created to replace images in scaling configurations in batches.|2020-07-02|All|[Replace images in multiple scaling configurations at a time](/intl.en-US/Scaling Group/Instance Configuration Source/Replace images in multiple scaling configurations at a time.md)|

## May 2020

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Auto Scaling service-linked role|The AliyunServiceRoleForAutoScaling service-linked role is automatically created for Auto Scaling when the Auto Scaling service is activated.|2020-05-06|All|[Manage the Auto Scaling service linked role](/intl.en-US/Quick Start/Manage the Auto Scaling service linked role.md)|

## April 2020

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Rolling update|Rolling update tasks can be used to update the configurations of ECS instances in batches.|2020-04-26|Some|[Rolling update](/intl.en-US/Scaling Group/Rolling update.md)|

## March 2020

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|System monitoring event-triggered tasks|System monitoring event-triggered tasks can support more monitoring metrics.|2020-03-17|All|[Event-triggered tasks for system monitoring](/intl.en-US/Automatic Scaling/Alarm tasks/Event-triggered tasks for system monitoring.md)|
|Optimization for creating scaling groups|Configuration items for creating a scaling group are optimized. You can select an existing instance as the template and add tags for a scaling group.|2020-03-11|All|[Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md)|

## December 2019

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Suspension and resumption of processes for a scaling group|Processes for a scaling group can be suspended or resumed to implement fine-grained control of scaling operations.|2019-12-03|All|-   [Suspend a scaling process](/intl.en-US/Scaling Group/Scaling group/Suspend a scaling process.md)
-   [Resume a scaling process](/intl.en-US/Scaling Group/Scaling group/Resume a scaling process.md) |

## October 2019

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Support for ECS instance health status|An API operation can be called to set the health status of an ECS instance.|2019-10-25|All|[SetInstanceHealth](/intl.en-US/API Reference/Instance/SetInstanceHealth.md)|
|Expected number of instances|The expected number of ECS instances in a scaling group can be set. This allows Auto Scaling to flexibly execute parallel scaling activities.|2019-10-22|All|[Expected number of instances](/intl.en-US/Scaling Group/Scaling group/Expected number of instances.md)|

## September 2019

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Support for creating a scaling configuration from an existing instance|An API operation can be called to specify an instance as the template when you create a scaling group. Auto Scaling obtains the configuration information of the instance and automatically creates a scaling configuration.|2019-09-24|All|[CreateScalingGroup](/intl.en-US/API Reference/Scaling group/CreateScalingGroup.md)|

## August 2019

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Support for associating a lifecycle hook with an OOS template|A lifecycle hook can be associated with an OOS template. When the lifecycle hook is triggered, Auto Scaling automatically uses the associated OOS template.|2019-08-14|All|[Create a lifecycle hook](/intl.en-US/Scaling Group/Lifecycle hooks/Create a lifecycle hook.md)|

## July 2019

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Support for mixed instance allocation in the cost optimization policy|Pay-as-you-go instances and preemptible instances are created based on the specified capacity when you set the multi-zone scaling policy to cost optimization policy.|2019-07-02|All|[Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md)|

## May 2019

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Step scaling rules|A step scaling rule can be created to implement fine-grained scaling control based on the size of the alert breach.|2019-05-20|All|[Create a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Create a scaling rule.md)|
|Multiple security groups|An automatically created instance can be added to multiple security groups.|2019-05-15|All|[Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md)|
|Query of the endpoint information|An API operation can be called to query regions that support Auto Scaling.|2019-05-05|All|[DescribeRegions](/intl.en-US/API Reference/Region/DescribeRegions.md)|

## April 2019

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Predictive scaling rules|Predictive scaling rules can be created. After a predictive scaling rule is created, Auto Scaling adjusts the minimum and maximum numbers of instances in a scaling group based on historical monitoring data.|2019-04-18|All|[t220151.md\#](/intl.en-US/Scaling Group/Scaling rule/Overview.md)|
|Support for the DiskName, DiskDescription, and Encrypted parameters in scaling configurations|The disk name, disk description, and encryption can be set for a scaling configuration.|2019-04-04|All|[Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md)|

## January 2019

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Target tracking scaling rules|Target tracking scaling rules can be created. After a target tracking scaling rule is created, Auto Scaling adjusts the number of ECS instances based on the specified target values.|2019-01-11|All|[Create a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Create a scaling rule.md)|

## December 2018

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Support for changing vSwitches|The vSwitches associated with a scaling group can be changed.|2018-12-28|All|[Modify a scaling group](/intl.en-US/Scaling Group/Scaling group/Modify a scaling group.md)|
|Cost optimization policy|The cost optimization policy is available for the multi-zone scaling policy.|2018-12-16|All|-   [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md)
-   [Reduce costs by configuring a cost optimization policy](/intl.en-US/Best practices/Reduce costs by configuring a cost optimization policy.md) |
|vServer groups|vServer groups cab be specified for SLB instances associated with a scaling group.|2018-12-07|All|[Use SLB in Auto Scaling](/intl.en-US/Instance Management/SLB instance/Use SLB in Auto Scaling.md)|

## November 2018

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|No Fees for Stopped Instances \(VPC-Connected\)|ECS instances that are removed from a scaling group can enter the No Fees for Stopped Instances \(VPC-Connected\) state.|2018-11-28|All|-   [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md)
-   [CreateScalingGroup](/intl.en-US/API Reference/Scaling group/CreateScalingGroup.md)
-   [RemoveInstances](/intl.en-US/API Reference/Trigger task/RemoveInstances.md) |

## October 2018

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Enhanced whitelists of ApsaraDB RDS instances|The internal IP addresses of ECS instances in a scaling group can be added to the enhanced whitelists of the ApsaraDB RDS instances that are associated with the scaling group.|2018-10-19|All|[Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md)|

## September 2018

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Release of Auto Scaling in the UK \(London\) region|Auto Scaling is available in the UK \(London\) region.|2018-09-30|All|[What is Auto Scaling?](/intl.en-US/Product Introduction/What is Auto Scaling?.md)|
|Shutdown and reclaim mode|The shutdown and reclaim mode can be specified for a scaling group.|2018-09-13|All|[Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md)|
|Launch template|A launch template can be specified as the instance configuration source for a scaling group.|2018-09-01|All|[Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md)|

## August 2018

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Cron expressions for scheduled tasks|Cron expressions can be used to specify the recurrence for scheduled tasks.|2018-08-20|All|[Create a scheduled task](/intl.en-US/Automatic Scaling/Scheduled tasks/Create a scheduled task.md)|
|Expiration notifications for scheduled tasks|Expiration notifications can be configured for scheduled tasks.|2018-08-20|All|[Create an event notification](/intl.en-US/Monitoring/Event notification/Create an event notification.md)|

## July 2018

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Modification of information about data disks and preemptible instances|Information about data disks and the price limits of preemptible instances in scaling configurations can be modified.|2018-07-27|All|[Modify a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Modify a scaling configuration.md)|
|Association with ApsaraDB RDS instances|ApsaraDB RDS instances can be associated with or disassociated from a scaling group.|2018-07-11|All|[Modify a scaling group](/intl.en-US/Scaling Group/Scaling group/Modify a scaling group.md)|
|Association with SLB instances|SLB instances can be associated with or disassociated from a scaling group.|2018-07-04|All|[Modify a scaling group](/intl.en-US/Scaling Group/Scaling group/Modify a scaling group.md)|

## June 2018

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Modification of scaling configurations|Existing scaling configurations can be modified.|2018-06-27|All|[Modify a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Modify a scaling configuration.md)|
|Lifecycle hooks|When an ECS instance is automatically created or removed from a scaling group, lifecycle hooks can be used to put the instance into the wait state. This allows you to perform operations on the instance.|2018-06-01|All|[Create a lifecycle hook](/intl.en-US/Scaling Group/Lifecycle hooks/Create a lifecycle hook.md)|

## April 2018

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Scaling activity notifications|When a scaling activity of a specific type occurs in a scaling group, notifications can be sent to Cloud Monitor or Message Service.|2018-04-20|All|[Event notification overview](/intl.en-US/Monitoring/Event notification/Event notification overview.md)|

## March 2018

|Feature|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Protected state|ECS instances in a scaling group can be put into the protected state. Instances in the protected state are not released or removed from the scaling group during scale-in events.|2018-03-28|All|[Put an ECS instance into the Protected state](/intl.en-US/Instance Management/ECS instance/Put an ECS instance into the Protected state.md)|
|Standby state|ECS instances in a scaling group can be put into the standby state. This allows you to manage the lifecycle of the ECS instances.|2018-03-15|All|[Put an ECS instance into the Standby state](/intl.en-US/Instance Management/ECS instance/Put an ECS instance into the Standby state.md)|

## 2015

|Service|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Auto Scaling|Auto Scaling is released.|2015-08-27|Some|[What is Auto Scaling?](/intl.en-US/Product Introduction/What is Auto Scaling?.md)|

## 2014

|Service|Description|Release date|Region|References|
|-------|:----------|:-----------|------|:---------|
|Auto Scaling|Auto Scaling is in internal preview.|2014-10-15|Some|[What is Auto Scaling?](/intl.en-US/Product Introduction/What is Auto Scaling?.md)|

