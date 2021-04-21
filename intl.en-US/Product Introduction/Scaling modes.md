# Scaling modes

This topic describes the scaling modes of Auto Scaling. A scaling mode is used to specify when to add or remove a specific number of ECS instances for a scaling group.

-   Scheduled mode: You can create a scheduled task to execute a specific scaling rule at the specified point in time.
-   Dynamic mode: You can create an event-triggered task based on a Cloud Monitor performance metric such as the CPU utilization. When the metric data of a scaling group meets the specified alert conditions, an alert is triggered to execute your specified scaling rule.
-   Fixed-number mode:
    -   If you have set **Minimum Number of Instances** when you create a scaling group, Auto Scaling automatically adds ECS instances to the scaling group to make the number of existing ECS instances equal to the minimum number of instances when the number of ECS instances in the scaling group is less than the minimum number.
    -   If you have set **Maximum Number of Instances** when you create a scaling group, Auto Scaling automatically removes ECS instances from the scaling group to make the number of existing ECS instances equal to the maximum number of instances when the number of ECS instances in the scaling group is greater than the maximum number.
    -   If you have set **Expected Number of Instances** when you create a scaling group, Auto Scaling automatically maintains the number of ECS instances in the scaling group at the expected number.
-   Health mode: After you enable the health check feature when you create a scaling group, Auto Scaling checks the status of the ECS instances in the scaling group on a regular basis. If an ECS instance is not in the Running state, the instance is considered to be unhealthy and is removed from the scaling group.
-   Custom mode: You can manually perform scaling, including manually executing scaling rules, or adding, removing, or deleting existing ECS instances.
-   Multi-mode: You can combine the preceding modes to meet your business requirements. For example, if your business loads significantly increase starting from 12:00 every day, you can create a scheduled task to create 20 ECS instances at 12:00 every day. If the number of created ECS instances do not meet your requirements, you can combine the scheduled mode with other scaling modes such as the dynamic mode and custom mode.

