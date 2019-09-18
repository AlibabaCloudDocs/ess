# Auto Scaling FAQ {#concept_bpd_tys_xgb .concept}

This topic lists FAQs related to Auto Scaling.

-   [How do I avoid scale-out failures due to an instance type having insufficient inventory?](#section_brg_xys_xgb)
-   [Which event takes priority between executing an alert task and executing a scheduled task?](#section_ch1_yys_xgb)
-   [Can I add an ECS instance to multiple scaling groups?](#section_pwr_yys_xgb)
-   [Why is an ECS instance in the protected state automatically released from a scaling group?](#section_ty9_oli_yc4)
-   [How can I prevent Auto Scaling from automatically releasing an ECS instance that I manually added to a scaling group?](#section_7ji_np8_vy4)

## How do I avoid scale-out failures due to an instance type having insufficient inventory? {#section_brg_xys_xgb .section}

Specify multiple zones \(select VSwitches in different zones\) when creating a scaling group, and select multiple Elastic Compute Service \(ECS\) instance types when creating a scaling configuration. If an instance type is out of inventory in one of the specified zones, Auto Scaling automatically switches to another zone where the instance type has sufficient inventory and executes the scale-out. For more information, see [Use custom scaling configurations to create scaling groups](reseller.en-US/User Guide/Realize Auto Scaling/Use custom scaling configurations to create scaling groups.md#) or [Use launch templates to create scaling groups](reseller.en-US/User Guide/Scaling configurations/Create a scaling configuration.md#).

## Which event takes priority between executing an alert task and executing a scheduled task? {#section_ch1_yys_xgb .section}

No priority is given to one task type over the other. At present, only one scaling activity can be executed in a scaling group at a time. If one task triggers a scaling activity earlier than the other task does, the earlier one is executed and the other one is rejected.

If an alert task is rejected and the alert triggers still exist, the alert task is executed after the scheduled task is completed.

You can set the Retry Interval parameter for a scheduled task. This ensures that the scheduled task can be triggered again after it is rejected. For more information, see [Create a scheduled task](reseller.en-US/User Guide/Realize Auto Scaling/Scheduled tasks/Create a scheduled task.md#).

## Can I add an ECS instance to multiple scaling groups? {#section_pwr_yys_xgb .section}

No. An ECS instance can be added to only one scaling group.

## Why is an ECS instance in the protected state automatically released from a scaling group? {#section_ty9_oli_yc4 .section}

Auto Scaling can automatically release an ECS instance created in a scale-out event even if you enable instance release protection in the ECS console or by calling the [ModifyInstanceAttribute](../../../../reseller.en-US/API Reference/Instances/ModifyInstanceAttribute.md#) operation.

To protect the ECS instance from being automatically released, you need to switch to the protected state for the ECS instance in the Auto Scaling console. For more information, see [Switch to the protected state for an ECS instance](reseller.en-US/User Guide/Maintain Auto Scaling/Switch to the protected state for an ECS instance.md#).

## How can I prevent Auto Scaling from automatically releasing an ECS instance that I manually added to a scaling group? {#section_7ji_np8_vy4 .section}

To prevent an ECS instance from being automatically released, you need to switch to the protected state for the ECS instance in the Auto Scaling console. For more information, see [Switch to the protected state for an ECS instance](reseller.en-US/User Guide/Maintain Auto Scaling/Switch to the protected state for an ECS instance.md#).

