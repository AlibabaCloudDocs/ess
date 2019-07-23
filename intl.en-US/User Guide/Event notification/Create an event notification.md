# Create an event notification {#concept_dcl_hhv_lgb .concept}

This topic describes the limits and procedure for creating event notifications.

## Limits {#section_oz1_d2g_mgb .section}

-   You can create a limited number of event notifications at the same time. For more information, see [Quantity limits](reseller.en-US/User Guide/Usage notes/Quantity limits.md#).
-   A receiver in a scaling group must be unique. For example, CloudMonitor, a specific MNS topic, or a specific MNS queue cannot be repeatedly used for different event notifications of a scaling group.
-   You must create an MNS topic or MNS queue before using it, and ensure the topic or queue is in the same region as the scaling group.

## Create an event notification by using the console {#section_ydl_rjv_lgb .section}

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  In the **Actions** column corresponding to a scaling group, click **Manage**.
3.  In the left-side navigation pane, click **Event Notifications**.
4.  On the Event Notifications page that appears, click **Create Notification**.
5.  In the Create Notification dialog box that appears, set parameters for creating an event notification.
    1.  Set **Notification Method**.

        |Method|Description|
        |------|-----------|
        |CloudMonitor|If a specific event occurs, an event notification is sent to CloudMonitor. For more information, see [Cloud service system event monitoring](../../../../reseller.en-US/User Guide/Event monitoring/Cloud product events/View cloud service events.md#).|
        |MNS Topic|If a specific event occurs, a message is pushed to an MNS topic.|
        |MNS Queue|If a specific event occurs, a message is pushed to an MNS queue.|

    2.  Configure **Event Types**.

        You can select multiple types.

        |Type|Description|
        |----|-----------|
        |Successful Scale-Outs|An ECS instance is added to the scaling group.|
        |Successful Scale-Ins|An ECS instance is removed from the scaling group.|
        |Failed Scale-Outs|Scale-out activities were triggered but ECS instances failed to be added to the scaling group.|
        |Failed Scale-Ins|Scale-in activities were triggered but ECS instances failed to be removed from the scaling group.|
        |Rejected Scaling Activities|The scaling group received the scaling request but rejected the request because the triggering conditions are not met.|
        |The scale-out activities for the specified scaling group are running|Scale-out activities were triggered and ECS instances are being added to the scaling group.|
        |The scale-in activities for the specified scaling group are running|Scale-in activities were triggered and ECS instances are being removed from the scaling group.|
        |Scheduled Task Expirations|If you select this type, notifications on expiring scheduled tasks of the scaling group will be sent on a daily basis seven days before the task expires. **Note:** If a scheduled task has a recurring cycle, the task expiration time is the last time the task will be executed.

 |

        **Note:** A successful scaling activity can be partially or completely successful. To determine whether a scaling activity is partially or completely successful, you can view the scaling detail in the event notification for the activity.

6.  Click **Create Notification**.

