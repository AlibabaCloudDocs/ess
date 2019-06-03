# Create a scaling rule {#concept_nyt_kpw_rfb .concept}

After creating a scaling group, you must create scaling rules to manage specific scaling actions of the group. This topic describes how to create a scaling rule.

## Limits {#section_x1c_ppw_rfb .section}

-   There is a limit to the maximum number of scaling rules that you can create in a scaling group. For more information, see [Quantity limits](reseller.en-US/User Guide/Usage notes/Quantity limits.md#).
-   Target tracking scaling rules can only be executed by alert tasks that were automatically created.
-   After you execute a scaling rule, if the actual number of ECS instances in service in a scaling group is greater than the configured **MaxSize** or smaller than the configured **MinSize** of the group, Auto Scaling automatically adds or removes instances to ensure the number of instances is within the configured range. The following examples illustrate this limit:
    -   Assume that you have a scaling group named asg-bp19ik2u5w7esjcu\*\*\*\*. The group has a MaxSize attribute of three, and has a scaling rule named add3 to add three instances. If the current number of instances in service is two and you execute the scaling rule add3, only one ECS instance is added.
    -   Assume that you have a scaling group named asg-bp19ik2u5w7esjcu\*\*\*\*. The group has a MinSize attribute of two, and has a scaling rule named reduce2 to remove two instances. If the current number of instances in service is three and you execute the scaling rule reduce2, only one ECS instance is removed.

## Procedure {#section_ash_r1x_rfb .section}

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  Click **Manage** in the **Actions** column corresponding to a scaling group for which you want to create a scaling rule.
3.  In the left-side navigation pane, click Scaling Rules. On the page that appears, click **Create Scaling Rule** in the upper-right corner.
4.  In the Create Scaling Rule dialog box that appears, set the parameters as needed, and then click **Create Scaling Rule**.

    You can set Rule Type as needed. For more information about these parameters, see [Simple scaling rules](#section_w87_i9q_o4h) and [Target tracking scaling rules](#section_d0c_275_idu).

    **Note:** When you create a target tracking scaling rule, an alert task associated with the rule is also created. Only this alert task is able to execute the target tracking scaling rule.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40578/155952337846200_en-US.png)


## Simple scaling rules {#section_w87_i9q_o4h .section}

A simple scaling rule directly adds or removes a specified number of instances, or adjusts instances in a scaling group to a specified number. The following table describes the simple scaling rule parameters.

|Parameter|Description|
|---------|-----------|
|**Rule Name**|The name of the scaling rule.|
|**Rule Type**|The type of the scaling rule. This parameter cannot be modified after the scaling rule is created.|
|**Operation**|The operation to be executed when the scaling rule is triggered. The operations include: -   Change to N instances: When the scaling rule is executed, the number of instances in the scaling group changes to N. A maximum of 500 instances can be scaled at a time.
-   Add N instances: When the scaling rule is executed, N instances are added to the scaling group. A maximum of 500 instances can be added at a time.
-   Add instances by N%: When the scaling rule is executed, N% of the current instances in the scaling group are added. A maximum of 500 instances can be scaled at a time.
-   Remove N instances: When the scaling rule is executed, N instances are removed from the scaling group. A maximum of 500 instances can be removed at a time.
-   Remove instances by N%: When the scaling rule is executed, N% of the current instances in the scaling group are removed. A maximum of 500 instances can be scaled at a time.

 |
|**Cooldown Time**|Optional. The cooldown period. Unit: seconds. If this parameter is not specified, the default cooldown period of the scaling group is used. For more information, see [Cooldown period](reseller.en-US/User Guide/Usage notes/Cool-down time.md#).|

## Target tracking scaling rules {#section_d0c_275_idu .section}

A target tracking scaling rule specifies a target value of a CloudMonitor metric. Auto Scaling automatically calculates the number of instances required to meet that target and scales ECS instances to ensure that the metric value remains close to the target value. The following table describes the parameters of target tracking scaling rules.

|Parameter|Description|
|---------|-----------|
|**Rule Name**|The name of the scaling rule.|
|**Rule Type**|The type of the scaling rule. This parameter cannot be modified after the scaling rule is created.|
|**Metric Name**|The name of a CloudMonitor metric to be monitored. Valid values: -   Average CPU Usage
-   Average Inbound Internal Traffic
-   Average Outbound Internal Traffic
-   Average Inbound Public Traffic
-   Average Outbound Public Traffic

 |
|**Target Value**|The target value of the CloudMonitor metric. A target tracking scaling rule keeps the CloudMonitor metric value close to the target value.|
|**Warmup Time**|The instance warm-up period. Unit: seconds. During this warm-up period, if instances are created by a target tracking scaling rule, the created and started instances do not affect the CloudMonitor metric value. This is to prevent the metric value from being changed multiple times because of scaling activities within the warm-up period.|
|**Disable Scale-in**|Indicates whether to disable scale-in. If this parameter is selected, a target tracking scaling rule cannot remove instances from the scaling group.|

