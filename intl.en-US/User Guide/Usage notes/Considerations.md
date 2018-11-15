# Considerations {#concept_25880_zh .concept}

This topic introduces the considerations about Auto Scaling.

## Scaling rules {#section_qls_z3n_qfb .section}

When you run and compute a scaling rule, the system can automatically adjust the number of ECS instances according to the MaxSize value and the MinSize value of the scaling group. For example, if the number of ECS instances is set to 50 in the scaling rule, but the MaxSize value of the scaling group is set to 45, we compute and run the scaling rule with 45 ECS instances.

## Scaling activity { .section}

-   Only one scaling activity can be executed at a time in a scaling group.
-   A scaling activity cannot be interrupted. For example, if a scaling activity to add 20 ECS instances is being executed, it cannot be forced to terminate when only five instances have been created.
-   When a scaling activity fails to add or remove ECS instances to or from a scaling group, the system maintains the integrity of ECS instances rather than the scaling activity. That is, the system rolls back ECS instances, not the scaling activity. For example, if the system has created 20 ECS instances for the scaling group, but only 19 ECS instances are added to the Server Load Balancer instance, the system only releases the failed ECS instance.
-   Since Auto Scaling uses Alibaba Cloud’s Resource Access Management \(RAM\) service to replace ECS instances through ECS API, the rollback ECS instance is still charged.

## Cool-down time { .section}

-   During the cool-down time, only scaling activity requests from CloudMonitor alarm tasks are rejected by the scaling group. Other tasks, such as manually executed scaling rules and scheduled tasks, can immediately trigger scaling activities without waiting for the cool-down time to expire.
-   The cool-down time starts after the last ECS instance is added to or removed from the scaling group by a scaling activity.

