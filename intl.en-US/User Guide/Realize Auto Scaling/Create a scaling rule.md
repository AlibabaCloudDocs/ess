# Create a scaling rule {#concept_nyt_kpw_rfb .concept}

This topic introduces the definition and creation steps of scaling rules.

After [creating a scaling group](reseller.en-US/User Guide/Use custom scaling configurations to create scaling groups.md#), you successfully enable a scaling group. If you want to scale up or scale down ECS resources, you must create scaling rules.

## What is a scaling rule {#section_x1c_ppw_rfb .section}

A scaling rule defines specific scaling actions; for example, adding or removing ECS instances. Currently, the following three scaling rules are supported:

-   Change to N instances: After you perform the scaling rule, the number of instances in service is changed to N.
-   Add N instances: After you perform the scaling rule, the number of instances in service increases by N.
-   Decrease N instances: After you perform the scaling rule, the number of instances in service is reduced by N.

**Note:** The number of scaling rules that can be created within a scaling group is limited. See [quantity restrictions](reseller.en-US/User Guide/Usage notes/Quantity restrictions.md#).

After you perform a scaling rule, if the actual number of instances in service in the scaling group is greater than the **MaxSize** or less than the **MinSize** of instances, Auto Scaling automatically changes the number of instances to ensure that the scaling result does not exceed the limit.

## Examples {#section_clc_l1x_rfb .section}

-   You have a scaling group asg-bp19ik2u5w7esjcucu28. The MaxSize is three, and the scaling rule add3 is to add three instances. If the current number of instances in service is two, when you perform the scaling rule add3, only 1 ECS instance is added.
-   You have a scaling group asg-bp19ik2u5w7esjcucu28. The MinSize is two, and the scaling rule reduce2 is to reduces two instances. If the current number of instances in service is three, when you perform the scaling rule reduce2, only 1 ECS instance is reduced.

## Procedure {#section_ash_r1x_rfb .section}

Following these steps to create a scaling rule:

1.  On the Scaling Groups page, click **Manage** in the **Actions** list next to the target scaling group.
2.  Go to the Scaling Rules page, click **Create Scaling Rule**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40578/155047587321666_en-US.png)

3.  In the Create Scaling Rule dialog box, specify the rule name, rule, and the cool-down time, and then click **Create Scaling Rule**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40578/155047587321667_en-US.png)

    **Note:** The cool-down time is an optional item. If you leave it empty, the cool-down time of the scaling group applies by default.


