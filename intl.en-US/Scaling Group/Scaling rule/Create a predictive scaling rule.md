# Create a predictive scaling rule

This topic describes how to create a predictive scaling rule. After a predictive scaling rule is executed, Auto Scaling analyzes historical monitoring data of a scaling group to predict the values of specified metrics by using machine learning. Auto Scaling can also automatically create scheduled tasks to help set the optimal minimum and maximum numbers of ECS instances for the scaling group.

A target tracking scaling rule is created if you want to reference one.

When you create a scaling group, you can manually set the boundary values: minimum and maximum numbers of ECS instances for the scaling group. However, the boundary values you set may not reflect the actual requirements. If the minimum number of ECS instances exceeds the actual requirements, you may purchase excess compute resources. If the maximum number of ECS instances cannot meet the actual requirements, the service stability may be affected due to insufficient compute resources.

After a predictive scaling rule is executed, Auto Scaling can obtain historical monitoring data that is generated in a period of at least the past 24 hours. Based on the historical data, Auto Scaling predicts the values of monitored metrics over the next 48 hours by using machine learning. Then, Auto Scaling can calculate the number of ECS instances that are required by the scaling group per hour and provide the number as the predicted value. Predictions are updated once a day, and 48 prediction tasks are created for each of the next 48 hours. Prediction tasks change the boundary values of the scaling group, but not the actual number of ECS instances in the scaling group.

A predictive scaling rule can be used together with a target tracking scaling rule or a simple scaling rule. When the predictive scaling rule is used together with a target tracking scaling rule, we recommend that you set the same metric and target value for both rules. Otherwise, the number of instances in the scaling group may frequently change due to the difference in metrics.

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Find the scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   Click **Details** in the **Actions** column.
5.  In the upper part of the page, click the **Scaling Rules** tab.

6.  Click **Create Scaling Rule**.

7.  Configure parameters and click **OK**.

    A scaling group can have only one predictive scaling rule. The following table describes the parameters of a predictive scaling rule.

    |Parameter|Description|
    |---------|-----------|
    |**Rule Name**|The name of the scaling rule.|
    |**Rule Type**|The type of the scaling rule. Select **Predictive Scaling Rule**.|
    |**Reference Existing Target Tracking Scaling Rule**|Specifies whether to use the predictive scaling rule with a target tracking scaling rule. If you select this option, **Select a rule** appears. Then, you can select a target tracking scaling rule.|
    |**Select a rule**|The target tracking scaling rule for the predictive scaling rule to reference. This parameter appears when you select **Reference Existing Target Tracking Scaling Rule**. After you select a target tracking scaling rule, its **Metric Type** and **Target Value** apply to the predictive scaling rule.|
    |**Metric Type**|The metric to be monitored by Cloud Monitor. Valid values:     -   **\(ECS\) Average CPU Utilization**. Unit: %.
    -   **\(ECS\) Average Inbound Internal Traffic**. Unit: KB/min.
    -   **\(ECS\) Average Inbound Internal Traffic**. Unit: KB/min. |
    |**Target Value**|The target value of the metric to be monitored by Cloud Monitor. The predictive scaling rule calculates an appropriate predicted value based on multiple factors such as the target value. If you change the target value, existing prediction tasks of the current scaling group will be cleared. New prediction tasks will be created within an hour. |
    |**Predicative Mode**|The prediction mode for the scaling group. Valid values:     -   **Predict Only**: produces predictions but does not create prediction tasks.
    -   **Predict and Scale**: produces predictions and creates prediction tasks.
We recommend that you first select **Predict Only** and change it to **Predict and Scale** if the predictions meet your expectations. You can view the prediction result in the scaling rule details. For more information, see [Check the result of a predictive scaling rule](/intl.en-US/Scaling Group/Scaling rule/Evaluate the prediction of a predictive scaling rule.md). |
    |**Preset Max Capacity**|The maximum number of ECS instances in the scaling group. This parameter is used together with **Maximum Capacity Handling Method**. The default value is the current maximum number of instances in the scaling group. |
    |**Maximum Capacity Handling Method**|The action to be taken on the predicted value when it exceeds the preset maximum capacity. Valid values:     -   **Predicted Capacity Overwrites Preset Max Capacity**: uses the predicted value as the maximum value for prediction tasks.
    -   **Preset Max Capacity Overwrites Predicted Capacity**: uses the preset maximum capacity as the maximum value for prediction tasks.
    -   **Predicted Capacity with Additional Ratio**: increases the predicted value with a specific ratio before comparing it with the preset maximum capacity. When you select this option, the **Increase Ratio** parameter appears. This allows you to set the ratio.
Default value: **Predicted Capacity Overwrites Preset Max Capacity** |
    |**Increase Ratio**|The ratio of the increment to the predicted value. This parameter appears when you set **Maximum Capacity Handling Method** to **Predicted Capacity with Additional Ratio**. The current predicted value increases with this ratio, and the predicted value after increase is used as the maximum value for prediction tasks. For example, if the current predicted value is 100 and increases with a ratio of 10%, the maximum value for prediction tasks is 110. Valid values: 0 to 100. Default value: 0. |
    |**Pre-launch Time**|The buffer time before prediction tasks are executed. By default, all scheduled tasks that are automatically created for a predictive scaling rule are executed on the hour. You can set a buffer time to execute prediction tasks ahead of schedule so that resources can be prepared in advance. Valid values: 0 to 60. Default value: 0. |


**Related topics**  


[CreateScalingRule](/intl.en-US/API Reference/Scaling rule/CreateScalingRule.md)

