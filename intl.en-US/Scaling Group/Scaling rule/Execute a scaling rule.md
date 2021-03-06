# Execute a scaling rule

This topic describes how to manually or automatically execute a scaling rule to scale ECS instances.

-   You have no overdue payments within your account.

    **Note:** If you have overdue payments within your account, all scaling activities fail to be executed. Make sure that you have sufficient balance within your account to ensure the service availability of Auto Scaling.

-   The scaling group to which the scaling rule belongs is in the **Enabled** state.
-   No scaling activity is in progress in the scaling group to which the scaling rule belongs.

For information about the limits on the number of ECS instances in a scaling group, see [Limits](/intl.en-US/Product Introduction/Limits.md).

## Manually execute a scaling rule

If you want to temporarily scale ECS instances, you can manually execute a scaling rule.

**Note:** If the scaling group has no scaling activities in progress, you can immediately execute the scaling rule without the need to wait for the cooldown time to expire.

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Find the scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   Click **Details** in the **Actions** column.
5.  In the upper part of the page, click the **Scaling Rules** tab.

6.  Find the scaling rule and click **Execute** in the **Actions** column.

7.  In the message that appears, click **OK**.


## Execute a scaling rule by using a scheduled task

If your business uses ECS instances on a regular basis, you can create a scheduled task to execute a scaling rule. Auto Scaling automatically executes the scaling rule at the specified time of point. For more information, see [Create a scheduled task](/intl.en-US/Automatic Scaling/Scheduled tasks/Create a scheduled task.md).

## Execute a scaling rule by using an event-triggered task

If your business does not use ECS instances on a regular basis, you can create an event-triggered task to execute a scaling rule. When the specified condition is met, Auto Scaling automatically executes the scaling rule. For more information, see [Create event-triggered tasks](/intl.en-US/Automatic Scaling/Alarm tasks/Create a monitoring task.md). For more information about event-triggered tasks, see [Event-triggered task overview](/intl.en-US/Automatic Scaling/Alarm tasks/Event-triggered task overview.md).

**Note:** A target tracking scaling rule can be triggered only by the associated event-triggered task. For more information, see [Create a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Create a scaling rule.md).

