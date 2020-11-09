# Expected number of instances

This topic describes the Expected Number of Instances feature and how to use the feature to specify the expected number of instances in a scaling group to execute parallel scaling activities.

## Overview

After the expected number of instances is specified, Auto Scaling automatically keeps the number of ECS instances at the expected value.

To enable the Expected Number of Instances feature, you must specify the **Expected Number of Instances** parameter when you create a scaling group. The specified expected number of instances in the scaling group can be modified.

**Note:** The Expected Number of Instances feature can be enabled only when you create a scaling group. You cannot enable the feature by modifying an existing scaling group.

The following table describes the terms for Expected Number of Instances.

|Term|Description|
|----|-----------|
|stable instance|An instance that is in the **In Service**, **Protected**, or **Standby** state in a scaling group.|
|parallel scaling activity|A scaling activity that can be executed in parallel with other scaling activities in a scaling group. Parallel scaling activities can be triggered by the following actions: -   Execute scaling rules manually or by using scheduled tasks.
-   Manually add or remove ECS instances.
-   Perform checks on the expected number of instances, instance health, minimum number of instances, and maximum number of instances. |
|non-parallel scaling activity|A scaling activity that cannot be executed in parallel with other scaling activities. A scaling activity that is not a parallel activity is a non-parallel scaling activity. Non-parallel scaling activities can be triggered by the following actions: -   Execute a scaling rule by using event-triggered tasks.
-   Manually execute the re-balancing task.
-   Execute the task of supplementing preemptible instances. |

## Scenarios

The Expected Number of Instances feature solves the following problems:

-   When a scaling activity fails to be executed, you must manually execute the scaling activity again.
-   When a scaling activity is being executed, other scaling activities cannot be executed.

## Limits

The following limits apply to the Expected Number of Instances feature:

-   After the Expected Number of Instances feature is enabled for a scaling group, the feature cannot be disabled.
-   The expected number of instances in a scaling group must range from the minimum number to the maximum number of ECS instances in the scaling group.

## Rules for changes of the expected number of instances

You can manually specify the expected number of instances. When Auto Scaling executes scaling activities, the expected number of instances can be changed. The following table describes the relationship between changes of the expected number of instances and how scaling activities are triggered.

|Scaling activity type|Method for triggering a scaling activity|Scaling activity result|New expected number of instances|Example|
|---------------------|----------------------------------------|-----------------------|--------------------------------|-------|
|Parallel scaling activity|Manually execute a scaling rule|Only the expected number of instances is changed. You must wait for Auto Scaling to perform a check on the expected number of instances to determine whether to add or remove instances.|Number of stable instances ± Number of added or removed instances|Scenario: -   Current expected number of instances: three
-   Current number of stable instances: two
-   A scaling rule is executed to automatically create four ECS instances.

Result:

The expected number of instances is changed to six, but the ECS instances are not created immediately. You must wait for Auto Scaling to perform a check on the expected number of instances to add or remove instances. |
|Execute a scaling rule by using scheduled tasks|Only the expected number of instances is changed. You must wait for Auto Scaling to perform a check on the expected number of instances to determine whether to add or remove instances.|Number of stable instances ± Number of added or removed instances|Scenario: -   Current expected number of instances: three
-   Current number of stable instances: two
-   A scaling rule is executed to automatically create four ECS instances.

Result:

The expected number of instances is changed to six, but the ECS instances are not created immediately. You must wait for Auto Scaling to perform a check on the expected number of instances to add or remove instances. |
|Manually add ECS instances|The ECS instances are added immediately, and the expected number of instances is changed.|Current expected number of instances + Number of manually added instances|Scenario: -   Current expected number of instances: three
-   Current number of stable instances: two
-   Manually add four existing ECS instances.

Result:

Four ECS instances are added to the scaling group. The number of stable instances is changed to six, and the expected number of instances is changed to seven. |
|Manually remove ECS instances|The ECS instances are removed immediately, and the expected number of instances is changed.|Current expected number of instances - Number of manually removed instances|Scenario: -   Current expected number of instances: three
-   Current number of stable instances: two
-   Manually remove one ECS instance.

Result:

