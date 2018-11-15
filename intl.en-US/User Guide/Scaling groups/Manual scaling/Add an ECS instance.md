# Add an ECS instance {#task_zn2_2nx_rfb .task}

This topic describes how to add an ECS instance to a scale group.

If you add an ECS instance manually, the instance must meet the following conditions:

-   The ECS instance is in the same region as the scaling group.
-   The ECS instance is not in any other scaling group.
-   The ECS instance is **Running**.
-   The ECS instance can be the classic type or VPC, but has the following restrictions:
    -   If the scaling group is the classic type, only classic type instances can be added.
    -   If the scaling group is the VPC type, only instances belonging to the same VPC can be added.

To add an ECS instance, the scaling group must meet the following conditions:

-   The scaling group is **active**.
-   The scaling group is not executing any scaling activity.

**Note:** When no scaling activity is being executed for the scaling group, adding an ECS instance is executed directly without waiting for the cool-down time. A successful return indicates that the Auto Scaling service will shortly execute the scaling activity, but does not mean that the scaling activity will be successfully executed. Use the returned ScalingActivityID to check the scaling activity status. If the number of ECS instances to be added by the scaling rule plus the number of existing ECS instances in the scaling group \(Total Capacity\) exceeds the MaxSize value, the operation fails. Manually added ECS instances are not associated with the active scaling configuration in the scaling group. If you have any problem, open a ticket.

For detailed ECS instance configuration, see [create a scaling configuration](reseller.en-US/User Guide/Scaling configurations/Create a scaling configuration.md#).

You can add ECS instances in two ways:

-   [Perform a scaling rule](reseller.en-US/User Guide/Scaling groups/Realize Auto Scaling/Execute a scaling rule.md#) to automatically create one or more ECS instances. Automatically created ECS instances automatically meet the current scaling configuration. You do not have to worry about specification limitations.
-   Manually add one or more ECS instances. The manually added ECS instance configuration is not associated with the current scaling configuration.

You can skip the [cool-down time](reseller.en-US/User Guide/Usage notes/Cool-down time.md#) if you add ECS instances manually. The procedure of adding ECS instances manually is shown as follows.

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess). 
2.   On the Scale Groups page, click **Manage** in the **Actions** column next to the specified scaling group. 
3.  Go to the ECS Instances page, click **Add Existing Instance**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40594/154227328232047_en-US.png)

4.   Select the available ECS instances from the list on the left, click **\>** to to the instances to the scaling group, and then click **OK**. 
5.  Go to the Manually Add page to view the result. 

    **Note:** If the page does not refresh automatically, click **Refresh** in the upper-right corner of the page.


