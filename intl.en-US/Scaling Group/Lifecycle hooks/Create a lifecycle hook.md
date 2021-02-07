# Create a lifecycle hook

You can use lifecycle hooks to put ECS instances that are being added or removed into the wait state. After the ECS instances are put into the wait state, you can perform custom operations on them.

You can configure scaling configurations or launch templates to create ECS instances that have specified settings. However, to meet complex business requirements, you may want to perform custom operations on these instances before they are started. In this case, you can use lifecycle hooks.

You can create lifecycle hooks for a scaling group. When a scaling group with lifecycle hooks executes scaling activities, the instances that are being added to or removed from the scaling group are put into the wait state. You can create only a limited number of lifecycle hooks for a scaling group. For more information, see [Limits](/intl.en-US/Product Introduction/Limits.md).

**Note:** Lifecycle hooks take effect only when a scaling rule is executed to add or remove ECS instances to or from a scaling group. Lifecycle hooks do not take effect when ECS instances are manually added to or removed from a scaling group.

When ECS instances in a scaling group are put into the wait state:

-   You can perform custom operations on these instances during the timeout period of a lifecycle hook. For example, you can initialize or obtain the configurations of the ECS instances.
-   Whether other scaling activities in the scaling group can be executed depends on the settings of the expected number of instances.

    -   If the expected number of instances is not specified for the scaling group, Auto Scaling rejects other scaling activities.
    -   If the expected number of instances is specified for the scaling group, Auto Scaling can execute other scaling activities only when the ongoing scaling activity is a parallel scaling activity. For information about how to determine a parallel scaling activity, see [Glossary](/intl.en-US/Product Introduction/Glossary.md).
    **Note:** You can delete a lifecycle hook or call the [CompleteLifecycleAction](/intl.en-US/API Reference/Lifecycle Hook/CompleteLifecycleAction.md) operation to terminate the wait state of a scaling activity in advance.


You can configure a notification method for a lifecycle hook. When the lifecycle hook is triggered, a notification can be sent to the specified Message Service \(MNS\) topic or queue, or an operation can be performed based on the specified Operation Orchestration Service \(OOS\) template. To configure a notification method, you must create an [MNS topic](https://www.alibabacloud.com/help/doc-detail/34424.htm), [MNS queue](https://www.alibabacloud.com/help/doc-detail/34417.htm), or [OOS custom template](https://www.alibabacloud.com/help/doc-detail/120695.htm) in advance.

**Note:** If you use an OOS public template, you do not need to create it in advance. For more information, see [Public templates](https://www.alibabacloud.com/help/doc-detail/123171.htm).

Example:

Assume that you have created a scaling group named asg-bp1iir8uwwpdsjfj\*\*\*\*. The minimum number of instances that the scaling group must contain is zero. The scaling group has one lifecycle hook for scale-out events and does not have ECS instances.

Change the minimum number of instances to one for the scaling group. After the minimum number is modified, a scale-out event is triggered because the number of instances in the scaling group does not meet the minimum requirement. Then, Auto Scaling automatically adds an ECS instance to the scaling group. However, the status of the ECS instance does not immediately become **In Service** because the scaling group has a lifecycle hook. Instead, its status becomes **Pending**.

During the timeout period of the lifecycle hook, you can log on to the ECS instance and install applications or perform custom operations.

## Procedure

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Find the scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   Click **Details** in the **Actions** column.
5.  In the upper part of the page, click the **Lifecycle Hook** tab.

6.  In the upper-left corner of the Lifecycle Hook page, click **Create Lifecycle Hook**.

7.  Configure the parameters for the lifecycle hook.

    The following table describes the parameters of a lifecycle hook.

    |Parameter|Description|
    |---------|-----------|
    |Name|The name cannot be modified after the lifecycle hook is created. The name must be 2 to 64 characters in length, and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter or a digit.|
    |Applicable Scaling Activity Type|When scaling activities of the specified type occur, the lifecycle hook is triggered to put corresponding ECS instances into the wait state. Valid values:     -   **Scale-in Event**
    -   **Scale-out Event** |
    |Timeout Period|During the timeout period, corresponding ECS instances remains in the wait state. The value must be an integer from 30 to 21600. Unit: seconds.|
    |Execution Policy|This parameter specifies the action to be taken after the lifecycle hook times out. Valid values:     -   **Continue**: Auto Scaling continues to execute a scale-in or scale-out event.
    -   **Reject**: Auto Scaling releases the created ECS instances for a scale-out event or removes the ECS instances for a scale-in event. |
    |Notification Method|When the lifecycle hook is triggered, Auto Scaling sends a notification or performs an operation based on the specified notification method. Valid values:     -   **No Notification**: This is the default value.
    -   **MNS Topic**: If you set the parameter to this value, you must select an MNS topic.
    -   **MNS Queue**: If you set the parameter to this value, you must select an MNS queue.
    -   **OOS Template**: If you set the parameter to this value, you must select an OOS template.
You can set a notification ID if you set the notification method to MNS Topic or MNS Queue. The notification ID is sent along with notifications to the MNS topic or MNS queue so that you can manage the notifications by ID. |

8.  Click **OK**.


