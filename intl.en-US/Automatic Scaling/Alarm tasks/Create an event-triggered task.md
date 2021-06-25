# Create an event-triggered task

This topic describes how to create an event-triggered task associated with a CloudMonitor metric in response to emergent or unpredictable business changes. After you create and enable an event-triggered task, Auto Scaling collects data for the specified metric in real time and triggers an alert when the specified condition is met. Then, Auto Scaling executes the scaling rule that is specified in the event-triggered task to dynamically scale ECS instances in the scaling group during the effective period of the event-triggered task.

## Procedure

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Scaling Tasks** \> **Event-Triggered Tasks**.

3.  In the top navigation bar, select a region.

4.  Select a monitoring type for the event-triggered task.

    -   If you want to use metrics defined by the system, click the **System Monitoring** tab.
    -   If you want to use custom metrics, click the **Custom Monitoring** tab.
5.  Click **Create Event-triggered Task**.

6.  In the dialog box that appears, configure parameters for the monitoring task.

    1.  Enter a task name.

        The name must be 2 to 64 characters in length and can contain periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter or a digit.

    2.  Enter a task description.

    3.  Select the resource to be monitored.

        The resource to be monitored is a scaling group.

    4.  Configure monitoring information based on the monitoring type.

        -   System monitoring event-triggered task: You must select a metric defined by the system. For information about metrics supported by the system, see [Event-triggered tasks for system monitoring](/intl.en-US/Automatic Scaling/Alarm tasks/Event-triggered tasks for system monitoring.md).
        -   Custom monitoring event-triggered task: You must select an application group, a metric, and a dimension that are preconfigured in CloudMonitor. For more information about how to use custom metrics, see [Custom monitoring event-triggered tasks](/intl.en-US/Automatic Scaling/Alarm tasks/Custom monitoring event-triggered tasks.md).
    5.  Set the reference period.

        You can set the reference period to **1 Minute**, **2 Minutes**, **5 Minutes**, or **15 Minutes**. Auto Scaling collects, summarizes, and compares data based on the specified reference period. The shorter the reference period is, the more frequently alerts are triggered. Set the reference period based on your business requirements.

    6.  Configure the condition.

        The condition is a rule that specifies whether the CloudMonitor metric value exceeds the threshold range. You can specify the condition based on the average, minimum, or maximum value. For example, if you want alerts to be triggered when the CPU utilization exceeds 80%, you can configure the condition by using one of the following methods:

        -   Average: Alerts are triggered when the average CPU utilization of all the ECS instances in the scaling group exceeds 80%.
        -   Maximum: Alerts are triggered when the highest CPU utilization of all the ECS instances in the scaling group exceeds 80%.
        -   Minimum: Alerts are triggered when the lowest CPU utilization of all the ECS instances in the scaling group exceeds 80%.
    7.  Specify the number of times that the condition is met before an alert is triggered.

        Auto Scaling counts the number of times that the condition is met. When the number reaches the value of Trigger After, Auto Scaling triggers an alert and executes the scaling rule specified in the event-triggered task.

    8.  Set the effective period.

        During the effective period, Auto Scaling executes the scaling rule specified in the event-triggered task when alerts are triggered. If alerts are triggered beyond the effective period, Auto Scaling does not execute the scaling rule.

        -   Not Set: The event-triggered task is effective all the time.
        -   Cron Expression: The event-triggered task is effective only within the time range specified by the cron expression. For information about cron expressions, see [Cron expressions](#section_0rg_6a5_cw7).
    9.  Set the trigger rule.

        Select the scaling rule to be executed when the condition is met for the specified number of times. You can select only a scaling rule that belongs to the monitored scaling group.

7.  Click **OK**.


## Cron expressions

A cron expression is a string that represents a schedule. The string consists of multiple fields that are separated by spaces and describe individual details of the schedule. An event-triggered task supports a cron expression that consists of five fields in the `X X X X X` format. `X` indicates a placeholder for a field. Each field in a cron expression represents seconds, minutes, hours, day of month, and months. Each field can be a definite value or a special character that has logical meaning.

**Note:** Cron expressions are in UTC. When you configure a cron expression, you must convert the local time to UTC. For example, the time in China is in UTC+8. If you want to execute your task between 01:00 and 02:59 every day in China, you must subtract 8 hours from the scheduled execution time. In this case, you must set the cron expression to `* * 17-18 * *`.

|Field|Required|Value range|Special character|
|:----|:-------|:----------|-----------------|
|Second|Yes|0~59|, - / \*|
|Minute|Yes|0~59|, - / \*|
|Hour|Yes|0~23|, - / \*|
|Day|Yes|1~31|, - / \* L W|
|Month|Yes|1~12|, - / \*|

|Special characters|Description|Example|
|------------------|-----------|-------|
|`*`|Indicates all possible values.|In the Month field, an asterisk \(`*`\) indicates every month.|
|`,`|Lists enumerated values.|In the Minute field, `5,20` indicates the fifth minute and the twentieth minute.|
|`-`|Indicates a range.|In the Minute field, `5-20` indicates that the task is triggered once every minute from the 5th to 20th minute.|
|`/`|Indicates increments.|In the Minute field, `0/15` indicates every 15 minutes starting from the zeroth minute. `3/20` indicates every 20 minutes from the third minute.|
|`L`|Indicates last. Only the Day field supports this character. **Note:** To avoid logic errors, do not specify a list or range when you use the `L` character.

|In the Day field, `L` indicates the last day of a month.|
|`W`|The weekday nearest to the specified day of the month. The weekday that the `W` character finalizes on is in the same month as the given day.|If `5W` is specified in the Day field and the fifth day of the month falls on Saturday, the event-triggered task is effective on the nearest weakday Friday, which is the fourth day of the month. If the fifth day of the month falls on Sunday, the event-triggered task is effective on the nearest weekday Monday, which is the sixth day of the month. If the fifth day of the month falls on a weekday, the event-triggered task is effective on the fifth day of the month.|

|Example|Description|
|-------|-----------|
|`* * * * *`|Is effective all the time.|
|`* 0-30 1-2 * *`|Is effective between 01:00 and 01:30 and between 02:00 and 02:30 every day.|
|`* * 0,2 * *`|Is effective between 00:00 and 00:59 and between 02:00 and 02:59 every day.|
|`* * 1 1/2 *`|Is effective between 01:00 and 01:59 every two days staring from the first day of each month. For example, the first two effective time ranges of each month are between 01:00 and 01:59 on the first day of each month and between 01:00 and 01:59 on the third day of each month.|
|`* * 1 L *`|Is effective between 01:00 and 01:59 on the last day of each month.|
|`* * 1 5W *`|Is effective on different days based on whether the fifth day of each month is a weekday:-   If the fifth day of a month is a weekday between Monday and Friday, the event-triggered task is effective between 01:00 and 01:59 on the fifth day of the month.
-   If the fifth day of a month is Saturday, the event-triggered task is effective between 01:00 and 01:59 on the fourth day of the month.
-   If the fifth day of a month is Sunday, the event-triggered task is effective between 01:00 and 01:59 on the sixth day of the month. |

