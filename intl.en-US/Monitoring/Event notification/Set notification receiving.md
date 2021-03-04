# Set notification receiving

This topic describes how to receive notifications about scaling activitiesby using internal messages and emails.

No event notifications are created.

You can use internal messages and emails to receive notifications.You must handle the notifications on your own after you receive them.

You can also use the event notification feature to configure events related to Auto Scaling to be automatically sent to Cloud Monitor or Message Service \(MNS\). For more information, see [Event notification overview](/intl.en-US/Monitoring/Event notification/Event notification overview.md). After you customize handling policies in these services, these services can initiate handling processes after the event notifications are received.

**Note:** If you have created event notifications, you cannot set notification receiving. To set notification receiving, you must delete all event notifications.

## Procedure

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Find the scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   Click **Details** in the **Actions** column.
5.  In the upper part of the page, click the **Event Notifications** tab.

6.  Click **Set Notification Receiving**.

7.  Configure the notification method and contact.

    1.  In the **Set Notification Receiving** dialog box, click **Learn more**.

    2.  On the **Common Settings** page, find **Notifications Regarding the Creation and Activation of Product Instances** in the **Product Message** section and configure the notification method and contact.

        ![msg-center](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0213224061/p168985.png)

8.  Go back to the **Set Notification Receiving** dialog box, select the scenarios where notifications are sent, and then click **OK**.

    You can configure notifications for the following scaling scenarios:

    -   **Scaling Activity Success**: Auto Scaling adds or removes ECS instances to or from the scaling group.
    -   **Scaling Activity Failed**: A scaling activity is triggered, but Auto Scaling fails to add or remove ECS instances to or from the scaling group.
    -   **Scaling Activity Rejected**: The request of a scaling activity is received but rejected because the trigger conditions are not met.

