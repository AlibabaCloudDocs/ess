# Overview

Vertical scaling can change instance types \(vCPU and memory\) of pay-as-you-go instances. When your business requirements increase, vertical scaling upgrades instance types to ensure computing power. When your business requirements decrease, vertical scaling downgrades instance types to reduce costs. The system monitors changes in business requirements on a regular basis or by using Cloud Monitor metrics and automatically triggers vertical scaling tasks to meet your diversified business requirements.

When the system performs a vertical scaling task, the system automatically completes a series of operations, including stopping the instances to be scaled, changing the instance types, and starting the scaled instances.

## Scenarios

-   If you can predict business peak periods, for example, if you expect a large number of tasks to be processed at the beginning of each month or promotion activities to be launched at a specified time, you can create scheduled vertical scaling tasks. This way, vertical scaling upgrades instance types before the business soars to ensure computing power, and downgrades instance types when the business declines to reduce costs.
-   If your business requirements are not regular, for example, if you need to report hot news from time to time, you can create threshold-triggered vertical scaling tasks. The system monitors the specified Cloud Monitor metrics and changes instance types when the threshold rules are met.

    **Note:** The new instance types of the instances scaled in the vertical scaling task take effect only after the instances are restarted. When the system restarts the instance, the high availability of the business is compromised.


## Benefits

-   Efficient: Vertical scaling increases or reduces the computing power of existing ECS instances, which eliminates the need to create and release ECS instances and perform custom configurations.
-   Convenient: Vertical scaling automatically changes instance types. You do not need to manually stop the instances to be scaled, change instance types, or start the scaled instances.
-   Flexible: Vertical scaling changes instance types on a regular basis or in real time based on thresholds to better meet changing business needs.
-   Cost-effective: Vertical scaling can reduce resource costs by downgrading instance types in a timely manner when the business decreases. It also reduces the O&M costs caused by your continuous attention to resource usage.

## Billing methods

The vertical scaling feature is free of charge, but the billing of instances changes after instance types of the instances are changed. Prices increase after instance types are upgraded and decrease after instance types are downgraded. For more information about the billing rules for pay-as-you-go instances, see [Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md).

## Limits

-   Vertical scaling changes only instance types of pay-as-you-go instances excluding preemptible instances.
-   In a vertical scaling task, you can upgrade or downgrade an instance among the instance types within the same instance family. For example, you can change the instance type of an instance from ecs.g6.large to ecs.g6.2xlarge, but not to instance types of other instance families such as ecs.c6.2xlarge and ecs.r6.2xlarge.
-   You can only upgrade or only downgrade instance types in a vertical scaling task. If you have different business requirements, you can configure multiple vertical scaling tasks.
-   If vertical scaling tasks are tasks that are triggered and executed repeatedly, such as scheduled tasks or threshold-triggered tasks, the following rules apply:
    -   If you upgrade instance types, you can specify up to 10 instance types in ascending order of computing power \(vCPU and memory\).
    -   If you downgrade instance types, you can specify up to five instance types in descending order of computing power \(vCPU and memory\).
-   When you configure a vertical scaling task as a recurring task, the interval between consecutive cycles must be greater than 30 minutes. Otherwise, frequent changes in instance types affect high availability of the business.

