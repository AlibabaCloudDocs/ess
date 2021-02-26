# Usage processes

This topic describes how to use Auto Scaling to build high-elasticity and high-availability applications.

Auto Scaling provides the following capabilities for applications:

-   High elasticity: Auto Scaling automatically creates and releases ECS instances based on your settings without the need for manual intervention.
-   High availability: Auto Scaling automatically performs checks on ECS instances, releases stopped instances, and then creates instances.

The following figure shows the general process of using Auto Scaling.

![autoscaling-process](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3861034161/p190444.png)

The following section describes the process:

1.  [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md).

    A scaling group is a basic management unit when you use Auto Scaling to manage ECS instances on which your business is deployed. Scaling groups are used to manage ECS instances that are applied to the same scenario and can be associated with multiple SLB instances and ApsaraDB RDS instances. After a scaling group is associated with SLB and ApsaraDB RDS instances, ECS instances that are added to the scaling group are automatically added as backend servers of the associated SLB instances. The internal IP addresses of these instances are automatically added to the whitelists of the associated ApsaraDB RDS instances.

2.  [Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md).

    A scaling configuration is a template used by Auto Scaling to automatically create ECS instances. You can create multiple scaling configurations for a scaling group. However, only one scaling configuration can be active at a time. For more information, see [Overview of instance configuration sources](/intl.en-US/Scaling Group/Instance Configuration Source/Overview of instance configuration sources.md).

    **Note:** If you use a launch template or an existing instance as the configuration source when you create a scaling group, you can directly enable the scaling group without the need to manually create a scaling configuration.

3.  Enable the scaling group.

    After you create a scaling configuration for the first time, you are prompted to enable the scaling group. You can also enable the scaling group on the Scaling Groups page. For more information, see [Enable a scaling group](/intl.en-US/Scaling Group/Scaling group/Enable a scaling group.md).

4.  [Create a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Create a scaling rule.md).

    A scaling rule is used to specify information such as the number of ECS instances to be scaled or intelligently set the boundary values of a scaling group. You can create scaling rules of the corresponding type based on your business needs. For more information, see [Scaling rule overview](/intl.en-US/Scaling Group/Scaling rule/Scaling rule overview.md).

5.  Create a scaling task.

    After a scaling rule is created, you can use a scaling task to automatically execute the scaling rule. Auto Scaling supports the following types of scaling tasks:

    -   [Scheduled tasks](/intl.en-US/Automatic Scaling/Scheduled tasks/Create a scheduled task.md)

        If you can predict the time when your business loads fluctuate, you can use scheduled tasks to automatically scale ECS instances at the specified time. You can set the recurrence for scheduled tasks to meet your periodic requirements for automatic scaling.

    -   [Event-triggered tasks](/intl.en-US/Automatic Scaling/Alarm tasks/Create a monitoring task.md)

        If you want to automatically scale ECS instances based on their running metrics, you can use event-triggered tasks. An event-triggered task dynamically manages ECS instances in a scaling group based on monitoring metrics from Cloud Monitor. For more information, see [Event-triggered task overview](/intl.en-US/Automatic Scaling/Alarm tasks/Event-triggered task overview.md).


