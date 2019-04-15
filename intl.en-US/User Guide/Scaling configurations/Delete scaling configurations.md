# Delete scaling configurations {#task_ihs_s14_qfb .task}

You can delete scaling configurations that are no longer required to release more quotas.

Before you delete a scaling configuration, ensure the following conditions are met, or the delete operation will fail.

-   The status of the scaling configuration must be **Inactive**.
-   In the scaling group, no ECS instance is automatically created based on the scaling configuration.

1.  Log on to the [Auto Scaling Console](https://partners-intl.console.aliyun.com/#/ess). 
2.  On the Scaling Groups page, click **Manage** in the **Actions** column. 
3.  In the left-side navigation pane, select Instance Configuration Source. 
4.  On the Scaling Configurations tab, locate the required scaling configuration, and click **Delete** in the **Actions** column. 

    ![Delete scaling configurations - Delete single scaling configuration](images/21331_en-US.png)

    If you decide to delete multiple scaling configurations, select multiple scaling configurations, and click **Delete** in the **Scaling Configuration Name/ID** column.

    ![Delete scaling configurations - Delete multiple scaling configurations](images/21332_en-US.png)

5.  In the Delete Scaling Configuration dialog box, click **Confirm**. 

