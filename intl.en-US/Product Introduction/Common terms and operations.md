# Common terms and operations

This topic describes the common terms and operations in Auto Scaling.

## Common terms

|Term|Description|Reference|
|----|-----------|---------|
|Auto Scaling|Auto Scaling is a service that automatically scales ECS instances. You can configure the settings based on your business needs. When business loads increase, Auto Scaling automatically adds ECS instances to ensure computing power. When business loads decrease, Auto Scaling automatically removes ECS instances to reduce costs.|[What is Auto Scaling?](/intl.en-US/Product Introduction/What is Auto Scaling?.md)|
|scaling group|A scaling group is a group of ECS instances that are dynamically scaled based on the configured scenario. You can specify the minimum and maximum numbers of ECS instances in a scaling group, as well as the SLB and ApsaraDB RDS instances associated with the scaling group.|[Overview](/intl.en-US/Scaling Group/Scaling group/Overview.md)|
|ECS instance|An ECS instance is a virtual server that includes basic computing components such as CPU, memory, operating system, bandwidth, and disks. ECS eliminates the need to invest in IT hardware up front and allows you to scale computing resources on demand. This makes ECS more convenient and efficient than physical servers.|[What is ECS?](/intl.en-US/Product Introduction/What is ECS?.md)|
|Server Load Balancer instance or SLB instance|Server Load Balancer \(SLB\) is a service that distributes network traffic on demand to a group of backend servers to increase the throughput of your applications. You can use SLB to prevent service interruptions caused by single points of failure \(SPOFs\) and improve the availability of applications.|[What is CLB?](/intl.en-US/Product Introduction/What is CLB?.md)|
|RDS instance|ApsaraDB RDS \(RDS\) is a stable and reliable online database service that supports elastic scaling. It supports mainstream database engines and offers a full range of database solutions, such as disaster recovery, backup, restoration, monitoring, and migration.|[What is ApsaraDB for RDS?](/intl.en-US/Product Introduction/What is ApsaraDB for RDS?.md)|
|scaling mode|A scaling mode corresponds to operations for adding or removing ECS instances. Scaling modes include scheduled mode, dynamic mode, fixed quantity mode, custom mode, health mode, and multi-mode.|[Scaling modes](/intl.en-US/Product Introduction/Scaling modes.md)|
|instance configuration source|Auto Scaling uses the instance configuration source that you selected to create ECS instances. Instance configuration sources of scaling groups include scaling configurations and launch templates.|[Overview of instance configuration sources](/intl.en-US/Scaling Group/Instance Configuration Source/Overview of instance configuration sources.md)|
|scaling configuration|A scaling configuration is a source of instance configuration information and includes the configuration information of ECS instances.|[Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md)|
|scaling rule|-   Step scaling rules, target tracking scaling rules, and simple scaling rules are used to add or remove ECS instances when scaling activities are triggered.
-   Predictive scaling rules are used to predict the future metric values based on historical monitoring data and intelligently set boundary values for scaling groups.

|[Scaling rule overview](/intl.en-US/Scaling Group/Scaling rule/Scaling rule overview.md)|
|scaling task|Scaling tasks are classified into scheduled tasks and event-triggered tasks. A scheduled task can be used to scale ECS instances at the specified time. An event-triggered task can be used to dynamically scale ECS instances based on the specified monitoring metrics.|-   [Create a scheduled task](/intl.en-US/Automatic Scaling/Scheduled tasks/Create a scheduled task.md)
-   [Event-triggered task overview](/intl.en-US/Automatic Scaling/Alarm tasks/Event-triggered task overview.md) |
|scaling activity|A scaling activity records the changes of the number of ECS instances in a scaling group, the boundary values of the scaling group, and the expected number of ECS instances. Scaling activities are triggered when scaling rules are executed, the boundary values of a scaling group are modified, or the expected number of instances are modified.|[View the details of a scaling activity](/intl.en-US/Monitoring/Scaling events/View the details of a scaling activity.md)|
|expected number of instances|After the Expected Number of Instances feature is enabled, Auto Scaling automatically keeps the number of ECS instances at the expected value without the need for manual intervention.**Note:** You can enable this feature only when you create a scaling group. You can modify the expected number of instances for a scaling group that has the feature enabled.

|[Expected number of instances](/intl.en-US/Scaling Group/Scaling group/Expected number of instances.md)|
|parallel scaling activity|A scaling activity triggered by using one of the following methods is a parallel scaling activity:-   Execute a scaling rule manually or by using a scheduled task.
-   Manually add or remove ECS instances.
-   Perform a check on the instance health, or the expected, minimum, or maximum number of instances.

A parallel scaling activity can be executed if the ongoing scaling activities are also parallel ones.

**Note:** Parallel scaling activities and non-parallel scaling activities are differentiated only after the Expected Number of Instances feature is enabled. Otherwise, no other scaling activities can be executed while a scaling activity is in progress.

|[Expected number of instances](/intl.en-US/Scaling Group/Scaling group/Expected number of instances.md)|
|non-parallel scaling activity|A scaling activity that is not a parallel activity is a non-parallel scaling activity. No other scaling activities can be triggered if a non-parallel scaling activity is in progress.**Note:** Parallel scaling activities and non-parallel scaling activities are differentiated only after the Expected Number of Instances feature is enabled. Otherwise, no other scaling activities can be executed while a scaling activity is in progress.

