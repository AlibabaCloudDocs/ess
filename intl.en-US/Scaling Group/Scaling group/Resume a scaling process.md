# Resume a scaling process

This topic describes how to resume a suspended scaling process. This allows the scaling group to continue the specified process based on its functional logic.

After a scaling process is resumed, the process takes into account the changes made during the suspension. For example, the expected number of instances in a scaling group changes when the scale-out process is suspended for the scaling group. After the scale-out process is resumed, Auto Scaling performs checks on the expected number of ECS instances to add instances, and the expected number of instances changes accordingly.

|Scaling process|Effect of a resumed process|
|---------------|---------------------------|
|Scale-out|The scaling group resumes scale-out events, such as manually adding instances as well as checking the expected and minimum numbers of instances. If the Expected Number of Instances feature is enabled and the expected number of instances increases during a suspension, Auto Scaling performs checks on the expected number of instances to add ECS instances. |
|Scale-in|The scaling group resumes scale-in events, such as manually removing instances as well as checking the expected and maximum numbers of instances. If the Expected Number of Instances feature is enabled and the expected number of instances decreases during a suspension, Auto Scaling performs checks on the expected number of instances to remove ECS instances. |
|Health check|The scaling group resumes the health check and automatically removes unhealthy ECS instances.|
|Scheduled task|If a scheduled task is not due or is being retried, the scaling rule that is associated with the task is triggered.|
|Event-triggered task|If an event-triggered task enters the alert state, the scaling rule that is associated with the task is triggered.|

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Find the scaling group and click **Edit** in the **Actions** column.

5.  In the **Suspended Processes** section, remove the process that you want to resume.

6.  Click **OK**.


**Related topics**  


[ResumeProcesses](/intl.en-US/API Reference/Scaling group/ResumeProcesses.md)

