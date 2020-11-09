# Automatically add ECS instances

Auto Scaling executes a scaling rule to add or remove ECS instances by using scheduled tasks. This topic describes how to automatically add ECS instances to a scaling group. Two ECS instances are added to a scaling group in this topic.

The following operations are performed:

-   [Manage the Auto Scaling service linked role](/intl.en-US/Quick Start/Manage the Auto Scaling service linked role.md)
-   [Create a scaling group and a scaling configuration](/intl.en-US/Quick Start/Create a scaling group and a scaling configuration.md)

The MyFirstScalingGroup scaling group and MyFirstScalingConfiguration scaling configuration are used in this topic to demonstrate how to automatically add ECS instances. The scaling group already contains one ECS instance.

## Step 1: Create a scaling rule

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  Find the scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   Click **Details** in the **Actions** column.
4.  In the upper part of the page, click the **Scaling Rules** tab.

5.  In the upper-left corner of the Scaling Rules tab, click **Create Scaling Rule**.

6.  Configure parameters for the scaling rule and click **OK**.

    The following table describes the parameters used in this example. For parameters that are not described in the following table, use the default values.

    |Parameter|Example|
    |---------|-------|
    |**Rule Name**|Add2|
    |**Rule Type**|Simple Scaling Rule|
    |**Operation**|Add 2 Instances|


## Step 2: Create a scheduled task

1.  In the left-side navigation pane, choose **Scaling Tasks** \> **Scheduled Tasks**.

2.  In the upper-left corner of the Scheduled Tasks page, click **Create Scheduled Task**.

3.  Configure parameters for the scheduled task and click **OK**.

    The following table describes the parameters used in this example. For parameters that are not described in the following table, use the default values.

    |Parameter|Example|Description|
    |---------|-------|-----------|
    |**Task Name**|ScheduledScalingOut|None|
    |**Description**|Add two ECS instances at the scheduled time.|None|
    |**Executed At**|2019-11-11 16:35|Five minutes after the current time.|
    |**Scaling Group**|MyFirstScalingGroup|Executes the scheduled task for the MyFirstScalingGroup scaling group.|
    |**Scaling Method**|Select an existing rule|None|
    |**Simple Scaling Rule**|Add2|Executes the Add2 scaling rule to add two ECS instances to the scaling group.|


At 16:35 on November 11, 2019, the ScheduledScalingOut scheduled task automatically executes the Add2 scaling rule to add two ECS instances to the MyFirstScalingGroup scaling group. For more information, see the Scaling Activities page.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7940317951/p68058.png)

