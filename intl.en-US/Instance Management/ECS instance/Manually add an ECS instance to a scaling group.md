# Manually add an ECS instance to a scaling group

This topic describes how to manually add an ECS instance to a scaling group. You can add existing ECS instances to a scaling group to take full advantage of the computing resources.

The following table describes the requirements that the ECS instances must meet to be manually added to a scaling group.

|Item|Prerequisite|
|----|------------|
|The ECS instances to be manually added to a scaling group|-   The instances are located in the same region as the scaling group.
-   The instances are not added to any other scaling group.
-   The instances are in the **Running** state.
-   The network type of the instances is classic network or Virtual Private Cloud \(VPC\). Take note of the following items:
    -   When the network type of the scaling group is classic network, only ECS instances of the classic network type can be added to the scaling group.
    -   When the network type of the scaling group is VPC, only ECS instances in the same VPC as the scaling group can be added to the scaling group. |
|The scaling group|-   The scaling group is in the **Enabled** state.
-   The scaling group does not have ongoing scaling activities. |

The active scaling configuration of a scaling group does not affect whether ECS instances can be manually added to the scaling group. You can manually add ECS instances without waiting for the cooldown period to expire. For more information, see [Cooldown time](/intl.en-US/Scaling Group/Scaling group/Cooldown time.md).

Typically, Auto Scaling scales out sufficient ECS instances based on your configurations. However, if the instance inventory is insufficient or the sum of ECS instances to be added and existing ECS instances in the scaling group exceeds the maximum number of instances specified for the scaling group, the number of actually created instances may be less than what you specified. In these cases, check the configuration of the scaling group to troubleshoot the issue. If the issue persists, [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Find the scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   Click **Details** in the **Actions** column.
5.  In the upper part of the page, click the **Instances** tab.

6.  Click the **Manually Added** tab.

7.  Click **Add Existing Instance**.

8.  In the Add Existing Instance dialog box, select available ECS instances in the left-side list, click **\>** to add the selected ECS instances to the right-side list, and then click **Add**.

    If you select **Enable the scaling group to manage the instance lifecycle**, ECS instances that are manually added to the scaling group will be removed and released during scale-in events. Subscription instances can be manually added to a scaling group, but their lifecycle cannot be managed by the scaling group.

    **Warning:** Make sure that you have sufficient balance in your account. If you have overdue payments in your account, pay-as-you-go and preemptible instances will be stopped or even released. For information about status changes of ECS instances due to overdue payments, see [Overdue payments](/intl.en-US/Pricing/Overdue payments.md).

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3406369951/p21750.png)


**Related topics**  


[AttachInstances](/intl.en-US/API Reference/Trigger task/AttachInstances.md)

