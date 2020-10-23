# Create a scaling rule

The purpose of a scaling rule is determined by its type. A scaling rule can be used to trigger a scaling activity or set the minimum and maximum numbers of Elastic Compute Service \(ECS\) instances for a scaling group. This topic describes how to create a scaling rule.

Auto Scaling supports four types of scaling rules. For information about the purposes and limits of scaling rules, see [Scaling rule overview](/intl.en-US/Scaling Group/Scaling rule/Scaling rule overview.md)

You can create only a limited number of scaling rules for a scaling group. For more information, see [Limits](/intl.en-US/Product Introduction/Limits.md).

## Procedure

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  Find the scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   Click **Details** in the **Actions** column.
3.  In the upper part of the page, click the **Scaling Rules** tab.

4.  Click **Create Scaling Rule**.

5.  In the Create Scaling Rule dialog box, configure parameters for the scaling rule.

    1.  Enter a scaling rule name.

    2.  Select a scaling rule type and configure the related parameters.

        **Note:** You cannot change the type of a scaling rule after the scaling rule is created.

        For information about parameters for different types of scaling rules, see [Parameter description for a step scaling rule](#table_k3g_2e4_d5k), [Parameter description for a predicative scaling rule](#table_sa7_0zz_g31), [Parameter description for a target tracking scaling rule](#table_ket_pwt_d92), or [Parameter description for a simple scaling rule](#table_58k_037_d3u).

        -   Parameters for a step scaling rule

            |Parameter|Description|
            |---------|-----------|
            |**Monitoring Type**|Select a monitoring type based on the event-triggered task to be associated with the scaling rule.             -   **System Monitoring**: Select this option to associate a system monitoring event-triggered task with the scaling rule.
            -   **Custom Monitoring**: Select this option to associate a custom monitoring event-triggered task with the scaling rule. |
            |**Start Time**|Specify an event-triggered task to be associated with the scaling rule. The condition of the event-triggered task are used as the reference for triggering step scaling operations. For example, you can select an event-triggered task that generates an alert when the average CPU utilization is greater than or equal to 80% three times in a row.

If no event-triggered tasks are available, you can create one. For more information, see [Create event-triggered tasks](/intl.en-US/Automatic Scaling/Alarm tasks/Create a monitoring task.md).

**Note:** If an event-triggered task is created when you create a step scaling rule, the event-triggered task automatically uses the current step scaling rule as the trigger rule and the current scaling group as the monitoring resource. |
            |**Operation**|Specify step scaling operations based on the condition of the event-triggered task. To set a step scaling operation, you must specify the size of the alert breach and the corresponding operation. When the event-triggered task generates an alert, Auto Scaling performs a step scaling operation based on the size of the alert breach. You must set at least one step scaling operation. Examples:

            -   Adds two ECS instances when the average CPU utilization is greater than or equal to 80% but less than 90%.
            -   Adds three ECS instances when the average CPU utilization is greater than or equal to 90%.
The size of the alert breach for each step scaling operation must be set based on the condition of the event-triggered task. For example, if the condition is that the average CPU utilization is greater than or equal to 80% three times in a row, the lower limit of the alert breach for the initial step scaling operation must be greater than or equal to 80%.

Step scaling rules support the same operations as simple scaling rules, including changing to N instances, adding N instances, removing N instances, adding instances by N%, and removing instances by N%. |
            |**Instance Warmup Time**|The instance warmup period. Unit: seconds. Auto Scaling adds instances in the warmup state to a scaling group, but does not report monitoring data to Cloud Monitor during the warmup period. When Auto Scaling calculates the number of instances to be scaled based on the Cloud Monitor metric, Auto Scaling does not count instances in the warmup state as existing instances in the scaling group. Otherwise, the metric value may change when the warmup period expires. Assume that the instance warmup period is 300 seconds and two ECS instances are added to the scaling group. Within 300 seconds after the two ECS instances are created, Auto Scaling does not take the two instances into account when Auto Scaling calculates the average CPU utilization of ECS instances in the scaling group. |

        -   Parameters for a predictive scaling rule

            **Note:** A scaling group can have only one predictive scaling rule.

            |Parameter|Description|
            |---------|-----------|
            |**Reference Existing Target Tracking Scaling Rule**|Specifies whether to reference an existing target tracking scaling rule. If a target tracking scaling rule exists in the scaling group, you can use the values of **Metric Type** and **Target Value** specified in the target tracking scaling rule.|
            |**Select a rule**|This parameter appears when you select **Reference Existing Target Tracking Scaling Rule**. After you select a target tracking scaling rule, the values of **Metric Type** and **Target Value** specified in the target tracking scaling rule apply to the predictive scaling rule.|
            |**Metric Type**|The name of a Cloud Monitor metric to be monitored. Valid values:             -   **\(ECS\) Average CPU Utilization**. Unit: %.
            -   **\(ECS\) Average Inbound Internal Traffic**. Unit: KB/min.
            -   **\(ECS\) Average Outbound Internal Traffic**. Unit: KB/min. |
            |**Target Value**|The target value of the metric to be monitored by Cloud Monitor. The predictive scaling rule calculates an appropriate predicted value based on multiple factors such as the target value. If you change the target value, existing prediction tasks of the current scaling group are cleared. New prediction tasks are created within an hour. |
            |**Predicative Mode**|The prediction mode for the scaling group. Valid values:             -   **Predict Only**: produces predictions but does not create prediction tasks.
            -   **Predict and Scale**: produces predictions and creates prediction tasks.
We recommend that you first select **Predict Only** and change it to **Predict and Scale** if you confirm that the predictions can meet your requirements. You can view the prediction results in the details of the scaling rule. For more information, see [Check the result of a predictive scaling rule](/intl.en-US/Scaling Group/Scaling rule/Evaluate the prediction of a predictive scaling rule.md). |
            |**Preset Max Capacity**|The maximum number of ECS instances in the scaling group. This parameter is used together with **Maximum Capacity Handling Method**. The default value is the maximum number of instances in the current scaling group. |
            |**Maximum Capacity Handling Method**|The action to be taken on the predicted value when it exceeds the preset maximum capacity. Valid values:             -   **Predicted Capacity Overwrites Preset Max Capacity**: uses the predicted value as the maximum value for prediction tasks.
            -   **Preset Max Capacity Overwrites Predicted Capacity**: uses the preset maximum capacity as the maximum value for prediction tasks.
            -   **Predicted Capacity with Additional Ratio**: increases the predicted value with a specified ratio before the system compares it with the preset maximum capacity. When you select this option, the **Increase Ratio** parameter appears. This allows you to set the ratio.
Default value: **Predicted Capacity Overwrites Preset Max Capacity** |
            |**Increase Ratio**|The ratio of the increment to the predicted value. This parameter appears when you set **Maximum Capacity Handling Method** to **Predicted Capacity with Additional Ratio**. The current predicted value increases with this ratio, and the predicted value after increase is used as the maximum value for prediction tasks. For example, if the current predicted value is 100 and increases with a ratio of 10%, the maximum value for prediction tasks is 110. Valid values: 0 to 100. Default value: 0. |
            |**Pre-launch Time**|The buffer time before prediction tasks are executed. By default, all scheduled tasks that are automatically created for a predictive scaling rule are executed on the hour. You can set a buffer time to execute prediction tasks ahead of schedule so that resources can be prepared in advance. Valid values: 0 to 60. Default value: 0. |

        -   Parameters for a target tracking scaling rule

            |Parameter|Description|
            |---------|-----------|
            |**Reference Existing Predictive Scaling Rule**|Specifies whether to reference an existing target tracking scaling rule. If a predictive scaling rule exists in the scaling group, you can specify whether to inherit the metric and target value from the predictive scaling rule.|
            |**Metric Type**|The name of a Cloud Monitor metric to be monitored. Valid values:             -   **\(ECS\) Average CPU Utilization**
            -   **\(ECS\) Average Inbound Internal Traffic**
            -   **\(ECS\) Average Outbound Internal Traffic**
            -   **\(ECS\) Average Inbound Public Traffic**
            -   **\(ECS\) Average Outbound Public Traffic** |
            |**Target Value**|The target value of the Cloud Monitor metric. The target tracking scaling rule keeps the Cloud Monitor metric close to the target value.|
            |**Instance Warmup Time**|The instance warmup period. Unit: seconds. Auto Scaling adds instances in the warmup state to a scaling group, but does not report monitoring data to Cloud Monitor during the warmup period. When Auto Scaling calculates the number of instances to be scaled based on the Cloud Monitor metric, Auto Scaling does not count instances in the warmup state as existing instances in the scaling group. Otherwise, the metric value may change when the warmup period expires.|
            |**Disable Scale-in**|Specifies whether to disable scale-in events. This parameter affects the number of automatically created event-triggered tasks.             -   If this parameter is selected, only one event-triggered task for scale-out events is automatically created and associated with the target tracking scaling rule. Then, the target tracking scaling rule cannot remove ECS instances from the scaling group.
            -   If this parameter is not selected, two event-triggered tasks are automatically created and associated with the target tracking scaling rule. One task is used for scale-out events, and the other task is used for scale-in events. |

        -   Parameters for a simple scaling rule

            |Parameter|Description|
            |---------|-----------|
            |**Operation**|The operation to be executed when the scaling rule is triggered. Valid values:             -   Change to N Instances: When the scaling rule is executed, the number of instances in the scaling group is changed to N. A maximum of 500 instances can be added to or removed from a scaling group at a time.
            -   Add N Instances: When the scaling rule is executed, N instances are added to the scaling group. A maximum of 500 instances can be added to a scaling group at a time.
            -   Add Instances by N%: When the scaling rule is executed, N% of the number of existing instances in the scaling group are added. A maximum of 500 instances can be added to a scaling group at a time.
            -   Remove N Instances: When the scaling rule is executed, N instances are removed from the scaling group. A maximum of 500 instances can be removed from a scaling group at a time.
            -   Remove Instances by N%: When the scaling rule is executed, N% of the number of existing instances in the scaling group are removed. A maximum of 500 instances can be removed from a scaling group at a time. |
            |**Cooldown Time**|Optional. The cooldown period. Unit: seconds. If this parameter is not specified, the cooldown period of the scaling group is used. For more information, see [Cooldown time](/intl.en-US/Scaling Group/Scaling group/Cooldown time.md).|

6.  Click **OK** to create the scaling rule.


**Related topics**  


[CreateScalingRule](/intl.en-US/API Reference/Scaling rule/CreateScalingRule.md)

