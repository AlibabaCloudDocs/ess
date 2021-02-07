# Rebalance the distribution of ECS instances

If ECS instances are not evenly distributed across zones due to insufficient resources, you can use the Rebalance Distribution feature to evenly distribute the ECS instances.

-   The network type of the scaling group is **VPC**.
-   The multi-zone scaling policy of the scaling group is **Balanced Distribution Policy**.
-   The scaling group is associated with multiple vSwitches that are distributed across at least two zones.

A maximum of 20 ECS instances can be replaced during a single rebalancing activity. When the rebalancing activity is executed, Auto Scaling first creates new ECS instances, and then stops and releases existing ECS instances to ensure that the ECS instances are evenly distributed across multiple zones. This does not affect the performance or availability of applications.

Auto Scaling allows the number of ECS instances to exceed 10% of the maximum number of instances for a short period of time. This occurs if the number of ECS instances in a scaling group approaches or reaches the maximum number of instances, but you must continue the balancing activity. If 10% of the maximum number of instances in the scaling group is not an integer, the decimal can be rounded up to one. The situation may last for a while until the distribution of ECS instances is balanced. It typically takes 1 to 6 minutes.

For example, the maximum number of instances in a scaling group is 15. A value of 10% indicates that the number of instances is 1.5. Then, the number of instances that a scaling group can exceed for a short period of time is 2.

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the top navigation bar, select a region.

3.  Find the scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   Click **Details** in the **Actions** column.
4.  In the upper part of the page, click the **Instances** tab.

5.  Click the **Auto Created** tab.

6.  Click **Rebalance Distribution**.

7.  Read the confirmation items and click **Confirm Execution**.


The message The rebalancing task has been assigned appears in the upper-right corner of the page. The newly created instances are displayed in the instance list. After a period of time, the newly created instances enter the InService state, and some existing ECS instances are released. However, the total number of ECS instances in the scaling group remains unchanged.

