# Create a scheduled task

This topic describes how to create a scheduled task to scale computing resources in response to predictable business changes in the future. Scheduled tasks enable the system to obtain sufficient computing resources before business peaks and release idle computing resources after business peaks.

A scheduled task is preconfigured to execute the specified scaling rule at the specified time. When the specified time arrives, the scheduled task automatically scales computing resources. This allows you to reduce costs and meet business requirements. You can also specify the recurrence for scheduled tasks to respond to business changes based on flexible rules.

**Note:** You can create only a limited number of scheduled tasks within an Alibaba Cloud account. For more information, see [Limits](/intl.en-US/Product Introduction/Limits.md).

You can set the retry interval at which a scheduled task is automatically retried to ensure that the scheduled task is executed in a timely manner. If multiple scheduled tasks are to be executed in 1 minute, Auto Scaling executes the scheduled task that is most recently created.

## Procedure

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Scaling Tasks** \> **Scheduled Tasks**.

3.  In the top navigation bar, select a region.

4.  Click **Create Scheduled Task**.

5.  In the dialog box that appears, configure parameters for the scheduled task.

    1.  Enter a task name.

        The name must be 2 to 64 characters in length. It must start with a letter or a digit. It can contain periods \(.\), underscores \(\_\), and hyphens \(-\).

    2.  Enter a description.

        You can enter the details about the scheduled task, such as its purpose and function.

    3.  Set the time to execute the scheduled task.

        The scheduled task is triggered when the specified time arrives.

    4.  Select a scaling group.

    5.  Set the scaling method.

        -   **Select Existing Scaling Rule**: Select an existing scaling rule in the scaling group. The scaling rule is executed when the scheduled task is triggered.

            **Note:** Scheduled tasks can execute only simple scaling rules.

        -   **Configure Number of Instances in Scaling Group**: Enter the minimum, maximum, and expected numbers of instances in the scaling group. When the scheduled task is triggered, its settings overwrite those of the scaling group.

            **Note:** If the Expected Number of Instances feature is disabled when a scaling group is created, you can specify only the minimum and maximum numbers of instances in the scaling group.

    6.  Set the retry interval.

        The value ranges from 0 to 21600, in seconds. If a scaling activity fails to be executed at the specified time, Auto Scaling executes the scheduled task again within the retry interval.

    7.  Set the recurrence period.

        You can configure the scheduled task to be repeatedly executed

        -   on a daily, weekly, or monthly basis. You can also use a cron expression to specify complex recurrence settings. For information about cron expressions, see [Cron expressions](#section_xyx_exw_poc).
        -   The recurrence end time must be later than the first execution time of the scheduled task.
6.  Click **OK**.


## Cron expressions

A cron expression is a string that represents a schedule. The string consists of multiple fields that are separated by spaces and describe individual details of the schedule. A scheduled task supports a cron expression that consists of five fields in the `X X X X X` format. `X` indicates a placeholder for a field. Each field in a cron expression represents minutes, hours, day of month, month, and day of week. Each field can be a definite value or a special character that has logical meaning.

When you configure a cron expression for a scheduled task, take note of the following items:

-   Cron expressions are in UTC. When you configure a cron expression, you must convert the local time to UTC. For example, the time in China is in UTC+8. If you want to execute your task at 20:00 every day in China, you must subtract 8 hours from the scheduled execution time. In this case, you must set the cron expression to `0 12 * * ?`.
-   A single scheduled task that has a specified cron expression can be executed only once per hour.
-   If the Day or Week field is specified, the other field must be set to a question mark \(`?`\) to avoid conflicts.

|Field|Required|Value range|Special character|
|:----|:-------|:----------|-----------------|
|Minute|Yes|0‒59|, - / \*|
|Hour|Yes|0‒23|, - / \*|
|Day|Yes|1‒31|, - / \* ? L W|
|Month|Yes|1‒12|, - / \*|
|Week|Yes|1‒7. The value for Sunday is 7.|, - \* ? / L \#|

|Special character|Description|Example|
|-----------------|-----------|-------|
|`*`|Indicates all possible values.|In the Month field, an asterisk \(`*`\) indicates every month. In the Week field, an asterisk \(`*`\) indicates every day of a week.|
|`,`|Lists enumerated values.|In the Minute field, `5,20` indicates the fifth minute and the twentieth minute.|
|`-`|Indicates a range.|In the Minute field, `5-20` indicates that the task is triggered once every minute from the 5th to 20th minute.|
|`/`|Indicates increments.|In the Minute field, `0/15` indicates every 15 minutes from the zeroth minute. `3/20` indicates every 20 minutes from the third minute.|
|`?`|Indicates an unspecified value. Only the Day and Week fields support this character. **Note:** If the Day or Week field is specified, the other field must be set to a question mark \(`?`\) to avoid conflicts.

|In the Day field, `?` indicates that no date is specified. In the Week field, `?` indicates that the day of the week is not specified. For example, `15 10 15 * ?` indicates that the scheduled task is executed at 10:15 on the fifteenth day of each month, regardless of the day of a week.|
|`L`|Indicates last. Only the Day and Week fields support this character. **Note:** To avoid logic errors, do not specify a list or range when you use the `L` character.

|-   In the Day field, `L` indicates the last day of a month. In the Week field, `L` indicates the last day of a week, which is Sunday.
-   `L` can be preceded by a value. For example, `6L` in the Week field indicates the last Saturday of a month. |
|`W`|The weekday nearest to the specified day of the month. The weekday that the `W` character finalizes on is in the same month as the given day. `LW` indicates the last weekday of the specified month.|If `5W` is specified in the Day field and the fifth day of the month falls on Saturday, the task is triggered on the nearest weekday Friday, which is the fourth day of the month. If the fifth day of the month falls on Sunday, the scheduled task is triggered on the nearest weekday Monday, which is the sixth day of the month. If the fifth day of the month falls on a weekday, the scheduled task is triggered on the 5th day of the month.|
|`#`|A specific day of a specific week in every month. Only the Week field supports this character. Valid values: 1 to 5.|In the Week field, `4#2` indicates the second Thursday of a month.|

|Example|Description|
|-------|-----------|
|`15 10 ? * *`|Executes the scheduled task at 10:15 every day.|
|`0 12 * * ?`|Executes the scheduled task at 12:00 every day.|
|`0 10,14,16 * * ?`|Executes the scheduled task at 10:00, 14:00, and 16:00 every day.|
|`15 10 15 * ?`|Executes the scheduled task at 10:15 on the 15th day of every month.|
|`15 10 L * ?`|Executes the scheduled task at 10:15 on the last day of every month.|
|`15 10 ? * 6L`|Executes the scheduled task at 10:15 on the last Saturday of every month.|
|`15 10 ? * 6#3`|Executes the scheduled task at 10:15 on the third Saturday of every month.|

