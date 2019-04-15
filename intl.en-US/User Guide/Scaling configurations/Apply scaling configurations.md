# Apply scaling configurations {#task406 .task}

In a scaling group, you can create multiple scaling configurations, but you can only apply one of these scaling configurations.

A scaling configuration includes many configuration items. You can obtain the overview of a scaling configuration by using the View Details function to ensure that an appropriate ECS instance template is applied.

1.  Log on to the [Auto Scaling Console](https://partners-intl.console.aliyun.com/#/ess). 
2.  On the Scaling Groups page, click **Manage** in the **Actions** column. 
3.  In the left-side navigation pane, select Instance Configuration Source. 
4.  In the left-side navigation pane, select Instance Configuration Source. On the Scaling Configurations tab, locate the scaling configuration to be applied, and click **View Details** in the **Actions** column. 
5.  If you decide to apply the scaling configuration, click **Apply** in the **Actions** column. 

    **Note:** After you apply a scaling configuration, the status of the other scaling configurations will switch to **Inactive**.


After you apply a scaling configuration, ECS instances that are created later will be automatically based on the scaling configuration in a scaling group when the specified scaling condition is met.

