# Manage event notifications {#concept_qdn_dqv_lgb .concept}

This topic describes how to manage event notifications, such as viewing notification method details, modifying notification types, and deleting notifications.

## View notification method details {#section_rxg_qqv_lgb .section}

In the Auto Scaling console, you can click links to navigate to the CloudMonitor and Message Service pages. The pages show the notifications received for the relevant services.

1.  Log on to the[Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  In the**Actions** column corresponding to a scaling group, click**Manage**.
3.  In the left-side navigation pane, click**Event Notifications**.
4.  On theEvent Notifications page that appears, click the link in the**Notification Method** column corresponding to an event notification.

    **Note:** If the method is CloudMonitor,**CloudMonitor** is displayed in the column. If the method is MNS Topic or MNS Queue, the topic or queue name is displayed in the column.


## Modify event notification types by using the console {#section_y1f_drv_lgb .section}

**Note:** The notification type of a created event notification cannot be modified.

1.  Log on to the[Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  In the**Actions** column corresponding to a scaling group, click**Manage**.
3.  In the left-side navigation pane, click**Event Notifications**.
4.  On theEvent Notifications page that appears, click**Edit** in the**Actions** column corresponding to an event notification.
5.  In theEdit Notification dialog box that appears, modify**Notification Types**.
6.  Click**Edit Notification**.

## Modify event notification types by using an API {#section_nbb_jkh_mgb .section}

You can call[ModifyNotificationConfiguration](../../../../reseller.en-US/API-Reference/Event notification/ModifyNotificationConfiguration.md#) to modify notification types of an event notification. Before modifying notification types, you can call[DescribeNotificationConfigurations](../../../../reseller.en-US/API-Reference/Event notification/DescribeNotificationConfigurations.md#) to view event notification details.

## Delete an event notification by using the console {#section_qkn_drv_lgb .section}

1.  Log on to the[Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  In the**Actions** column corresponding to a scaling group, click**Manage**.
3.  In the left-side navigation pane, click**Event Notifications**.
4.  On theEvent Notifications page that appears, click**Delete** in the**Actions** column corresponding to an event notification.
5.  In theDelete Notification message that appears, click**OK**.

## Delete an event notification by using an API {#section_u5w_wkh_mgb .section}

You can call[DeleteNotificationConfiguration](../../../../reseller.en-US/API-Reference/Event notification/DeleteNotificationConfiguration.md#) to delete an event notification. Before deleting an event notification, you can call[DescribeNotificationConfigurations](../../../../reseller.en-US/API-Reference/Event notification/DescribeNotificationConfigurations.md#) to view event notification details.

