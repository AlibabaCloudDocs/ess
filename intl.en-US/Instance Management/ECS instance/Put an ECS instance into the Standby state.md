# Put an ECS instance into the Standby state

This topic describes how to put an Elastic Compute Service \(ECS\) instance that is not needed for the moment into the Standby state. After an ECS instance is put into the Standby state, the Server Load Balancer \(SLB\) weight value of the ECS instance changes to zero. If an ECS instance is in the Standby state, Auto Scaling does not check its health status or release it.

After an ECS instance is put into the Standby state:

-   If an SLB instance is associated with the scaling group to which the ECS instance belongs, the SLB weight value of the ECS instance changes to zero.
-   The ECS instance stays in the Standby state until you manually move it out of the Standby state.
-   Auto Scaling stops managing the lifecycle of the ECS instance. You must manually manage the lifecycle of the ECS instance.
-   If a scale-in event is triggered, Auto Scaling does not remove the ECS instance.
-   When the ECS instance is stopped or restarted, its health check status remains unchanged.
-   To release the ECS instance, you must first remove it from the scaling group.
-   If you delete the scaling group to which the ECS instance belongs, the instance is automatically moved out of the Standby state and removed from the scaling group.

    **Note:** If the lifecycle of the ECS instance is managed by the scaling group, the instance is released. Otherwise, the instance is not released and can run normally. For more information about the lifecycle management of ECS instances, see [ECS instance lifecycle](/intl.en-US/Instance Management/ECS instance/ECS instance lifecycle.md).

-   You can stop the ECS instance or change its configurations. For example, you can perform the following operations:
    -   [Stop an instance](/intl.en-US/Instance/Manage instances/Stop an instance.md)
    -   [Reboot the instance](/intl.en-US/Instance/Manage instances/Restart an instance.md)
    -   [Upgrade or downgrade instance configurations](/intl.en-US/Instance/Change configurations/Overview of instance upgrade and downgrade.md)
    -   [Change the operating system](/intl.en-US/Images/Change the operating system.md)
    -   [Initialize a cloud disk](/intl.en-US/Block Storage/Cloud disks/Reinitialize a cloud disk/Re-initialize a system disk.md)
    -   [Migrate an ECS instance from the classic network to a VPC](/intl.en-US/Best practices/Classic network-to-VPC migration/Overview.md)

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
7.  Use one of the following methods to put one or more ECS instances into the Standby state:

    -   Find the ECS instance that you want to put into the Standby state and click **Switch to Standby** in the **Actions** column.
    -   Select multiple ECS instances that you want to put into the Standby state and click **Switch to Standby** in the lower part of the Instances page.
8.  In the message that appears, click **OK**.


**Related topics**  


[EnterStandby](/intl.en-US/API Reference/Instance/EnterStandby.md)

