# Auto Scaling alarm tasks {#concept_w5s_m1d_sfb .concept}

This topic introduces Auto Scaling alarm tasks.

Auto Scaling alarm tasks integrate some functions of Auto Scaling and CloudMonitor. These tasks allow you to manage scaling groups in a manner similar to Auto Scaling scheduled tasks. The alarm tasks trigger user-defined scaling rules to execute scaling activities, adjusting the number of instances in scaling groups.

You can use scheduled tasks to execute specific scaling rules at specifics point in time. In scenarios where the time of traffic changes is predictable, scheduled tasks are sufficient to respond to such changes in advance. However, in scenarios where traffic is not predictable or for sudden spikes in traffic, scheduled tasks are insufficient to deal with the changes. In this case, alarm tasks provide more flexibility in triggering scaling rules. Alarm tasks can be used to increase the number of instances in a scaling group during peak hours to suffice business requirements, and release instances in the scaling group during off-peak hours to reduce production costs.

Alarm tasks collect measurements from specific metrics in real time. When a measurement meets user-defined alarm conditions, an alarm is triggered and the specified scaling rule is executed. Alarm tasks adjust the number of instances in a scaling group in real time based on business changes, ensuring that monitored metrics stay within a user-defined range.

Auto Scaling alarm tasks allow the dynamic change of the number of instances in a scaling group by monitoring specific metrics. Through the tasks, specified scaling rules are executed in real time based on business changes to adjust the number of instances in a scaling group.

## Updated version of Auto Scaling alarm tasks {#section_jjh_p1d_sfb .section}

Auto Scaling alarm tasks have been comprehensively optimized in the scope, method, and response time of monitoring. The features of the updated version allow you to use alarm tasks to manage scaling groups in a more comprehensive and reliable manner.

The new features are as follows:

-   You can configure alarm tasks for the system disks, NICs, and TCP connections.
-   You can set the data collection interval as short as one minute to perform monitoring functions at a finer granularity.
-   You can use the new custom monitoring function, which provides you with a standard way to integrate your own monitoring system with Auto Scaling alarm tasks.

You can use more metrics in the updated version. In addition to the metrics provided in earlier versions, you can add your custom metrics to customize alarm tasks. These custom metrics enhance the capabilities of Auto Scaling alarm tasks to meet a range of diverse scenarios.

