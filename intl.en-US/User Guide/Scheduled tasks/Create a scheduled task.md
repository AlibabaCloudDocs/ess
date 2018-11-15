# Create a scheduled task {#concept_25904_zh .concept}

This topic introduces the definition and creation of scheduled tasks.

You can create up to 20 scheduled tasks according to input parameters.

## What is a scheduled task {#section_rx1_hyc_sfb .section}

A scheduled task is a default task that performs a specified scaling rule at a specified time. Thus, it automatically scales up or scales down the computing resources to meet business needs and control costs. You can also specify the repetition cycle for scheduled tasks to respond to the business changes with flexible rules.

**Note:** The number of scheduled tasks that can be created under one account is limited. See [quantity restrictions](reseller.en-US/User Guide/Usage notes/Quantity restrictions.md#).

Since only one scaling activity can exist in a scaling group at a time, the scheduled task also provides automatic retry function to guarantee the scheduled task results in case of single scaling rule performing failure. If more than one scheduled tasks to be performed exist in one minute, Auto Scaling performs the most recently created scheduled task.

## Procedure { .section}

Following these steps to create a scheduled task:

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  Select **Auto-Trigger Tasks**, go to the Scheduled Tasks page, and click **Create Scheduled Task**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40597/154227333932049_en-US.png)

3.  In the Create Scheduled Task dialog box, specify the task name, time to perform, scaling rule, retry expiration time \(optional\), and repetition cycle \(optional\). You can also add a description for later viewing. Click **Submit**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40597/154227333932050_en-US.png)

    **Note:** For the attributes of scheduled tasks, see [scheduled task attributes](#section_jqh_zyc_sfb).


## Scheduled task attribute {#section_jqh_zyc_sfb .section}

|Name|Description|Example|
|:---|:----------|:------|
|Task name|The name must consist of 2-40 characters. It must begin with a lower-case letter, number, or a Chinese character. It can contain ".", "\_", or "-".|st-yk201808301442|
|Description|Describes the purpose, function, and other information of the scheduled task.|The PV is large at the beginning of a month. Add three instances.|
|Time to perform|Time to trigger the scheduled task|00:00, September 2, 2018|
|Scaling rule|The name of the scaling rule, which specifies the scaling action to perform when the task is triggered.|add3|
|Retry expiration time|The time range is 0 seconds ~ 21,600 seconds \(6 hours\). If the scaling action fails to be performed at the specified time, Auto Scaling continues to perform the scheduled task within the retry expiration time.|600|
|Repetition cycle|The repetition cycle to perform the scheduled task. It can be on a daily, weekly, and monthly basis. If different requirements are needed, you can use the [Cron expressions](#section_jw5_jzc_sfb).|By monthPerform on the second to third day each month.

|
|Repetition ending time|The time to stop repeated performing of the scheduled task|00:00, September 30, 2018|

## Cron expressions {#section_jw5_jzc_sfb .section}

The Cron expressions use the UTC + 0 time zone. Eight hours should be added when you convert it into the system local time in China. In addition, the time of the first Cron expression performing must be less than the repetition ending time, otherwise, the scheduled task fails to be created.

A Cron expression is a string separated by spaces. It is divided into five to seven fields. Currently, the Auto Scaling scheduled tasks support five-field Cron expressions, inclluding minutes, hours, days, months, and weeks. The range of values are shown in the following table.

|Field|Required|Valid values|
|:----|:-------|:-----------|
|Minutes|Yes|\[0, 59\]|
|Hours|Yes|\[0, 23\]|
|Days|Yes|\[1, 31\]|
|Months|Yes|\[1, 12\]|
|Weeks|Yes|\[0, 7\]; Sunday = 0 or 7|

You can enter multiple values in a field:

-   Specify multiple values using a comma \(,\). For example, 1, 3, 4, 7, 8.
-   Specify the range of values using "-". For example, 1-6. The result is the same as 1, 2, 3, 4, 5, 6.
-   Specify any possible values using an asterisk \(\*\). For example, an asterisk in the hour field represents each hour, and the result is the same as 0-23.
-   Specify the interval frequency using a slash \(/\). For example, 0-23/2 in the hour field indicates performing every 2 hours. Slashes \(/\) can be used with asterisks \(\*\). For example, \*/3 in the hour field indicates performing every 3 hours.

