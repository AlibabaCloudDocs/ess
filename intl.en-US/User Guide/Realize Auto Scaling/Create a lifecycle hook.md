# Create a lifecycle hook {#concept_75094_zh .concept}

This topic describes the definition of lifecycle hook and how to create a lifecycle hook.

You have followed the steps described in [Execute a scaling rule](reseller.en-US/User Guide/Realize Auto Scaling/Execute a scaling rule.md#) to execute scaling rules to scale ECS instances. However, these ECS instances are only configured with basic settings. To use these instances in complex business, you may need to perform custom actions before enabling these ECS instances. To complete this task, you can use lifecycle hooks.

## What is lifecycle hook { .section}

You can create lifecycle hooks for a scaling group. When a scaling group with lifecycle hooks performs scaling activities, the instances to be added to or removed from the scaling group will be put to the Wait status. Lifecycle hooks only take effect on ECS instances that are automatically added to or removed from the scaling groups. Manually added or removed ECS instances are not affected.

**Note:** The maximum number of lifecycle hooks that you can create for a scaling group is limited. For more information, see [Restrictions](reseller.en-US/User Guide/Usage notes/Quantity restrictions.md#).

## Examples {#section_ep1_5dx_rfb .section}

For example, you have created scaling group sg-yk201808201449. The minimum number of instances that the scaling group must contain is 0. The scaling group has one lifecycle hook for scaling activities. Currently, the scaling group does not have any ECS instances.

Change the minimum number of instances to 1 for the scaling group. After the modification, a scaling activity is triggered because the number of instances that the scaling group contains does not meet the minimum requirement. An ECS instance is then automatically added to the scaling group. However, since the scaling group has a lifecycle hook, the status of the ECS instance will not change to **InService** immediately. Instead, its status changes to **Adding:Wait**.

During the lifecycle hook timeout period, you can log on to the ECS instance, and install applications or perform custom actions.

## Features {#section_bxq_12x_rfb .section}

The scaling group has the following features while its ECS instance is put into the Wait status by the lifecycle hook:

-   The scaling group does not perform other scaling activities.
-   You can perform custom actions during the lifecycle hook timeout period. For example, you can initialize the configuration of the ECS instance or obtain the ECS instance data.
-   You can delete the corresponding lifecycle hook to resume the scaling activity.
-   You can also call the [CompleteLifecycleAction](../../../../../reseller.en-US/API-Reference/Lifecycle Hook/CompleteLifecycleAction.md#) or [DeleteLifecycleHook](../../../../../reseller.en-US/API-Reference/Lifecycle Hook/DeleteLifecycleHook.md#) interface to resume the scaling activity.

## Procedure {#section_lw3_d2x_rfb .section}

Follow these steps to create a lifecycle hook:

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  On the Scale Groups page, click **Manage** in the **Actions** column for the target scaling group.
3.  Go to the Lifecycle Hooks page, click **Create Lifecycle Hook**.
4.  In the Create Lifecycle Hook dialog box, set the Name, Applicable Scaling Activity Type, Timeout, Policy, Notification Method, MNS Topic/Queue, and Notification ID then click **Create Lifecycle Hook**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40580/155046736221713_en-US.png)

    **Note:** For more information about lifecycle hook properties, see the following table.


## Lifecycle hook properties { .section}

The following table describes the lifecycle hook properties and examples.

|Property|Description|Example|
|:-------|:----------|:------|
|Name|The lifecycle hook name must be 2 to 40 characters in length. It must start with an English letter, number, or Chinese character. The name can contain periods \(.\), underscores \(\_\), and hyphens \(-\). After you have set the lifecycle name, you can no longer change it.|hz\_yk0626|
|Applicable Scaling Activity Type|The type of scaling activities.|Scale-In|
|Timeout|The lifecycle hook timeout period. During this period, the instances remain in the Wait status. The value must be an integer from 30 to 21,600 seconds.|600|
|Policy|Available policies include **Continue** and **Abandon**. -    **Continue**: Allows other scaling activities when the current lifecycle action ends.
-    **Abandon**: Releases the created ECS instances if the scaling activity type is scale-out. This policy does not take effect if the scaling activity type is scale-in.

 |Continue|
|Notification Method|The available notification methods include **MNS Topic** and **MNS Queue**. After you select a notification method, you must select the specific MNS topic or queue.|MNS Topic|
|Notification ID|The notification ID is sent to you with notifications so that you can easily manage the notifications by ID.|General information|

