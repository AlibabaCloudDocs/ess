# Execute a scaling rule {#concept_rxw_2bx_rfb .concept}

This topic describes how to execute scaling rules either manually or automatically to scale ECS instances.

## Prerequisites {#section_bpw_hbx_rfb .section}

Before you execute a scaling ruling, note that:

-   The status of the scaling group to which the scaling rule belongs is in the **Active** state.
-   The scaling group to which the scaling rule belongs is not undergoing any scaling activities.
-   Target tracking scaling rules can only be executed by alert tasks that were automatically created. For more information, see [Create a scaling rule](reseller.en-US/User Guide/Realize Auto Scaling/Create a scaling rule.md#).
-   There is no limit to the maximum number of ECS instances that a scaling group can have. However, the limits on ECS instance usage apply to Auto Scaling. For more information, see [Limits](../../../../reseller.en-US/Product Introduction/Limits.md#).

## Manually execute a scaling rule {#section_ovq_3cx_rfb .section}

If you need to scale ECS instances temporarily, you can manually execute a scaling rule.

**Note:** If the scaling group is not undergoing any scaling activities, you can immediately execute the scaling rule without the need to wait for the [cooldown period](reseller.en-US/User Guide/Usage notes/Cool-down time.md#) to expire.

1.  On the Scaling Rules page, click **Execute** in the **Actions** column corresponding to the scaling rule that you want to execute.
2.  In the Run Scaling Rule message that appears, click **OK**.
3.  If the scaling rule is executed, a prompt appears in the upper-right corner of the page.

    ![](images/21704_en-US.png)

    If the scaling rule fails to be executed, an error message appears in the center of the page.

    ![](images/21705_en-US.png)

4.  You can go to the Scaling Activities page to view the results of the scaling rule execution.

## Execute a scaling rule by using a scheduled task {#section_qhr_lbx_rfb .section}

There are services that use ECS instances on a regular basis. For these services, you can specify a scaling rule when you [create a scheduled task](reseller.en-US/User Guide/Realize Auto Scaling/Scheduled tasks/Create a scheduled task.md#). Then, Auto Scaling executes this scaling rule at the scheduled points in time.

![](images/21700_en-US.png)

## Execute a scaling rule by using an alert task {#section_rgw_fcx_rfb .section}

There are services that do not use ECS instances on a regular basis. For these services, you can specify a scaling rule when you [create an alert task](reseller.en-US/User Guide/Realize Auto Scaling/Alarm tasks/Create event-triggered tasks.md#). Then, Auto Scaling automatically executes this scaling rule when the conditions specified in the alert task are met.

Alert tasks include system monitoring alert tasks and custom monitoring alert tasks, which meet monitoring requirements in different scenarios. For more information, see [Auto Scaling alert tasks](reseller.en-US/User Guide/Realize Auto Scaling/Alarm tasks/Auto Scaling alarm tasks.md#).

![Set a system monitoring alert task](images/21701_en-US.png)

![Set a custom monitoring alert task](images/21702_en-US.png)

