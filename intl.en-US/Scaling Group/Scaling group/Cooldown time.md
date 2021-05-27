# Cooldown time

This topic describes the cooldown time in Auto Scaling.

Cooldown time refers to a period during which Auto Scaling cannot execute new scaling activities after a scaling activity is executed. During the cooldown time, Auto Scaling rejects all scaling activity requests triggered by event-triggered tasks. However, scaling activities triggered by non-event-triggered tasks such as manually triggered tasks and scheduled tasks can be immediately executed without the need to wait for the cooldown time to expire.

You can use one of the following methods to configure the cooldown time:

-   Configure the cooldown time in a scaling group. The default value cannot be empty. For more information, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md).
-   Configure the cooldown time in a scaling rule. If no cooldown time is configured, the default value is used. For more information, see [Create a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Create a scaling rule.md).

**Note:** If you configure the cooldown time in a scaling group and in a scaling rule, Auto Scaling preferentially uses the cooldown time configured in the scaling rule.

## Cooldown time rules

-   If multiple Elastic Compute Service \(ECS\) instances are added to or removed from a scaling group during a scaling activity, Auto Scaling starts to count the cooldown time from the time when the last ECS instance is added to or removed from the scaling group. For more information, see [Example 1](#section_d52_sbn_qfb). If no ECS instance is added to or removed from a scaling group during a scaling activity, Auto Scaling does not count the cooldown time.
-   If you disable a scaling group and then enable it, the first scaling activity triggered after the scaling group is enabled can be immediately executed without the need to wait for the cooldown time to expire. Auto Scaling starts to count the cooldown time after the first scaling activity is executed. For more information, see [Example 2](#section_d52_sbn_qfb).

    **Note:** The cooldown time applies only to scaling activities in the same scaling group and does not affect scaling activities in other scaling groups.

-   After a scaling activity is executed in a scaling group, scaling activities triggered by non-event-triggered tasks can be immediately executed without the need to wait for the cooldown time to expire. Non-event-triggered tasks include manually triggered tasks, scheduled tasks, and tasks for modifying the expected, minimum, or maximum number of instances in the scaling group. For more information, see [Example 3](#section_d52_sbn_qfb).

## Examples

-   Example 1

    You have a scaling group named asg-uf6f3xewn3dvz4bs\*\*\*\*. The default cooldown time is 10 minutes. A scaling rule named add3 exists in the scaling group, and a cooldown time of 15 minutes is configured in the scaling rule.

    After the add3 scaling rule is triggered to execute a scaling activity, three ECS instances are created. Within 15 minutes starting from the time when the third ECS instance is added to the scaling group, scaling activity requests triggered by event-triggered tasks are rejected.

-   Example 2

    You have a scaling group named asg-m5efkz67re9x7a57\*\*\*\*. The default cooldown time is 10 minutes. A scaling rule named remove1 exists in the scaling group, and no cooldown time is configured in the scaling rule.

    After a scaling activity triggered by the remove1 scaling rule is executed at 18:00, one ECS instance is removed from the scaling group. Typically, scaling activity requests triggered by event-triggered tasks are rejected before 18:10. After the ECS instance is removed from the scaling group, disable the scaling group and then enable it again at 18:05. If a scaling activity is triggered by an event-triggered task between 18:05 and 18:10, this scaling activity request is accepted and executed. Within 10 minutes starting from the time when the scaling activity is executed, scaling activity requests triggered by event-triggered tasks are rejected.

-   Example 3

    You have a scaling group named asg-bp15x5gq2ib3bhx3\*\*\*\*. The default cooldown time is 10 minutes. A scaling rule named add1 exists in the scaling group, and a cooldown time of 10 minutes is configured in the scaling rule.

    After a scaling activity triggered by the add1 scaling rule is executed at 18:00, one ECS instance is added to the scaling group. Typically, scaling activity requests triggered by event-triggered tasks are rejected before 18:10. If the add1 scaling rule is manually executed at 18:05, the scaling activity for creating one ECS instance triggered by the scaling rule is immediately accepted and executed without the need to wait for the cooldown time to expire.