One ECS instance is removed from the scaling group. The number of stable instances is changed to one, and the expected number of instances is changed to two. |
|Perform checks on the minimum and maximum numbers of instances|-|To be manually specified|Scenario: -   Current maximum number of instances: five
-   Current minimum number of instances: zero
-   Current expected number of instances: three
-   Current number of stable instances: two
-   Try to modify the maximum number of ECS instances to one.

Result:

The modification failed. You must modify the expected number of instances at the same time. |
|Perform health check on ECS instances|The ECS instances are immediately removed.|The expected number of instances remains unchanged|Scenario: -   Current expected number of instances: three
-   Current number of stable instances: two
-   One ECS instance is diagnosed as unhealthy.

Result:

The expected number of instances remains unchanged. The unhealthy ECS instance is removed from the scaling group, and the number of stable instances is changed to one. Auto Scaling can detect the difference between the expected number of instances and the number of stable instances, and then automatically perform a check on the expected number of instances to trigger the scaling activity to create two ECS instances. |
|Perform a check on the expected number of instances|The ECS instances are immediately added or removed.|The expected number of instances remains unchanged|Scenario: -   Current expected number of instances: three
-   Current number of stable instances: two

Result:

The expected number of instances remains unchanged. Auto Scaling can detect the difference between the expected number of instances and the number of stable instances, and then automatically perform a check on the expected number of instances to trigger the scaling activity to create one ECS instance. |
|Non-parallel scaling activity|Execute a scaling rule by using event-triggered tasks|The ECS instances are immediately added or removed, and the expected number of instances is changed.|Number of stable instances ± Number of added or removed instances|Scenario: -   Current expected number of instances: three
-   Current number of stable instances: two
-   A scaling rule is executed to automatically create four ECS instances.

Result:

A scaling activity is triggered to create four ECS instances, and the expected number of instances is changed to six. |

## Examples of parallel scaling activities

After the expected number of instances is specified, Auto Scaling can execute parallel scaling activities at the same time. Examples:

-   Example 1: Manually execute scaling rules continuously

    Scenario:

    -   Expected number of instances: three
    -   Number of stable instances: three
    -   The add3 scaling rule is executed to automatically create three ECS instances.
    -   The add1 scaling rule is executed to automatically create one ECS instance.
    -   Manually execute the add3 scaling rule first and then immediately execute the add1 scaling rule.
    Result: After the add3 scaling rule is executed, the expected number of instances is changed from three to six. However, Auto Scaling does not immediately perform a check on the expected number of instances to trigger a scale-out event. Therefore, the number of stable instances is still three. Then, the add1 scaling rule is immediately executed, and the expected number of instances is changed from six to four because the number of stable instances is still three. After Auto Scaling performs a check on the expected number of instances to trigger a scale-out event, the result of the parallel scaling activities is that one ECS instance is created.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3478449951/p71377.png)

-   Example 2: Manually execute a scaling rule and manually add ECS instances

    Scenario:

    -   Expected number of instances: three
    -   Number of stable instances: three
    -   The add1 scaling rule is executed to automatically create one ECS instance.
    -   Manually execute the add1 scaling rule first, and then manually add one existing ECS instance immediately.
    Result: After the add1 scaling rule is executed, the expected number of instances is changed from three to four. Manually add one existing ECS instance immediately, and the expected number of instances is changed from four to five. The result of the parallel scaling activities is that one ECS instance is created and one existing ECS instance is added.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3478449951/p71381.png)


## Examples of non-parallel scaling activities

After the expected number of instances is specified, Auto Scaling cannot execute parallel and non-parallel scaling activities at the same time. Example:

Scenario:

-   Expected number of instances: one
-   Number of stable instances: one
-   The scaling rule associated with an event-triggered task is executed to automatically create three ECS instances.
-   The add1 scaling rule is executed to automatically create one ECS instance.
-   After the event-triggered task is triggered, manually execute the add1 scaling rule immediately.

Result: After a scaling activity is triggered by the event-triggered task, the expected number of instances is changed from one to four. The scaling activity triggered by the event-triggered event is a non-parallel scaling activity, and cannot be immediately executed. The request to execute the add1 scaling rule is rejected, and the expected number of instances is still four.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3478449951/p71392.png)

