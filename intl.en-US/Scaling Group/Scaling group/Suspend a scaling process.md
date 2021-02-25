# Suspend a scaling process

This topic describes how to suspend a scaling process. After you suspend a scaling process, you can perform other operations. For example, before you stop an ECS instance, you must suspend the health check process to ensure that the instance is not removed from the scaling group because the instance fails the health check.

You can suspend the following processes for a scaling group. The suspended processes may affect each other.

|Scaling process|Effect of a suspended process|
|---------------|-----------------------------|
|Scale-out|All scale-out requests are rejected, which include: -   Add ECS instances manually.
-   Rebalance the distribution of ECS instances.
-   Execute scaling rules manually or by using scheduled or event-triggered tasks if the Expected Number of Instances feature is not enabled.
-   Execute scaling rules to add ECS instances by using event-triggered tasks if the Expected Number of Instances feature is enabled.
-   Add ECS instances. If the Expected Number of Instances feature is enabled, you can execute scaling rules manually or by using scheduled tasks to modify the expected number of instances. However, the number of ECS instances remains unchanged. After the scale-out process is resumed, Auto Scaling performs checks on the expected number of instances to add ECS instances.
-   Create ECS instances automatically when Auto Scaling performs checks on the minimum number of instances.
-   Create preemptible instances automatically if the Supplemental Preemptible Instance feature is enabled. |
|Scale-in|All scale-in requests are rejected, which include: -   Remove ECS instances manually.
-   Rebalance the distribution of ECS instances.
-   Execute scaling rules manually or by using scheduled tasks or event-triggered tasks if the Expected Number of Instances feature is not enabled.
-   Execute scaling rules to remove ECS instances by using event-triggered tasks if the Expected Number of Instances feature is enabled.
-   Remove ECS instances. If the Expected Number of Instances feature is enabled, you can execute scaling rules manually or by using scheduled tasks to modify the expected number of instances. However, the number of ECS instances remains unchanged. After the scale-in process is resumed, Auto Scaling performs checks on the expected number of instances to remove ECS instances.
-   Remove ECS instances automatically when Auto Scaling performs checks on the maximum number of instances. |
|Health check|Auto Scaling suspends the health check and does not remove unhealthy ECS instances.|
|Scheduled task|When the execution time of a scheduled task is reached, the scaling rule that is associated with the task is not triggered.|
|Event-triggered task|When an event-triggered task enters the alert state, the scaling rule that is associated with the task is not triggered.|

Suspended scaling processes help you control a scaling group at the scaling process level. If you want to control operations for ECS instances, we recommend that you put the ECS instances into the Standby or Protected state. For example, if you want to troubleshoot or restart an instance, you can put the instance into the Standby state. If you do not want the instance to be released, you can put the instance into the Protected state. For more information, see [Put an ECS instance into the Standby state](/intl.en-US/Instance Management/ECS instance/Put an ECS instance into the Standby state.md) and [Put an ECS instance into the Protected state](/intl.en-US/Instance Management/ECS instance/Put an ECS instance into the Protected state.md).

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Find the scaling group and click **Edit** in the **Actions** column.

5.  In the **Suspended Processes** section, select one or more processes that you want to suspend.

6.  Click **OK**.


**Related topics**  


[SuspendProcesses](/intl.en-US/API Reference/Scaling group/SuspendProcesses.md)

