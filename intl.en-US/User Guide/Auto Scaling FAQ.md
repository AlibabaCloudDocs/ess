# Auto Scaling FAQ {#concept_bpd_tys_xgb .concept}

-   [How do I avoid scale-out failures due to an instance type having insufficient inventory?](#section_brg_xys_xgb)
-   [Which event takes priority between executing an alarm task and executing a scheduled task?](#section_ch1_yys_xgb)
-   [Can I add an ECS instance to multiple scaling groups?](#section_pwr_yys_xgb)

## How do I avoid scale-out failures due to an instance type having insufficient inventory? {#section_brg_xys_xgb .section}

Specify multiple zones \(select VSwitches in different zones\) when creating a scaling group, and select multiple ECS instance types when creating a scaling configuration. If an instance type is unavailable in one of the specified zones, Auto Scaling automatically switches to another zone where the instance type is available and executes the scale-up. For more information, see [Use custom scaling configurations to create scaling groups](reseller.en-US/User Guide/Use custom scaling configurations to create scaling groups.md#) or [Use launch templates to create scaling groups](reseller.en-US/User Guide/Use launch templates to create scaling groups.md#).

## Which event takes priority between executing an alarm task and executing a scheduled task? {#section_ch1_yys_xgb .section}

No priority is given to one task type over the other. At present, only one scaling activity can be executed in a scaling group at a time. If one task triggers a scaling activity earlier than the other task does, the earlier one is executed and the other one is rejected.

## Can I add an ECS instance to multiple scaling groups? {#section_pwr_yys_xgb .section}

No.

