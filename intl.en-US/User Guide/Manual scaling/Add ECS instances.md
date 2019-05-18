# Add ECS instances {#task_zn2_2nx_rfb .task}

This topic describes how to manually add ECS instances to a scaling group.

Before manually adding ECS instances, ensure that the instances to be added meet the following conditions:

-   The instances are in the same region as the scaling group.
-   The instances do not belong to any other scaling groups.
-   The instances are in the **Running** state.
-   The instances to be added can be of either the classic network type or VPC type, but you must take note of the following limits:
    -   When the scaling group is classic network-connected, only classic network-connected instances can be added to the group.
    -   When the scaling group is VPC-connected, only instances in the same VPC as the group can be added to the group.

Before manually adding ECS instances to a scaling group, ensure that the group meet the following conditions:

-   The scaling group is in the **Enabled** state.
-   The scaling group is not currently executing any scaling activities.

The scaling configuration of the scaling group does not affect whether ECS instances can be manually added. Therefore, you can manually add ECS instances even with in the [Cool-down time](reseller.en-US/User Guide/Usage notes/Cool-down time.md#).

Typically, Auto Scaling scales out ECS instances based on your specifications. However, if the instance inventory is insufficient or the sum of ECS instances to be added and existing ECS instances in the scaling group exceeds the upper limit of the group, the number of actually scaled out instances may be less than what you specified. In these cases, check the scaling group configuration to troubleshoot the issue. If the problem persists, submit a ticket.

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  On the Scaling Groups page, click **Manage** in the **Actions** column corresponding to the scaling group to add instances. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40594/155815436221748_en-US.png)

3.  In the left-side navigation pane of the displayed page, click ECS Instances. On the page that appears, click **Add Existing Instances**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40594/155815436221749_en-US.png)

4.  In the dialog box that appears, select available ECS instances in the left-side list, click **\>** to add the selected instances to the scaling group, and click **OK**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40594/155815436221750_en-US.png)

5.  Go to the Manually Added tab to view the result. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40594/155815436321751_en-US.png)

    **Note:** If the page does not refresh automatically, click **Refresh** in the upper-right corner of the page.


