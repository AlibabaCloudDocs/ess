# Create an event notification

This topic describes how to create an event notification in a scaling group. After an event of the specified type occurs, Auto Scaling automatically sends a notification to the specified Message Service \(MNS\) topic, MNS queue, or Cloud Monitor.

If you want Auto Scaling to automatically send notifications to an MNS topic or queue, you must create the MNS topic or queue in advance. Make sure that the MNS topic or queue belongs to the same region where the scaling group resides. For more information, see [Create a topic](https://www.alibabacloud.com/help/doc-detail/34424.htm) or [Create a queue](https://www.alibabacloud.com/help/doc-detail/34417.htm).

-   Only a limited number of event notifications can be created in a scaling group. For more information, see [Limits](/intl.en-US/Product Introduction/Limits.md).
-   Receivers in a scaling group must be unique. For example, Cloud Monitor, the same MNS topic, or the same MNS queue cannot be used to receive different event notifications in a scaling group.

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Find the scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   Click **Details** in the **Actions** column.
5.  In the upper part of the page, click the **Event Notifications** tab.

6.  Click **Create Event Notification**.

7.  Configure parameters for the event notification.

    The following table describes the parameters for an event notification.

    |Parameter|Description|
    |---------|-----------|
    |**Notification Method**|Use one of the following notification methods:    -   **CloudMonitor**: If a specific event occurs, a notification is sent to Cloud Monitor. For more information, see [t6167.md\#](/intl.en-US/Event monitoring/System events/View system events.md).
    -   **MNS Topic**: If a specific event occurs, a notification is sent to an MNS topic.
    -   **MNS Queue**: If a specific event occurs, a notification is sent to an MNS queue. |
    |**Event Notification Type**|Choose one or more event notification types based on your requirements. The following section lists the available event notification types:    -   **Successful Scale-out Event**: All ECS instances are added to the scaling group.
    -   **Successful Scale-in Event**: All ECS instances are removed from the scaling group.
    -   **Failed Scale-out Event**: A scale-out event is triggered, but ECS instances are not added to the scaling group.
    -   **Failed Scale-in Event**: A scale-in event is triggered, but ECS instances are not removed from the scaling group.
    -   **Rejected Scaling Activity**: Auto Scaling receives a scaling activity request but rejects it because the trigger conditions are not met.
    -   **Start of Scale-out Event**: A scale-out event is triggered, and ECS instances start to be added to the scaling group.
    -   **Start of Scale-in Event**: A scale-in event is triggered, and ECS instances start to be removed from the scaling group.
    -   **Expiration of Scheduled Task**: If you select this type, notifications are sent on a daily basis for seven days before the scheduled task expires.

If you specify the frequency for the scheduled task, the task expiration time is the last time when the task is executed.

    -   **Partly Successful Scale-out Event**: A scale-out event is triggered, but only some ECS instances are added to the scaling group.
    -   **Partly Successful Scale-in Event**: A scale-in event is triggered, but only some ECS instances are removed from the scaling group. |

8.  Click **OK**.


