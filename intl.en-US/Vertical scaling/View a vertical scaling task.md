# View a vertical scaling task

This topic describes how to view the details of a vertical scaling task, including the execution time, execution result, and logs.

## Procedure

1.  Go to the Vertical Scaling page.

    1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

    2.  In the left-side navigation pane, click **Vertical Scaling**.

    3.  In the top navigation bar, select a region.

2.  On the **Vertical Scaling** page, find the vertical scaling task that you want to view based on information such as the trigger type and task type \(upgrade or downgrade\).

3.  Click **Details** in the **Actions** column to view the details of the task.

    The following section describes the common tabs on the details page of a vertical scaling task:

    -   On the **Advanced View** tab, you can view information of a vertical scaling task, such as the basic information, execution module, execution result, and execution logs.

        ![Advanced View](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2612907161/p254810.png)

    -   On the **Scheduled Execution List** tab, you can view the list of previous executions and the list of upcoming executions for a vertical scaling task whose trigger type is set to Scheduled Trigger.

        ![Scheduled tasks](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2047517161/p259005.png)

    -   On the **Event Alarm Execution List** tab, you can view the list of previous executions for a vertical scaling task whose trigger type is set to Threshold Trigger.

        ![Threshold execution list](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2612907161/p254811.png)


## FAQ

-   Does the **Waiting** state of a vertical scaling task on the **Vertical Scaling** page indicate that the task is not executed?

    No, the Waiting state of a vertical scaling task does not necessarily indicate that the task is not executed. The **Waiting** state of a vertical scaling task indicates that the task continues to be executed. For example, although a vertical scaling task whose trigger type is set to Threshold Trigger has been executed twice, the task is still in the **Waiting** state.

-   Why am I prompted the User not authorized to operate on the specified resource, or this API doesn't support RAM message when I move the pointer over the ![Error](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5931017161/p254528.png) icon if my vertical scaling task fails?

    This is because the RAM role used by Operation Orchestration Service \(OOS\) is not granted the required permissions. We recommend that you attach the AliyunECSFullAccess and AliyunESSFullAccess policies to the RAM role. For more information, see [Grant permissions to a RAM role](/intl.en-US/RAM Role Management/Grant permissions to a RAM role.md).


