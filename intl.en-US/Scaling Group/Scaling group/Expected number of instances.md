# Expected number of instances

This topic describes the Expected Number of Instances feature and how to use this feature to specify the expected number of instances in a scaling group to execute parallel scaling activities.

## Overview

After the expected number of instances is specified, Auto Scaling automatically maintains the number of ECS instances at the expected value. The Expected Number of Instances feature solves the following problems:

-   When a scaling activity fails to be executed, you must manually execute the scaling activity again.
-   When a scaling activity is being executed, other scaling activities cannot be executed.

To enable the Expected Number of Instances feature, you must specify the **Expected Instances** parameter when you create a scaling group. The specified expected number of instances in the scaling group can be modified.

**Note:** The Expected Number of Instances feature can be enabled only when you create a scaling group. You cannot enable the feature by modifying the number of instances in an existing scaling group.

The following table describes the terms for the Expected Number of Instances feature.

|Term|Description|
|----|-----------|
|stable instance|An instance that is in the **In Service**, **Protected**, or **Standby** state in a scaling group.|
|parallel scaling activity|A scaling activity that can be executed in parallel with other on-going scaling activities in a scaling group. Parallel scaling activities can be triggered by the following actions: -   Execute scaling rules manually or by using scheduled tasks.
-   Manually add or remove ECS instances.
-   Perform checks on the expected number of instances, instance health, minimum number of instances, and maximum number of instances. |
|non-parallel scaling activity|A scaling activity that cannot be executed in parallel with other on-going scaling activities. A scaling activity that is not a parallel activity is a non-parallel scaling activity. Non-parallel scaling activities can be triggered by the following actions: -   Execute a scaling rule by using event-triggered tasks.
-   Manually execute the rebalancing task on the **Instances** tab.
-   Automatically supplements preemptible instances.

**Note:** You must set **Multi-zone Scaling Policy** to **Cost Optimization Policy** and turn on **Enable Supplemental Preemptible Instances** when you create a scaling group. |

## Limits

-   After the Expected Number of Instances feature is enabled for a scaling group, the feature cannot be disabled.
-   The expected number of instances in a scaling group must range from the minimum number to the maximum number of instances in the scaling group.

## Rules for changes to the expected number of instances

You can manually specify the expected number of instances. You can also change the expected number of instances by executing scaling activities. The changes are related to how the scaling activities are triggered.

|Scaling activity type|Method for triggering a scaling activity|Scaling activity result|New expected number of instances|Example|
|---------------------|----------------------------------------|-----------------------|--------------------------------|-------|
|Parallel scaling activity|Manually execute a scaling rule|Only the expected number of instances is changed. You must wait for Auto Scaling to perform a check on the expected number of instances to determine whether to add or remove instances.|Number of stable instances ± Number of added or removed instances|Scenario: -   Current expected number of instances: 3
-   Current number of stable instances: 2
-   Number of instances created by a scaling rule: 4

Result:

The expected number of instances is changed to 6, but the ECS instances are not immediately created. You must wait for Auto Scaling to perform a check on the expected number of instances to add or remove instances. |
|Execute a scaling rule by using scheduled tasks|Only the expected number of instances is changed. You must wait for Auto Scaling to perform a check on the expected number of instances to determine whether to add or remove instances.|Number of stable instances ± Number of added or removed instances|Scenario: -   Current expected number of instances: 3
-   Current number of stable instances: 2
-   Number of instances created by a scaling rule: 4

Result:

The expected number of instances is changed to 6, but the ECS instances are not immediately created. You must wait for Auto Scaling to perform a check on the expected number of instances to add or remove instances. |
|Manually add ECS instances|The ECS instances are immediately added, and the expected number of instances is changed.|Current expected number of instances + Number of manually added instances|Scenario: -   Current expected number of instances: 3
-   Current number of stable instances: 2
-   Number of manually added instances: 4

Result:

Four ECS instances are added to the scaling group. The number of stable instances is changed to 6, and the expected number of instances is changed to 7. |
|Manually remove ECS instances|The ECS instances are immediately removed, and the expected number of instances is changed.|Current expected number of instances - Number of manually removed instances|Scenario: -   Current expected number of instances: 3
-   Current number of stable instances: 2
-   Number of manually removed instances: 1

Result:

