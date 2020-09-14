# Manually remove an ECS instance from a scaling group

This topic describes how to manually remove an ECS instance that is no longer needed from a scaling group.

-   The scaling group is in the **Enabled** state.
-   The scaling group does not have ongoing scaling activities.

You can manually remove an ECS instance from a scaling group without the need to wait for the cooldown period to expire.

You cannot remove an ECS instance if the number of ECS instances in the scaling group after the removal is less than the minimum number.

A scaling activity may fail to be executed after it is triggered. You can check the execution result in the details about the scaling activity. For more information, see [View the details of a scaling activity](/intl.en-US/Monitoring/Scaling events/View the details of a scaling activity.md).

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Find the target scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   Click **Manage** in the **Actions** column.
5.  In the left-side navigation pane, click **ECS Instances**.

6.  Select the source of an ECS instance.

    -   To select an automatically created ECS instance, click the **Auto Created** tab.
    -   To select a manually added ECS instance, click the **Manually Added** tab.
7.  Use one of the following methods to remove one or more ECS instances from a scaling group:

    When you delete an ECS instance, the instance is removed from the scaling group and released. Whether you can delete an ECS instance that is manually added to a scaling group is subject to the management mode of the instance. If the lifecycle of the instance is not managed by the scaling group, you can only remove the instance from the scaling group but cannot delete the instance. If the lifecycle of the instance is managed by the scaling group, you can remove the instance from the scaling group and delete the instance.

    -   Find the ECS instance that you want to remove from the scaling group and choose ![More](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3826400061/p130487.png) \> **Remove from Scaling Group** in the **Actions** column.
    -   Select multiple ECS instances that you want to remove from the scaling group and click **Remove from Scaling Group** in the lower part of the ECS Instances page.
    -   Find the ECS instance that you want to delete and choose ![More](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3826400061/p130487.png) \> **Delete Instance** in the **Actions** column.
    -   Select multiple ECS instances that you want to delete and click **Delete Instance** in the lower part of the ECS Instances page.
8.  In the message that appears, click **OK**.


