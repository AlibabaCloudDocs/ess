# Cooldown time

This topic describes the cooldown time in Auto Scaling.

Cooldown time refers to a period during which Auto Scaling cannot execute new scaling activities after a scaling activity is complete. You can use one of the following methods to configure the cooldown time:

-   Configure the cooldown time in a scaling group. The default value cannot be empty. For more information, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md).
-   Configure the cooldown time in a scaling rule. If no cooldown time is specified, the default value is used. For more information, see [Create a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Create a scaling rule.md).

**Note:** If you configure the cooldown time in both a scaling group and scaling rule, Auto Scaling preferentially uses the cooldown time configured in the scaling rule.

## Cooldown time rules

Within the cooldown time, Auto Scaling rejects all scaling activity requests triggered by event-triggered tasks from Cloud Monitor. However, scaling activities triggered by other types of tasks such as manually triggered tasks and scheduled tasks are not limited by the cooldown time. These tasks are immediately executed.

Auto Scaling starts to calculate the cooldown time after a scaling activity is complete. If multiple ECS instances are added to or removed from a scaling group during a scaling activity, the cooldown time is calculated since the time when the last instance is added to or removed from the scaling group. For more information, see [Example 1](#section_d52_sbn_qfb). If no ECS instance is added to or removed from a scaling group during a scaling activity, the cooldown time is not calculated.

If you disable a scaling group and then enable it again, the cooldown time becomes invalid. For more information, see [Example 2](#section_d52_sbn_qfb).

**Note:** The cooldown time applies only to scaling activities in the same scaling group. It does not affect scaling activities in other scaling groups.

## Examples

-   Example 1

    You have a scaling group named asg-uf6f3xewn3dvz4bs\*\*\*\*. The default cooldown time is 10 minutes. A scaling rule named add3 exists in the scaling group and a cooldown time of 15 minutes is specified in the scaling rule.

    After a scaling activity triggered by the add3 scaling rule is complete, three ECS instances are added to the scaling group. The cooldown time is calculated since the time when the third instance is added to the scaling group. Within 15 minutes, scaling activity requests triggered by event-triggered tasks from Cloud Monitor are rejected.

-   Example 2

    You have a scaling group named asg-m5efkz67re9x7a57\*\*\*\*. The default cooldown time is 10 minutes. A scaling rule named remove1 exists in the scaling group and no cooldown time is specified in the scaling rule.

    After a scaling activity triggered by the remove1 scaling rule is complete at 18:00, one ECS instance is removed from the scaling group. Typically, scaling activity requests triggered by event-triggered tasks from Cloud Monitor are rejected before 18:10. If you disable the scaling group and then enable it again at 18:05, the cooldown time becomes invalid. If a scaling activity request is triggered by an event-triggered task from Cloud Monitor from 18:05 to 18:10, Auto Scaling accepts and executes the scaling activity for the scaling group.


