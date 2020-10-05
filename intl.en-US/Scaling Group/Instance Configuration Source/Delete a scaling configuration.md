# Delete a scaling configuration

This topic describes how to delete a scaling configuration that is no longer needed to maintain a sufficient quota.

The following conditions are met:

-   The scaling configuration is in the **Inactive** state.
-   The scaling group does not contain ECS instances that were created based on the scaling configuration.

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the top navigation bar, select a region.

3.  Find the scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   Click **Details** in the **Actions** column.
4.  In the upper part of the page, click the **Configuration Source** tab.

5.  In the upper-left corner of the Instance Configuration Source page, click the **Scaling Configurations** tab.

6.  Find the scaling configuration that you want to delete and click **Delete** in the **Actions** column.

7.  In the message that appears, click **OK**.


**Related topics**  


[DeleteScalingConfiguration](/intl.en-US/API Reference/Scaling configuration/DeleteScalingConfiguration.md)

