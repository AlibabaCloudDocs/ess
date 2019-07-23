# Event notification overview {#concept_zsh_vdg_mgb .concept}

The event notification feature is a monitoring method that can automatically send messages to CloudMonitor or Message Service \(MNS\), providing you with timely information on scaling groups and improving automated management.

## Event notification methods {#section_bxp_42g_mgb .section}

Event notification methods include sending messages to CloudMonitor system events, MNS topics, and MNS queues.

In CloudMonitor, you can query and view statistics on system events of various cloud services, such as Auto Scaling. You can also obtain up-to-date information about scaling groups For more information about the event monitoring feature of CloudMonitor, see [Cloud service system event monitoring](../../../../reseller.en-US/User Guide/Event monitoring/Cloud product events/View cloud service events.md#).

There are two service models in Message Service: MNS topic and MNS queue. Message Service is a distributed message service that helps you easily transfer data and notification messages among distributed components, and build loosely coupled systems. For more information about the functions of MNS topics and MNS queues, see [Message Service overview](https://partners-intl.aliyun.com/help/doc-detail/27414.htm).

-   The queue model supports point-to-point sending and receiving of messages. It is designed to deliver a highly reliable and concurrent consumption model in a point-to-point manner. Each message in a queue can only be consumed by a single consumer.
-   The topic model supports one-to-many publishing and subscribing of messages. It is designed to provide publishing-subscribing and notification capabilities in a one-to-many manner. The model also allows you to publish messages in various ways.

The following section provides examples of each event notification method. For more information about parameter details, see [Create an event notification](reseller.en-US/User Guide/Event notification/Create an event notification.md#).

## Example: event notifications through CloudMonitor {#section_vqd_tjv_lgb .section}

You have created an event notification in which Notification Method is set to **CloudMonitor** and Event Types to **Successful Scale-Outs** and **The scale-out activities for the specified scaling group are running**. After a scale-out activity of a scaling group succeeds, CloudMonitor receives an event notification and displays the event. The following figure shows the notification result after the scale-out activity succeeds. Two events are displayed in the results, including **The scale-out activities for the specified scaling group are running** and **The scale-out activities for the specified scaling group are completed**.

In the [CloudMonitor console](https://partners-intl.console.aliyun.com/#/cms), you can view the status of scaling groups and [create an alarm rule](../../../../reseller.en-US/User Guide/Alarm service/Alarm rules/Manage alarm rules.md#) to notify multiple alarm contacts through SMS messages and emails, improving operation and maintenance efficiency.

## Example: event notifications through an MNS topic {#section_rrv_tjv_lgb .section}

You have created an event notification in which Notification Method is set to **MNS Topic**, and Event Types to **Successful Scale-Ins** and **The scale-in activities for the specified scaling group are running**. After a scale-in activity of a scaling group succeeds, the MNS topic receives an event notification and sends it to its subscribers. The following figure shows the notification result after the scale-in activity succeeds. The number displayed in the **Messages** column corresponding to the MNS topic has increased. You can view the subscribers for message details.

The MNS topic does not allow direct consumption of messages. You must subscribe to the MNS topic through an MNS queue, HTTP request, or email. When the MNS topic receives a message, it pushes the message to subscribers. In this way, multiple subscribers separately consume messages from the same publisher, achieving efficient automated management.

## Example: event notifications through an MNS queue {#section_ecw_tjv_lgb .section}

You have created an event notification in which Notification Method is set to **MNS Queue**, and Event Types to **Failed Scale-Outs** and **The scale-out activities for the specified scaling group are running**. After a scale-out activity for a scaling group fails, the MNS queue receives an event notification and allows you to configure the messages for consumption. The following figure shows the notification result after the scale-out activity fails. The number displayed in the **Active Message** column corresponding to the MNS topic has increased.

You can consume, delay, activate or delete the messages as needed, achieving automated management through event notifications.

