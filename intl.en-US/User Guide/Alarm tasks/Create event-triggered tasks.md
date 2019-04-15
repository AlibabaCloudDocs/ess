# Create event-triggered tasks {#concept_och_fzd_sfb .concept}

This section describes how to create and customize event-triggered tasks.

## Procedure {#section_agz_kzd_sfb .section}

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Scaling Tasks** \> **Event-Triggered tasks**.
3.  On the Event-Triggered tasks page, click **Create Event-Triggered Task**.
4.  In the Create Event-Triggered Task dialog box, configure the required options.
    1.  Enter the **Task Name**.
    2.  Enter the Description.
    3.  You must select a group to monitor from the **Resource Monitored** field.
    4.  Select a **Monitoring Type**.
        -   If you select the System Monitoring option, you must select a monitoring metric. For more information about metrics, see [Event-triggered tasks of system monitoring](intl.en-US/User Guide/Alarm tasks/System monitoring alarm tasks.md#).
        -   If you select the Custom Monitoring option, you are required to select the [Group](../../../../../intl.en-US/User Guide/Application groups/Application group overview.md#), [Metric](../../../../../intl.en-US/User Guide/Custom monitoring/Custom monitoring overview.md#) and Metric Type that are predefined in CloudMonitor. For more information about custom metrics, see [Event-triggered tasks of custom monitoring](intl.en-US/User Guide/Alarm tasks/Custom monitoring alarm tasks.md#).
    5.  Select a **Reference Period \(Minutes\)**.

        **Note:** You can select one the following options, such as 1, 2, 5, and 15. Auto Scaling collects, summarizes, and computes data based on the specified reference period. The smaller the granularity, the more easily an event will be triggered. You can select a rational reference period based on your business requirements.

    6.  Configure the **Condition**.

        **Note:** You can set a condition to verify whether the value of a metric exceeds the specified threshold. Assume that the condition is met when the CPU usage rate is higher than 80%.

        -   Average: For all ECS instances in a scaling group, an event will be triggered when the average CPU usage rate is higher than 80%.
        -   Max: In a scaling group, for the ECS instance that has the highest CPU usage rate, an event will be triggered when its usage rage is higher than 80%.
        -   Min: In a scaling group, for the ECS instance that has the lowest CPU usage rate, an event will be triggered when its usage rage is higher than 80%.
    7.  Select a **Trigger After**.

        **Note:** You can select one the following options, such as 1, 2, 3, and 5 times. When the value of a metric exceeds the threshold for specified times, an event is triggered, and the specified scaling rule is applied.

    8.  Select a **Triggered Rule** to be applied when the value of a metric meets the specified condition.
5.  Click **OK**.

