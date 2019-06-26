# Create a predictive scaling rule {#task_266223 .task}

Predictive scaling rules are used to analyze historical monitoring data in a scaling group and predict the values of monitored metrics by means of machine learning. Scheduled tasks can be automatically created for the predictive scaling rule to set the boundary values of the scaling group intelligently. This topic describes how to create a predictive scaling rule.

When creating a scaling group, you can set its boundary values, namely, the maximum and minimum number of ECS instances for scaling. However, the boundary values you set may not meet the actual requirements. If the minimum number of ECS instances is too large, excessive computing resources may be purchased. If the maximum number of ECS instances is too small, service stability may be affected due to insufficient computing resources.

A predictive scaling rule can obtain historical monitoring data generated in a period of at least the past 24 hours, and then predict the values of monitored metrics in the next 48 hours through machine learning. Then, the number of ECS instances required by the scaling group per hour \(predicted value\) can be calculated. Forecasts are updated once a day, and 48 forecast tasks are created for each of the next 48 hours. Forecast tasks change the boundary values of the scaling group, but not the actual number of ECS instances in the scaling group.

A predictive scaling rule can be used together with target tracking scaling rules and simple scaling rules. When it is used with a target tracking scaling rule, we recommend that you set the same metrics and target values for the rules, to prevent variation of the number of ECS instances caused by the difference in metrics.

1.   Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess). 
2.   On the Scaling Groups page, locate the row that contains the target scaling group and click **Manage** in the **Actions** column. 
3.   In the left-side navigation pane, click Scaling Rules. On the page that appears, click **Create Scaling Rule** in the upper-right corner. 
4.   Set the parameters as needed, and then click **Create Scaling Rule**. A scaling group can have only one predictive scaling rule. The following table describes the parameters of a predictive scaling rule.

    |Parameter|Description|
    |---------|-----------|
    | **Rule Name** |The name of the scaling rule.|
    | **Rule Type** |The type of the scaling rule. Select **Predictive Scaling Rule**.|
    | **Reference Existing Target Tracking Scaling Rule** |If you select this option, the **Select Rule** field appears for you to select a target tracking scaling rule.|
    | **Select Rule** |The target tracking scaling rule for the new predictive scaling rule to reference. This field appears when you select **Reference Existing Target Tracking Scaling Rule**. After you select a target tracking scaling rule, its **Metric Name** and **Target Value** apply to the new predictive scaling rule.|
    | **Metric Name** |The name of a metric that CloudMonitor will monitor. Valid values:     -   Average CPU Usage \(%\)
    -   Average Inbound Internal Traffic \(KB/Min\)
    -   Average Outbound Internal Traffic \(KB/Min\)
 |
    | **Target Value** |The target value of the selected metric that CloudMonitor will monitor. The predictive scaling rule calculates an appropriate predicted value based on the target value and other factors. If you change the target value, existing forecast tasks of the current scaling group will be cleared, and new forecast tasks will be created within an hour.

 |
    | **Predictive Scaling Mode** |The forecast mode for the scaling group. Valid values:     -    **Forecast and Scale**: produces forecasts and creates forecast tasks.
    -    **Forecast Only**: produces forecasts but does not create forecast tasks.
 We recommend that you select **Forecast Only** first and change it to **Forecast and Scale** after confirming that the forecasts meet your expectations. You can [check the result of the predictive scaling rule](reseller.en-US/User Guide/Maintain Auto Scaling/Check the result of a predictive scaling rule.md#) on the details page.

 |
    | **Initial Max Capacity** |The maximum number of ECS instances in the scaling group. This parameter is used together with **Max Capacity Behavior**. The default value is the current value of **Maximum Instances**.

 |
    | **Max Capacity Behavior** |The action taken on the predicted value when it exceeds **Initial Max Capacity**. Valid values:     -    **Predicted Max Capacity Overwrites Initial Max Capacity**: uses the predicted value as the maximum value for forecast tasks.
    -    **Initial Max Capacity Overwrites Predicted Max Capacity**: uses the initial maximum capacity as the maximum value for forecast tasks.
    -    **Increase Predicted Max Capacity by Specified Ratio**: increases the predicted value with a specified ratio before comparing it with the initial maximum capacity. When you select this option, the **Increase Ratio** field appears for you to set the ratio.
 The default value is **Predicted Max Capacity Overwrites Initial Max Capacity**.

 |
    | **Increase Ratio** |The ratio of the increment to the predicted value. This field appears when you set **Max Capacity Behavior** to **Increase Predicted Max Capacity by Specified Ratio**. If the predicted value increased with this ratio is greater than the initial maximum capacity, the predicted value after increase is used as the maximum value for forecast tasks. The default value is 0, and the maximum value is 100.

 |
    | **Scheduled Task Buffer Time \(minutes\)** |The amount of buffer time ahead of the forecast task execution time. By default, all scheduled tasks that are automatically created for a predictive scaling rule are executed at the beginning of each hour. You can set a buffer time to execute forecast tasks ahead of schedule, so that resources can be prepared in advance. The default value is 0, and the maximum value is 60.

 |


