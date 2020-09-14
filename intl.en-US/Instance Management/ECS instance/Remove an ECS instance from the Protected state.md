# Remove an ECS instance from the Protected state

This topic describes how to remove an ECS instance from the Protected state. After an ECS instance is removed from the Protected state, Auto Scaling continues to manage the lifecycle of the ECS instance.

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
7.  Use one of the following methods to remove one or more ECS instances from the Protected state:

    -   Find the ECS instance that you want to remove from the Protected state and click **Remove from Protected** in the **Actions** column.
    -   Select multiple ECS instances that you want to remove from the Protected state and click **Remove from Protected** in the lower part of the ECS Instances page.
8.  In the message that appears, click **OK**.


**Related topics**  


[SetInstancesProtection](/intl.en-US/API Reference/Instance/SetInstancesProtection.md)

