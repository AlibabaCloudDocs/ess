# Glossary {#concept_yxx_khm_qfb .concept}

This article explains the related terms of Auto Scaling.

## Auto Scaling {#section_x3l_rhm_qfb .section}

Auto Scaling is a management service that allows users to automatically adjust elastic computing resources according to application demand and scaling policies you specify. It automatically creates ECS instances when demand peaks to improve capacity, and release them when demand decreases to save costs.

## Scaling group {#section_etz_shm_qfb .section}

A scaling group is a collection of ECS instances with similar configuration applying to a scenario. You can setup the minimum and maximum number of ECS instances, Server Load Balancer, and RDS for the scaling group.

## Scaling configuration {#section_l1y_thm_qfb .section}

Scaling configuration defines the specifications of ECS instances used to scale.

## Scaling rule {#section_knq_5hm_qfb .section}

A scaling rule specifies the scaling operation, such as whether, when, and how to create or release ECS instances.

## Scaling activity {#section_y3p_vhm_qfb .section}

When a scaling rule is triggered, a scaling activity takes place. Scaling activities is the changes made to the ECS instances in a scaling group.

## Scaling trigger task {#section_ynm_whm_qfb .section}

Tasks that can trigger scaling rules, such as the scheduled task or CloudMonitor alarm task.

## Cool-down time {#section_d2k_xhm_qfb .section}

The time Auto Scaling waited for the previous scaling activity to complete before resuming scaling activities. During the cool-down time, no other scaling activities can be performed in the same scaling group.

## Remarks {#section_wdr_yhm_qfb .section}

-   A scaling group includes settings of scaling configuration, scaling rules, and scaling activities.
-   Scaling configuration, scaling rules, and scaling activities are associated with the lifecycle management of a scaling group. Deleting the scaling group also deletes the associated scaling configuration, scaling rules, and scaling activities.
-   Scaling trigger tasks include scheduled tasks and CloudMonitor alarm tasks.
-   Scheduled tasks are independent of the scaling group. Deleting the scaling group does not lead to the deletion the scheduled tasks.
-   CloudMonitor alarm tasks are independent of the scaling group. Deleting the scaling group does not lead to the deletion of the CloudMonitor alarm tasks.

