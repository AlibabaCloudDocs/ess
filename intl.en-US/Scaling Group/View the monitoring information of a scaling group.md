# View the monitoring information of a scaling group

You can view the monitoring charts of a scaling group. This helps you understand the resource usage of the scaling group within a month.

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  Go to the **Monitoring Details** page of the scaling group.

    1.  In the left-side navigation pane, click **Scaling Groups**.

    2.  In the top navigation bar, select a region.

    3.  Find the scaling group and use one of the following methods to open the details page of the scaling group:

        -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
        -   Click **Details** in the **Actions** column.
    4.  In the upper part of the page, click the **Monitoring Details** tab.

3.  Select the time range of the monitoring charts.

    ![Configure the time range](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8196292161/p206881.png)

    -   Time range: You can select 1 Hour, 6 Hours, 12 Hours, 1 Day, or 1 Week, or specify a time period within a month.
    -   Auto refresh: If you turn on **Auto Refresh**, the system automatically refreshes the monitoring data every 5 seconds.
4.  View the monitoring charts.

    The following figure shows the CPU, Memory, and Load Metrics monitoring charts.

    ![Charts](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8196292161/p207369.png)

    -   You can click a monitoring dimension such as Average or Maximum in the upper part of the monitoring chart to hide or show relevant data in the chart.
    -   You can click the ![Zoom in](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8196292161/p206799.png) icon in the chart to enlarge the current chart. You can also select a time range in the enlarged chart to view data of that time period.
    -   If a monitoring chart has no data, you have not created an event-triggered task for the corresponding metric. Create an event-triggered task as prompted. For more information, see [Create event-triggered tasks](/intl.en-US/Automatic Scaling/Alarm tasks/Create a monitoring task.md).

