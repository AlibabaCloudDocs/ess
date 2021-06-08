# Move an ECS instance out of the Standby state

This topic describes how to move an ECS instance out of the Standby state. You can move an instance out of the Standby state to reuse it.

After an ECS instance in a scaling group is moved out of the Standby state:

-   The ECS instance enters the In Service state.
-   If a Server Load Balancer \(SLB\) instance is associated with the scaling group to which the ECS instance belongs, the ECS instance is added to the backend server group of the associated SLB instance again. By default, the SLB weight value of the instance is 50.
-   When the ECS instance is stopped or restarted, its health status is updated.
-   When a scale-in event is triggered in the scaling group, the ECS instance can be removed from the scaling group.

    **Note:** If the lifecycle of the ECS instance is managed by the scaling group, the ECS instance is released. Otherwise, the ECS instance can still run normally. For more information about the lifecycle management of ECS instances, see [ECS instance lifecycle](/intl.en-US/Instance Management/ECS instance/ECS instance lifecycle.md).


1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Find the scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   In the **Actions** column corresponding to the scaling group, click **Details**.
5.  In the upper part of the page, click the **Instances** tab.

6.  Select the source of an ECS instance.

    -   To select an automatically created ECS instance, click the **Auto Created** tab.
    -   To select a manually added ECS instance, click the **Manually Added** tab.
7.  Use one of the following methods to move one or more ECS instances out of the Standby state:

    -   Find the ECS instance that you want to move out of the Standby state and click **Remove from Standby** in the **Actions** column.
    -   Select multiple ECS instances that you want to move out of the Standby state and click **Remove from Standby** in the lower part of the Instances page.
8.  In the message that appears, click **OK**.


**Related topics**  


[ExitStandby](/intl.en-US/API Reference/Instance/ExitStandby.md)

