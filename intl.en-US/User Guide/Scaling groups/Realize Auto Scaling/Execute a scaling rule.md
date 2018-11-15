# Execute a scaling rule {#concept_rxw_2bx_rfb .concept}

This topic introduces how to perform a scaling rule.

After [creating a scaling rule](reseller.en-US/User Guide/Scaling groups/Realize Auto Scaling/Create a scaling rule.md#), you have successfully created a scaling rule, and then you can perform a scaling rule to scale up or scale down ECS resources.

## Limits {#section_bpw_hbx_rfb .section}

If you need to perform a scaling rule, note the following:

-   The status of the scaling group which the scaling rule belongs to must be `Enabled`.
-   No scaling activities in progress are in the scaling group which the scaling rule belongs to.
-   For all regions and all scaling groups, the number of ECS instances to be scaled for each account is limited. See [quantity restrictions](reseller.en-US/User Guide/Usage notes/Quantity restrictions.md#).

Currently, you can perform a scaling rule in three ways:

-   [Through scheduled tasks](#section_qhr_lbx_rfb).
-   [Through alarm tasks](#section_rgw_fcx_rfb).
-   [By performing manually](#section_ovq_3cx_rfb).

## Through scheduled tasks {#section_qhr_lbx_rfb .section}

Select a scaling rule when you [create a scheduled task](reseller.en-US/User Guide/Scheduled tasks/Create a scheduled task.md#). Auto Scaling automatically performs the scaling rule at the specified time point.

## Through alarm tasks {#section_rgw_fcx_rfb .section}

Select an alarm trigger rule when you create an alarm task. Auto Scaling automatically performs the scaling rule when the alarm is triggered.

## By performing manually {#section_ovq_3cx_rfb .section}

When no scaling activities in progress are in the scaling group, you can skip [cool-down time](reseller.en-US/User Guide/Usage notes/Cool-down time.md#) by performing the scaling rule manually. Follow these steps to manually perform a scaling rule:

1.  In the Scaling Rules page, click **Perform** in the **Actions** column.
2.  In the Perform Scaling Rule dialog box, click **OK**.
3.  If the scaling rule is performed successfully, a prompt appears in the upper-right corner of the page.

    If the scaling rule fails to be performed, an error prompt appears.

4.  You can go to the Scaling Activities page to view the result of scaling rule performing.

