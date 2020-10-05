# Rolling update

This topic describes how to manage rolling update tasks. Rolling update tasks can be used to update the configurations of ECS instances in batches. You can use Rolling Update to perform batch operations on ECS instances in the In Service state in a scaling group. You can perform operations such as updating images or executing scripts.

-   Operation Orchestration Service \(OOS\) is available in the region where the scaling group resides.

    **Note:** OOS is unavailable in the China \(Qingdao\), China \(Ulanqab\), China \(Heyuan\), US \(Silicon Valley\), and UAE \(Dubai\) regions. Therefore, the Rolling Update feature is also unavailable in these regions.

-   No scaling activities are in progress in the scaling group.
-   A script or an image is prepared.

You can update the configurations of ECS instances by updating images or executing scripts. The following section describes the applicable scenarios:

-   Image updates are more comprehensive. You can perform image updates to update the operating systems of all ECS instances in a scaling group at a time.
-   Scripts are more flexible. You can use scripts to perform one or more O&M operations that are suitable for the following scenarios:
    -   View and update some system configurations such as the disk space.
    -   Install commonly used software such as Apache.
    -   Deploy business code.

## Limits

-   You can update images or execute scripts only for ECS instances in the **In Service** state.
-   You can execute only one rolling update task at a time.

## Create and execute a rolling update task

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the top navigation bar, select a region.

3.  In the left-side navigation pane, click **Scaling Groups**.

4.  Find the scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   Click **Details** in the **Actions** column.
5.  In the left-side navigation pane, click **Rolling Update**.

6.  In the upper-right corner of the page, click **Create Execution Task**.

7.  In the **Create Execution Task** dialog box, configure the required parameters and click **Create Task**.

    The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Task Description**|The description of the rolling update task.|
    |**Task Type**|    -   **Image Update**

Specifies the image that is used to replace images of ECS instances. You can select a public image, a custom image, a shared image, or an Alibaba Cloud Marketplace image. During the process, the ECS instances are restarted. You must specify the following parameters:

        -   **Image for Update**: the image that is used to execute the rolling update task
        -   **Image for Rollback**: the image that is used to execute the rollback task

**Note:** By default, when you create a rollback task, this image is used. You can select other images.

    -   **Script Execution**

Cloud Assistant is used to execute scripts. ECS instances are not stopped when the scripts are executed. You must specify the following parameters:

        -   In the **Script Type** section, select one of the following script types:
            -   **Linux Shell**: such as echo hello and hostname
            -   **Windows Bat**: such as dir c:\\
            -   **Windows PowerShell**: such as Get-Services
        -   **Script for Execution**: the script that is used to execute tasks for ECS instances
        -   **Script for Rollback**: the script that is used to execute rollback tasks

**Note:** By default, when you create a rollback task, this script is used. You can also edit the script. |
    |**Execution Batch**|The number of times this task is executed. The ECS instances are divided into multiple batches, and the task is run in these batches. Each batch contains at least one ECS instance. For example, if a scaling group has 10 ECS instances in the In Service state, and Execution Batch is set to 2, this task is executed in two batches.|
    |**Suspension Policy**|    -   **Automatic**: The task is executed without interruptions.
    -   **Suspend First Batch**: Auto Scaling suspends the task after the first batch is complete. You must manually continue the task. After you manually continue the task, the task will not be suspended in the subsequent batches.
    -   **Suspend Each Batch**: Auto Scaling suspends the task each time after a batch is complete. You must manually continue the task after each batch. |

8.  Read the execution impact and click **OK** if you confirm the information.

    Then, the rolling update task is automatically executed. After the rolling update task starts to be executed, it has the following impacts on the scaling group and ECS instances in the scaling group:

    -   Auto Scaling suspends the scale-in and scale-out processes in the scaling group during the rolling update process. After the rolling update task is complete, the scale-in and scale-out processes are resumed. If the scale-in and scale-out processes are manually suspended before execution, these events stay suspended. This ensures that the process status in the scaling group remains unchanged.
    -   Auto Scaling switches ECS instances to the **Standby** state in batches and restores the instances to the **In Service** state after the execution is complete.

        **Note:** If the scaling group is associated with SLB instances, the SLB weight values of ECS instances in the **Standby** state will be set to zero and no business traffic is received.

