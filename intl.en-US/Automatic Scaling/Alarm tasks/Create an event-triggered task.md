# Create an event-triggered task

This topic describes how to create an event-triggered task associated with a CloudMonitor metric in response to emergent or unpredictable business changes. After you create and enable an event-triggered task in a scaling group, Auto Scaling collects data for the specified metric in real time and triggers an alert when the specified condition is met. Then, Auto Scaling executes the specified scaling rule to dynamically scale ECS instances in the scaling group.

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Scaling Tasks** \> **Event-Triggered Tasks**.

3.  In the top navigation bar, select a region.

4.  Select a monitoring type for the event-triggered task.

    -   If you want to use metrics defined by the system, click the **System Monitoring** tab.
    -   If you want to use custom metrics, click the **Custom Monitoring** tab.
5.  Click **Create Event-triggered Task**.

6.  In the dialog box that appears, configure parameters for the event-triggered task.

    1.  Enter a task name.

        The name must be 2 to 64 characters in length, and can contain periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter or a digit.

    2.  Enter a task description.

    3.  Select the resource to be monitored.

        The resource to be monitored is a scaling group.

    4.  Configure monitoring information based on the monitoring type.

        -   System monitoring event-triggered task: You must select a metric defined by the system. For information about metrics supported by the system, see [Event-triggered tasks for system monitoring](/intl.en-US/Automatic Scaling/Alarm tasks/Event-triggered tasks for system monitoring.md).
        -   Custom monitoring event-triggered task: You must select an application group, a metric, and a dimension that are preconfigured in CloudMonitor. For information about how to use custom metrics, see [Custom monitoring event-triggered tasks](/intl.en-US/Automatic Scaling/Alarm tasks/Custom monitoring event-triggered tasks.md).
    5.  Set the reference period.

        You can set the reference period to **1 Minute**, **2 Minutes**, **5 Minutes**, or **15 Minutes**. Auto Scaling collects, summarizes, and compares data based on the specified reference period. The shorter the reference period is, the more frequently alerts are triggered. Set the reference period based on your business requirements.

    6.  Configure the condition.

        The condition is a rule that specifies whether the CloudMonitor metric value exceeds the threshold range. You can specify the condition based on the average, minimum, or maximum value. For example, if you want alerts to be triggered when the CPU utilization exceeds 80%, you can configure the condition by using one of the following methods:

        -   Average: Alerts are triggered when the average CPU utilization of all the ECS instances in the scaling group exceeds 80%.
        -   Maximum: Alerts are triggered when the highest CPU utilization of all the ECS instances in the scaling group exceeds 80%.
        -   Minimum: Alerts are triggered when the lowest CPU utilization of all the ECS instances in the scaling group exceeds 80%.
    7.  Specify the number of times that the condition is met before an alert is triggered.

        Auto Scaling counts the number of times that the condition is met. When the number of times that the condition is met reaches the value of Trigger After, Auto Scaling triggers an alert and executes the scaling rule specified in the event-triggered task.

    8.  Set the trigger rule.

        Select the scaling rule to be executed when the condition is met for the specified number of times. You can select only a scaling rule that belongs to the monitored scaling group.

7.  Click **OK**.


