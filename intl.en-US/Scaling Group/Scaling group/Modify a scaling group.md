# Modify a scaling group

This topic describes how to modify a scaling group. You can modify the parameters of a scaling group based on your actual needs after it is created.

The following limits apply when you mofiy a scaling group:

-   You cannot change the network type of a scaling group.
-   If the network type of a scaling group is **VPC**, you can change the vSwitch, but cannot change the multi-zone scaling policy or reclaim mode.

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Find the scaling group and click **Edit** in the **Actions** column.

5.  Modify the parameters of the scaling group.

    For information about the parameters of a scaling group, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md).

    **Note:** After you modify the Maximum Number of Instances or Minimum Number of Instances parameter, the number of existing ECS instances in the scaling group may fall outside the specified range. In this case, Auto Scaling automatically adds or removes ECS instances to ensure that the number of ECS instances in the scaling group is within the specified range.

6.  Click **OK**.


**Related topics**  


[ModifyScalingGroup](/intl.en-US/API Reference/Scaling group/ModifyScalingGroup.md)

