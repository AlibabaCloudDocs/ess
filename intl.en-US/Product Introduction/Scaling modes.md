# Scaling modes {#concept_q24_3gm_qfb .concept}

This article introduces the scaling modes of Auto Scaling.

-   Scheduled scaling: You tell Auto Scaling to perform a scaling operation at specified times. For example, scaling up at 13:00 every day.
-   Dynamic scaling: Auto Scaling dynamically scales up and down by tracking targets. You select a metric and set a target value. Auto Scaling creates the CloudMonitor alarms that trigger the scaling policy. The scaling policy adds or removes capacity as required to keep the metric at, or close to, the specified target value.
-   Capacity maintaining: You setup the **MinSize** to maintain the minimum number of running healthy instances in the scaling group.
-   Customized target tracking: Uses API to manually scale based on metrics from your own monitoring system.
    -   Manually run scaling policy.
    -   Manually add or remove ECS instances.
    -   Automatically adjust the number of your ECS instances to lie between the MinSize and MaxSize you setup.
-   Health check: Automatically release instances with status other than **Running** according to the policies you specify.
-   Multimode: Combine multiple scaling modes when demand of your application is hard to predict. For example, you setup to scale out 20 ECS instances during 13:00 ~ 14:00 everyday, but the actual demand may need more instances, then you can use this scheduled scaling together with other scaling modes to better follow the demand changes.

