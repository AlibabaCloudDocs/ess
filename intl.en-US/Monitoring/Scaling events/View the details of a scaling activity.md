# View the details of a scaling activity

This topic describes how to view the details of a scaling activity. If a scaling activity is triggered by a scheduled or event-triggered task, you can view the details of the scaling activity to check its execution result.

A scaling activity can have the following states: Rejected, Executing, Successful, Warning, and Failed. For more information, see [t40555.md\#section\_02d\_seh\_4vm](/intl.en-US/Monitoring/Scaling events/Overview.md).

**Note:** During a scaling activity, if some ECS instances fail to be added to a scaling group, Auto Scaling performs rollback on these ECS instances. After the scaling activity is complete, the scaling activity enters the Warning state. For more information, see [t40555.md\#section\_jp3\_qxl\_rxd](/intl.en-US/Monitoring/Scaling events/Overview.md).

## Procedure

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Find the scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   Click **Details** in the **Actions** column.
5.  In the upper part of the page, click the **Scaling Activities** tab.

6.  Find the scaling activity whose details you want to view and click its ID in the **Scaling Activity ID** column.