|[Expected number of instances](/intl.en-US/Scaling Group/Scaling group/Expected number of instances.md)|
|stable instance|A stable instance refers to an ECS instance that is in the In Service, Protected, or Standby state in a scaling group.|[ECS instance lifecycle](/intl.en-US/Instance Management/ECS instance/ECS instance lifecycle.md)|
|scaling process|A scaling process refers to a process that you can manually suspend and resume, including the scale-out process, scale-in process, health check, scheduled task, and event-triggered task. Scaling processes help you control scaling groups at the process level.|-   [Suspend a scaling process](/intl.en-US/Scaling Group/Scaling group/Suspend a scaling process.md)
-   [Resume a scaling process](/intl.en-US/Scaling Group/Scaling group/Resume a scaling process.md) |
|lifecycle of an ECS instance in a scaling group|The lifecycle of an ECS instance in a scaling group refers to the process from the time when the instance is created to the time when it is released. The lifecycle management mode of an ECS instance depends on how the instance is created.-   If the instance is automatically created, the lifecycle of the instance is managed by the scaling group.
-   If the instance is manually created, and you enable the scaling group to manage the lifecycle of the instance, its lifecycle is managed by the scaling group. If you do not enable the scaling group to manage the lifecycle of the instance, you can manage its lifecycle by yourself.

|[ECS instance lifecycle](/intl.en-US/Instance Management/ECS instance/ECS instance lifecycle.md)|
|lifecycle hook|A lifecycle hook is used to put ECS instances that are being added to or removed from a scaling group into the wait state. After the ECS instances are put into the wait state, you can perform custom operations on them. For example, after an ECS instance is created, you can use a lifecycle hook to put the instance into the wait state. You can perform tests on the instance to ensure its service availability. Then, Auto Scaling adds the instance as an backend server to an associated SLB instance.|[Create a lifecycle hook](/intl.en-US/Scaling Group/Lifecycle hooks/Create a lifecycle hook.md)|
|cooldown time|The cooldown time refers to a period during which Auto Scaling cannot execute new scaling activities after one scaling activity is complete in a scaling group. Within the cooldown time, Auto Scaling rejects all scaling activity requests triggered by event-triggered tasks from Cloud Monitor. This prevents scaling activities from being triggered frequently due to metric value fluctuations.|[Cooldown time](/intl.en-US/Scaling Group/Scaling group/Cooldown time.md)|

## Common operations

|Operation|Description|Reference|
|---------|-----------|---------|
|Create a scaling group|Create a scaling group that is used to manage ECS instances used for the same scenario.|[Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md)|
|Create a scaling configuration|Create a scaling configuration that is used to specify the configuration information of automatically created ECS instances.|[Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md)|
|Create a scaling rule|Create a scaling rule that is used to add or remove ECS instances when scaling activities are triggered, or to intelligently set the boundary values of a scaling group.|[Create a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Create a scaling rule.md)|
|Create a scheduled task|Create a scheduled task that is used to scale ECS instances at the specified time.|[Create a scheduled task](/intl.en-US/Automatic Scaling/Scheduled tasks/Create a scheduled task.md)|
|Create an event-triggered task|Create an event-triggered task that is used to dynamically scale ECS instances based on specified monitoring metrics.|[Event-triggered task overview](/intl.en-US/Automatic Scaling/Alarm tasks/Event-triggered task overview.md)|
|Execute a scaling rule|Execute an existing scaling rule. You can execute a scaling rule manually, or by using a scheduled task or event-triggered task.|[Execute a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Execute a scaling rule.md)|
|Add existing ECS instances to a scaling group|Manually add existing ECS instances to a scaling group.**Note:** Subscription instances can be added to a scaling group, but their lifecycle cannot be managed by the scaling group.

|[Manually add an ECS instance to a scaling group](/intl.en-US/Instance Management/ECS instance/Manually add an ECS instance to a scaling group.md)|
|Perform rolling update|Update the configurations of ECS instances in a scaling group in batches. You can update the images of, execute scripts on, or install Operation Orchestration Service \(OOS\) packages on ECS instances in the In Service state in a scaling group.|[Rolling update](/intl.en-US/Scaling Group/Rolling update.md)|
|Perform an image update task|Select an ECS instance and replace the image of the specified scaling configuration with that of the ECS instance. Then, ECS instances are created based on the new image.**Note:** If you want to update the images of existing ECS instances in a scaling group, use the rolling update feature.

|[Replace images in multiple scaling configurations at a time](/intl.en-US/Scaling Group/Instance Configuration Source/Replace images in multiple scaling configurations at a time.md)|
|Suspend a scaling process|Suspend a scaling process. This allows you to perform some operations. For example, before you stop an ECS instance, you must suspend the health check process to make sure that the instance is not removed from the scaling group because the instance fails the health check.|[Suspend a scaling process](/intl.en-US/Scaling Group/Scaling group/Suspend a scaling process.md)|
|Resume a scaling process|Resume a suspended scaling process. This allows Auto Scaling to continue to perform some operations based on its functional logic. For example, after the health check process is resumed, Auto Scaling continues to perform health checks on ECS instances in the scaling group and removes unhealthy instances in a timely manner.|[Resume a scaling process](/intl.en-US/Scaling Group/Scaling group/Resume a scaling process.md)|
|Delete and remove an instance|Remove an ECS instance from a scaling group and then release it.|[Manually remove or delete an ECS instance](/intl.en-US/Instance Management/ECS instance/Manually remove or delete an ECS instance.md)|
|Remove an instance|Remove an ECS instance from a scaling group, but do not release it.|[Manually remove or delete an ECS instance](/intl.en-US/Instance Management/ECS instance/Manually remove or delete an ECS instance.md)|

