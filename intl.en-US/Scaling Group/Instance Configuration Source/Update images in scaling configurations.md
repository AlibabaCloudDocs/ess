# Update images in scaling configurations

The Update Image in Scaling Configuration feature applies to scenarios where applications are frequently published. You can create an update image task in the Auto Scaling console. When the task is executed, Auto Scaling automatically creates a custom image from the source instance and replaces images in the scaling configurations of the scaling group with the created custom image.

Update image tasks are executed by using Operation Orchestration Service \(OOS\). You must authorize OOS to perform operations on related resources. Make sure that at least one of the following requirements is met:

-   The current account has permissions to perform operations on resources of ECS and Auto Scaling.
-   A RAM role is created for OOS and is granted permissions to perform operations on resources of ECS and Auto Scaling. For more information, see [Grant RAM permission for OOS](https://www.alibabacloud.com/help/doc-detail/120810.htm).

**Note:** We recommend that you attach the AliyunECSFullAccess and AliyunESSFullAccess policies to grant permissions to the RAM role.

When an update image task is executed, Auto Scaling automatically creates a custom image from the source instance. You are charged based on the size of snapshots created from the image. For more information, see [Snapshot](/intl.en-US/Pricing/Billing items/Snapshot billing.md).

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Find the scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   Click **Details** in the **Actions** column.
5.  In the upper part of the page, click the **Configuration Source** tab.

6.  In the upper-left corner of the page, click the **Update Image Tasks** tab.

7.  In the upper-left corner of the tab, click **Update Image in Scaling Configuration**.

8.  Configure the parameters for the update image task.

    The following table lists the parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Instance**|Select an ECS instance. Auto Scaling creates a custom image from the instance. The custom image is used to replace the images in scaling configurations. The custom image is created only from the system disk.|
    |**Scaling Configuration ID**|Select one or more scaling configurations for which you want to update images.|
    |**Executed At**|Specify the time when the task is executed.     -   **Now**: immediately.
    -   **Scheduled**: at the specified time. You must specify the execution time, in minutes.
    -   **Periodic**: specifies the recurrence period, expiration time, and start time of the image update task. Assume that you configure the following settings for an image update task on August 17, 2020:

        -   **Recurrence**: Monthly
        -   Execute from Day 21 to Day 25 of Each Month
        -   **Start Time**: 02:00
        -   **Expired At**: 00:00 on August 26, 2020
The image update task is executed once at 02:00 every day from August 21, 2020 to August 25, 2020. |
    |**Permission Source**|Select the permission source for OOS to perform operations on related resources.     -   **Use Existing Permissions of Current Account**: The permissions of the current account are used.
    -   **Specify RAM Role and Use Permissions Granted to This Role**: You must select a RAM role to be assumed by OOS and use the permissions granted to this role. |

9.  Click **OK**.

    The update image task is automatically executed at the specified time. You can view the execution status and source instance of this task in the task list.

    ![Update image task](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6360881061/p129471.png)


After the task is executed, you can view the execution result on the **Scaling Configurations** tab. If the image names in the scaling configurations are in the `UpdateImage_from_<source ECS instance ID>_on_<update image task ID>` format, the images in the scaling configurations are updated.

![Update image result](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6360881061/p129493.png)

