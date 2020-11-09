# Automatically remove ECS instances

Auto Scaling monitors the ECS instances in a scaling group by using event-triggered tasks and automatically executes a scaling rule to add or remove ECS instances when an alert is triggered. This topic describes how to use event-triggered tasks to automatically remove ECS instances from a scaling group.

The following operations are performed:

-   [Manage the Auto Scaling service linked role](/intl.en-US/Quick Start/Manage the Auto Scaling service linked role.md)
-   [Create a scaling group and a scaling configuration](/intl.en-US/Quick Start/Create a scaling group and a scaling configuration.md)
-   [Automatically add ECS instances](/intl.en-US/Quick Start/Automatically add ECS instances.md)

The MyFirstScalingGroup scaling group is used in this topic to demonstrate how to automatically remove ECS instances. The scaling group already contains three ECS instances.

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
    |**Rule Name**|To1|
    |**Rule Type**|Simple Scaling Rule|
    |**Operation**|Change to 1 Instances|


## Step 2: Create an event-triggered task

1.  In the left-side navigation pane, choose **Scaling Tasks** \> **Event-Triggered tasks**.

2.  In the upper-right corner of the Event-Triggered Tasks page, click **Create Event-Triggered Task**.

3.  Configure parameters for the event-triggered task and click **OK**.

    The following table describes the parameters used in this example. For parameters that are not described in the following table, use the default values.

    |Parameter|Example|Description|
    |---------|-------|-----------|
    |**Task Name**|EventTriggeredScalingIn|None|
    |**Description**|Remove ECS instances when the average CPU utilization is less than 10%.|None|
    |**Resource Monitored**|MyFirstScalingGroup|Monitors metrics of the MyFirstScalingGroup scaling group.|
    |**Monitoring Type**|System Monitoring|None|
    |**Monitoring Metrics**|\(ECS\) CPU Usage|Monitors the CPU utilization of ECS instances in the scaling group.|
    |**Reference Period \(Minutes\)**|1|Collects data once every one minute.|
    |**Condition**|Average <= 10%|If the average CPU utilization of ECS instances in the scaling group is less than or equal to 10%, data is recorded once.|
    |**Trigger After**|5 Times|If the average CPU utilization of ECS instances in the scaling group is less than or equal to 10% for five times in a row, an alert is triggered.|
    |**Triggered Rule**|To1|When the alert is triggered, the To1 scaling rule is executed. Auto Scaling adjusts the number of ECS instances in the scaling group to one.|


The EventTriggeredScalingIn event-triggered task monitors the average CPU utilization of the three ECS instances in the MyFirstScalingGroup scaling group. The monitoring metric is calculated once every minute. If the average CPU utilization is less than or equal to 10% for five times in a row, an alert is triggered. The EventTriggeredScalingIn event-triggered task automatically executes the To1 scaling rule to adjust the number of ECS instances in the MyFirstScalingGroup scaling group to one. For more information, see the Scaling Activities page.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8940317951/p68070.png)

