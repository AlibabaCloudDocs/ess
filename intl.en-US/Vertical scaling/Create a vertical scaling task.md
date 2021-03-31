# Create a vertical scaling task

Vertical scaling allows you to change the instance type \(vCPUs and memory\) of ECS instances at the scheduled time or in real time to meet your changing business requirements. This topic describes how to create a vertical scaling task in the Auto Scaling console.

## Procedure

1.  Go to the Vertical Scaling page.

    1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

    2.  In the left-side navigation pane, click **Vertical Scaling**.

    3.  In the top navigation bar, select a region.

2.  In the upper-left corner of the page, click **Create Vertical Scaling**.

3.  On the **Create Vertical Scaling** page, configure parameters to create a vertical scaling task.

    1.  Specify the task type, instance, and new instance types.

        -   **Type**: specifies the direction of the vertical scaling task.
            -   **Upgrade**: upgrades the instance type of the instance to increase the computing power.
            -   **Downgrade**: downgrades the instance type of the instance to decrease the computing power.
        -   **Select Instances**: specifies the instance whose instance type to change.
        -   **Select Instance Specifications**: specifies the new instance types. When multiple new instance types are specified, the instance type of the selected instance is upgraded or downgraded in the order in which these new instance types are specified.

            **Note:** Only instance types of the same instance family can be upgraded or downgraded in a vertical scaling task.

            -   To create a vertical scaling task of the upgrade type, you can specify up to 10 instance types in ascending order of computing power. Each specified instance type has a smaller specification of vCPUs and memory than the next instance type. For example, the current instance type is ecs.g6.large. You specify the following instance types in sequence: ecs.g6.3xlarge, ecs.g6.4xlarge, and ecs.g6.6xlarge. If the upgrade task is successfully executed two consecutive times, the current instance type is changed to ecs.g6.4xlarge.
            -   To create a vertical scaling task of the downgrade type, you can specify up to five instance types in descending order of computing power. Each specified instance type has a larger specification of vCPUs and memory than the next instance type. For example, the current instance type is ecs.g6.6xlarge. You specify the following instance types in sequence: ecs.g6.4xlarge, ecs.g6.3xlarge, and ecs.g6.large. If the downgrade task is successfully executed three consecutive times, the current instance type is changed to ecs.g6.large.
    2.  Specify the trigger type.

        -   Scheduled: Select **Scheduled Trigger**, and specify the recurrence and execution time of the task.
            -   If you want the task to be executed only once, select **Execute Now** or **Executed Once at the Specified Time** and specify the execution time.
            -   If you want the task to be repeatedly executed, select **Executed Periodically**, and specify the recurrence, time zone, and end time of the task. You can click **Quick Selection** to specify the execution time of the task or configure a cron expression to specify the recurrence of the task.

                **Note:** For information about rules of cron expressions, see [Configure cron expressions]().

        -   Threshold: Select **Threshold Trigger**, and specify the threshold condition and trigger mute period.
            -   Rule Description: Specify the threshold condition for statistical values of a Cloud Monitor metric. The threshold condition contains the following parameters: metric name, aggregation period of monitoring data, number of times that statistics are collected, statistical method, comparison operator, and threshold. The following figure shows an example in which the aggregation period is set to 5 minutes, and the vertical scaling task is triggered when the average value of the DiskIOPSWrite metric exceeds 70 three consecutive times.

                ![Sample rule](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9701907161/p254402.png)

            -   Trigger Mute Period: During the mute period, the vertical scaling task can be executed only once.

                **Note:** We recommend that you configure an appropriate threshold condition. If the number of times that statistics are collected is small or if the mute period is short, ECS instances may be frequently started, stopped, and upgraded or downgraded. This affects your service availability.

    3.  Specify permissions for the RAM role used by Operation Orchestration Service \(OOS\).

        -   If you are using vertical scaling for the first time, you must create a RAM role for OOS and grant the RAM role permissions to manage resources of ECS and Auto Scaling. For more information, see [Create a RAM role for a trusted Alibaba Cloud service](/intl.en-US/RAM Role Management/Create a RAM role/Create a RAM role for a trusted Alibaba Cloud service.md) and [Grant permissions to a RAM role](/intl.en-US/RAM Role Management/Grant permissions to a RAM role.md).

            **Note:** We recommend that you attach the AliyunECSFullAccess and AliyunESSFullAccess policies to grant permissions to the RAM role.

        -   If you are using vertical scaling not for the first time, you can select an existing RAM role such as OOSServiceRole.
    4.  Add a description and tags for the vertical scaling task for easy management.

4.  Click **Create Vertical Scaling**.


After the vertical scaling task is created, the system executes the task at the specified time or when the threshold condition is met. Operations such as stopping the instance, changing the instance type, and restarting the instance are automatically performed. You can view the execution details of the task. For more information, see [View a vertical scaling task](/intl.en-US/Vertical scaling/View a vertical scaling task.md).

