# Cool-down time {#concept_d3h_51n_qfb .concept}

This topic introduces the cool-down time in Auto Scaling.

Cool-down time refers to a period during which Auto Scaling cannot execute any new scaling activity after another scaling activity is executed successfully in a scaling group. Cool-down time is described as follows:

-   During cool-down time, the scaling activity requests from CloudMonitor alarm tasks are rejected. Other tasks, such as manually executed scaling rules and scheduled tasks, can immediately trigger scaling activities without waiting for the cool-down time to expire. See [create a scaling group](reseller.en-US/User Guide/Scaling groups/Realize Auto Scaling/Create a scaling group.md#).
-   During cool-down time, only the corresponding scaling group is locked. Scaling activities set for other scaling groups can be executed. See [create a scaling rule](reseller.en-US/User Guide/Scaling groups/Realize Auto Scaling/Create a scaling rule.md#).

**Note:** After a scaling group is re-enabled after being disabled, the cool-down time is no longer in effect. For example, if a scaling activity is completed at 12:00 PM and the cool-down time is 15 minutes, the scaling group is then disabled and re-enabled, and the cool-down time is no longer in effect. If a request for triggering a scaling activity is sent at 12:03 PM from the CloudMonitor, the requested scaling activity is executed immediately.

## Cool-down time rules {#section_l14_3bn_qfb .section}

After the scaling group successfully performs the scaling activity, Auto Scaling starts to calculate the cool-down time. If multiple ECS instances are added to or removed from the scaling group in a scaling activity, the cool-down time is calculated since the last instance is added to or removed from the scaling group. See [examples](#). If no ECS instance is successfully added to or removed from the scaling group during the scaling activity, the cool-down time is not calculated.

Within the cool-down time, the scaling group rejects the scaling activity request triggered by the CloudMonitor alarm tasks. However, the scaling activity triggered by other types of tasks \(manually executing tasks, scheduled tasks\) can be performed immediately, bypass cooling time.

If you disable a scaling group and then enable the scaling group again, the cool-down time becomes invalid. See [example 1](#1114).

**Note:** The cool-down time only locks the scaling activities in the same scaling group. It does not affect the scaling activities in other scaling groups.

## Examples {#section_d52_sbn_qfb .section}

**Example 1**

You have a scaling group asg-uf6f3xewn3dvz4bsy7r1. The default cool-down time is 10 minutes, and a scaling rule add3 exists in the scaling group with a cool-down time of 15 minutes.

After a scaling activity is successfully performed based on add3, three ECS instances are added. The cool-down time is calculated since the third instance is added to the scaling group. Within 15 minutes, scaling activity requests triggered by the alarm task from CloudMonitor are rejected.

**Example 2**

You have a scaling group asg-m5efkz67re9x7a571bjh. The default cool-down time is 10 minutes, and a scaling rule remove1 exists in the scaling group without cool-down time set.

A scaling activity is successfully performed based on remove1 at 18:00. One ECS instance is decreased. Normally, scaling activity requests triggered by the alarm task from CloudMonitor are rejected before 18:10. Disable the scaling group, and then enable the scaling group again at 18:05. The cool-down time becomes invalid. The scaling group accepts the scaling activity requests triggered by the alarm task from CloudMonitor from 18:05 to 18:10.

