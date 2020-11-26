# FAQ about event-triggered tasks and scheduled tasks

This topic provides answers to commonly asked questions about event-triggered tasks and scheduled tasks.

-   [Can I create tasks that are executed periodically?](#section_3s6_peo_yf6)
-   [What conditions are used by event-triggered tasks to trigger scaling activities?](#section_vmd_inq_1ug)
-   [How do I configure conditions for event-triggered tasks?](#section_aah_1sk_dyk)
-   [How do I use event-triggered tasks to delete instances created by Auto Scaling?](#section_isj_t30_bbm)
-   [Does Auto Scaling support automatic scaling based on custom Cloud Monitor metrics?](#section_1ag_12s_rjg)
-   [Which is prioritized to be executed: an event-triggered task or a scheduled task?](#section_kql_ahe_ij5)
-   [Does Auto Scaling support automatic scaling of data disks?](#section_1gg_n38_ldi)

## Can I create tasks that are executed periodically?

Yes, you can create scheduled tasks that are executed periodically. For more information, see [Create a scheduled task](/intl.en-US/Automatic Scaling/Scheduled tasks/Create a scheduled task.md).

## What conditions are used by event-triggered tasks to trigger scaling activities?

Event-triggered tasks can trigger scaling activities based on Cloud Monitor metrics such as the CPU utilization, memory usage, average system load, and inbound or outbound traffic.

## How do I configure conditions for event-triggered tasks?

Before you configure conditions for event-triggered tasks, you must install the latest version of Cloud Monitor on your Elastic Compute Service \(ECS\) instances. For more information, see [Install the Cloud Monitor Java agent]().

Then, you can select required conditions when you create event-triggered tasks. For more information, see [Create event-triggered tasks](/intl.en-US/Automatic Scaling/Alarm tasks/Create a monitoring task.md).

## How do I use event-triggered tasks to delete instances created by Auto Scaling?

To use an event-triggered task to delete instances created by Auto Scaling, set the trigger rule of the event-triggered task to a rule that deletes instances created by Auto Scaling. For more information, see [Create a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Create a scaling rule.md) and [Create event-triggered tasks](/intl.en-US/Automatic Scaling/Alarm tasks/Create a monitoring task.md).

## Does Auto Scaling support automatic scaling based on custom Cloud Monitor metrics?

Yes, Auto Scaling can scale ECS instances based on custom Cloud Monitor metrics. For more information, see [Custom monitoring event-triggered tasks](/intl.en-US/Automatic Scaling/Alarm tasks/Custom monitoring event-triggered tasks.md).

## Which is prioritized to be executed: an event-triggered task or a scheduled task?

Event-triggered tasks and scheduled tasks cannot be triggered at the same time. They are independent of each other and are not prioritized over each other.

If an event-triggered task is rejected and the trigger conditions are still met, the event-triggered task is executed after the current scaling activity is complete.

You can set the Retry Interval parameter for a scheduled task. This ensures that the scheduled task can be triggered again after it is rejected. For more information, see [Create a scheduled task](/intl.en-US/Automatic Scaling/Scheduled tasks/Create a scheduled task.md).

## Does Auto Scaling support automatic scaling of data disks?

No, Auto Scaling does not support automatic scaling of data disks. Auto Scaling can automatically increase or decrease the number of ECS instances in a scaling group. Auto Scaling cannot automatically increase or decrease the number or sizes of data disks on an ECS instance.