9.  Perform the following operations based on the execution status of the rolling update task:

    -   If the suspension policy of the rolling update task is **Suspend First Batch** or **Suspend Each Batch**, the task will enter the **Pending \(Batch Suspension\)** state once or more times. Confirm that the ECS instances that have been updated meet your requirements. Perform the following operations if you confirm the information:
        1.  Click **Continue** in the **Actions** column.
        2.  In the **Continue Execution Task** dialog box, click **OK**.
    -   If the execution of the rolling update task fails, the task enters the **Pending \(Failure Suspension\)** state. If you want to continue this task, perform the following operations:
        1.  Click **Details** in the **Actions** column.
        2.  Find an ECS instance in the Failure state. Click **Retry**, **Skip**, or **Cancel** in the **Actions** column.
            -   Click **Retry** to execute the rolling update for this ECS instance again.
            -   Click **Skip** to execute the rolling update for the next ECS instance. The status of the current ECS instance is changed to **Success**.

                **Note:** You must manually remove the ECS instance that is skipped from the **Standby** state.

            -   Click **Cancel** to execute the rolling update for the next ECS instance. The status of the current ECS instance is changed to **Failure**.
    -   If you want to cancel the rolling update task, click **Cancel** in the **Actions** column.

        **Note:** After you cancel the rolling update task, you must manually resume the suspended scaling processes and remove the ECS instances that are in the Failure state or are being updated in the current batch from the **Standby** state.

    -   For more information, see [Roll back a rolling update task](#section_361_yxj_08r).

## Roll back a rolling update task

You can roll back a rolling update task that is in the Pending state \(contains Batch Suspension and Failure Suspension\) or is last executed to resume the configurations of ECS instances when an exception occurs. You cannot roll back a rollback task.

**Note:** Before you roll back a rolling update task in the Pending state, the rolling update task will be canceled. Instances that have been updated will be rolled back.

1.  In the execution task list, find the rolling update task that you want to roll back and click **Rollback** in the **Actions** column.

2.  In the **Create Rollback Task** dialog box, configure the required parameters.

    The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Task Description**|The description of the rollback task.|
    |**Task Type**|The task type is consistent with that of the rolling update task. You cannot modify the task type.     -   If the task type is **Image Update**, the image that is used when you create the rolling update task is automatically selected. You can select other images.
    -   If the task type is **Script Execution**, the script that is specified when you create the rolling update task is automatically filled. You can edit the script. |
    |**Execution Batch**|The number of times this task is executed. The ECS instances are divided into multiple batches, and the task is run in these batches. Each batch contains at least one ECS instance. For example, if a scaling group has 10 ECS instances in the In Service state, and Execution Batch is set to 2, this task is executed in two batches.|
    |**Suspension Policy**|    -   **Automatic**: The task is executed without interruptions.
    -   **Suspend First Batch**: Auto Scaling suspends the task after the first batch is complete. You must manually continue the task.
    -   **Suspend Each Batch**: Auto Scaling suspends the task each time after a batch is complete. You must manually continue the task after each batch. |

3.  Click **Create Task**.

4.  Read the rollback impact and click **OK** if you confirm the information.

    Then, the rollback task is automatically executed.


## View the details of a rolling update task

You can view the details of a rolling update task and retry or skip the task for an ECS instance.

1.  In the execution task list, find the task whose details you want to view and click **Details** in the **Actions** column.

2.  View the basic task information.

    The basic task information contains the task status and type. If the task type is **Script Execution**, click **Script Details** to view the details of the script.

3.  View the execution instance list.

    ECS instances in various states are displayed.

    -   If an ECS instance is not updated, you can skip or cancel the task for the instance.
    -   If an ECS instance fails to be updated, you can retry, skip, or cancel the task for the instance in the **Actions** column.
    -   If the task type is **Script Execution**, click **View** in the **Result** column to view the execution result of the script.
    The following section describes the difference between retrying, skipping, and canceling a task for an ECS instance:

    -   Click **Retry** to execute the rolling update for this ECS instance again.
    -   Click **Skip** to execute the rolling update for the next ECS instance. The status of the current ECS instance is changed to **Success**.

        **Note:** You must manually remove the ECS instance that is skipped from the **Standby** state.

    -   Click **Cancel** to execute the rolling update for the next ECS instance. The status of the current ECS instance is changed to **Failure**.

**Related topics**  


[t1930744.md\#](/intl.en-US/Best practices/Rolling update.md)

