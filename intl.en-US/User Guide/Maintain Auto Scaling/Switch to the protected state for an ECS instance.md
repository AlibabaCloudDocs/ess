# Switch to the protected state for an ECS instance {#task_1664409 .task}

This topic describes how to switch to the protected state for an Elastic Compute Service \(ECS\) instance.

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  In the top navigation bar, select a region.
3.  Find the scaling group to which the instance belongs and click **Manage** in the **Actions** column.
4.  In the left-side navigation pane, click **ECS Instances**.
5.  Find the target ECS instance and choose **More** \> **Switch to Protected State** in the **Actions** column.
6.  Click **OK**.

An ECS instance in the protected state has the following features:

-   If a Server Load Balancer \(SLB\) instance is attached to the scaling group to which the ECS instance belongs, the load balancing weight of the ECS instance remains unchanged after it is switched to the protected state.
-   Auto Scaling cannot automatically release the ECS instance until you remove from the protected state for the ECS instance.
-   If a scaling-in event is triggered when the number of ECS instances in a scaling group changes or an alert task detects triggers, Auto Scaling does not automatically release the ECS instance in the protected state. You need to remove from the protected state for the ECS instance to release it.
-   When the ECS instance is stopped or restarted, its health check status remains unchanged.