One ECS instance is removed from the scaling group. The number of stable instances is changed to 1, and the expected number of instances is changed to 2. |
|Perform checks on the minimum and maximum numbers of instances|-|To be manually specified|Scenario: -   Current maximum number of instances: 5
-   Current minimum number of instances: 0
-   Current expected number of instances: 3
-   Current number of stable instances: 2
-   Maximum number of instances that is attempted to modify: 1

Result:

The maximum number fails to be modified. You must modify the expected number of instances at the same time. |
|Perform a health check on ECS instances|The ECS instances are immediately removed.|The expected number of instances remains unchanged|Scenario: -   Current expected number of instances: 3
-   Current number of stable instances: 2
-   Number of instances that are diagnosed as unhealthy: 1

Result:

The expected number of instances remains unchanged. The unhealthy ECS instance is removed from the scaling group, and the number of stable instances is changed to 1. Auto Scaling detects the difference between the expected number of instances and the number of stable instances, and then automatically performs a check on the expected number of instances to trigger the scaling activity to create 2 ECS instances. |
|Perform a check on the expected number of instances|The ECS instances are immediately added or removed.|The expected number of instances remains unchanged|Scenario: -   Current expected number of instances: 3
-   Current number of stable instances: 2

Result:

The expected number of instances remains unchanged. Auto Scaling detects the difference between the expected number of instances and the number of stable instances, and then automatically performs a check on the expected number of instances to trigger the scaling activity to create 1 ECS instance. |
|Non-parallel scaling activity|Execute a scaling rule by using event-triggered tasks|The ECS instances are immediately added or removed, and the expected number of instances is changed.|Number of stable instances ± Number of added or removed instances|Scenario: -   Current expected number of instances: 3
-   Current number of stable instances: 2
-   Number of instances created by a scaling rule: 4

Result:

A scaling activity is triggered to create 4 ECS instances, and the expected number of instances is changed to 6. |

## Examples of parallel scaling activities

After the expected number of instances is specified, Auto Scaling can execute parallel scaling activities at the same time. Examples:

-   Example 1: Manually execute scaling rules in a consecutive manner

    Scenario:

    -   Expected number of instances: 3
    -   Number of stable instances: 3
    -   The add3 scaling rule specifies to create 3 ECS instances.
    -   The add1 scaling rule specifies to create 1 ECS instance.
    -   Manually execute the add3 scaling rule first and then immediately execute the add1 scaling rule.
    Result: After the add3 scaling rule is executed, the expected number of instances is changed from 3 to 6. The add1 scaling rule is immediately executed, and the expected number of instances is changed from 6 to 4. After the parallel scaling activity is executed, 1 ECS instance is created and the number of stable instances in the scaling group is changed to 4.

    ![Example 1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3478449951/p71377.png)

-   Example 2: Manually execute a scaling rule and manually add ECS instances

    Scenario:

    -   Expected number of instances: 3
    -   Number of stable instances: 3
    -   The add1 scaling rule specifies to create 1 ECS instance.
    -   Manually execute the add1 scaling rule first, and then immediately add 1 existing ECS instance.
    Result: After the add1 scaling rule is executed, the expected number of instances is changed from 3 to 4. One existing ECS instance is immediately added, and the expected number of instances is changed from 4 to 5. After the parallel scaling activity is executed, 1 ECS instance is created, 1 existing ECS instance is added, and the number of stable instances in the scaling group is changed to 5.

    ![Example 2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3478449951/p71381.png)


## Examples of non-parallel scaling activities

After the expected number of instances is specified, Auto Scaling cannot execute parallel and non-parallel scaling activities at the same time. Example:

Scenario:

-   Expected number of instances: 1
-   Number of stable instances: 1
-   The scaling rule associated with an event-triggered task specifies to create 3 ECS instances.
-   The add1 scaling rule specifies to create 1 ECS instance.
-   After the event-triggered task is triggered, immediately execute the add1 scaling rule manually.

Result: After a scaling activity is triggered by the event-triggered task, the expected number of instances is changed from 1 to 4. The scaling activity triggered by the event-triggered event is a non-parallel scaling activity and cannot be immediately executed. The request to execute the add1 scaling rule is rejected, and the expected number of instances is still 4. After the non-parallel scaling activity is executed, 3 ECS instances are created, and the number of stable instances in the scaling group is changed to 4.

![Examples of non-parallel scaling activities](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3478449951/p71392.png)

