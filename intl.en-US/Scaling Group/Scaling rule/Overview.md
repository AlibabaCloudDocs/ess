# Overview

The purpose of a scaling rule is determined by its type. A scaling rule can be used to trigger a scaling activity or set the minimum and maximum numbers of ECS instances for a scaling group. This topic describes the types and limits of scaling rules.

## Rule types

The following table describes the scaling rule types supported by Auto Scaling.

|Type|Purpose|Description|
|----|-------|-----------|
|Step scaling rule|A step scaling rule is used to trigger a scaling activity.|When you create a step scaling rule, you must associate an event-triggered task with the step scaling rule and configure a set of step scaling policies that are triggered based on the condition of the event-triggered task. Step scaling rules are similar to simple scaling rules, except that each simple scaling rule defines only one scaling policy. You can use a step scaling rule to precisely control the number of ECS instances to be scaled in a scaling group.|
|Predictive scaling rule|A predictive scaling rule is used to intelligently set the minimum and maximum numbers of ECS instances for a scaling group.|After a predictive scaling rule is executed in a scaling group, Auto Scaling analyzes historical monitoring data of the scaling group to predict the values of specified metrics by using machine learning. Auto Scaling can also automatically create scheduled tasks to help set the optimal minimum and maximum numbers of ECS instances for the scaling group.

However, the boundary values you set may not reflect the actual requirements. If the minimum number of ECS instances exceeds the actual requirements, you may purchase excess computing resources. If the maximum number of ECS instances cannot meet the actual requirements, the service stability may be affected due to insufficient computing resources. After a predictive scaling rule is executed, Auto Scaling can obtain historical monitoring data that is generated in a period of at least the past 24 hours. Based on the historical data, Auto Scaling predicts the values of monitored metrics over the next 48 hours by using machine learning. Then, Auto Scaling can calculate the number of ECS instances that are required by the scaling group per hour and provide the number as the predicted value. Predictions are updated once a day, and 48 prediction tasks are created for each of the next 48 hours.

**Note:** A predictive scaling rule changes only the minimum and maximum numbers of ECS instances for a scaling group, but does not scale ECS instances in the scaling group. |
|Target tracking scaling rule|A target tracking scaling rule is used to trigger a scaling activity.|When you create a target tracking scaling rule, you must select a Cloud Monitor metric and set a target value. Auto Scaling automatically calculates the number of ECS instances required to keep the metric close to the target value, and scales ECS instances accordingly. **Note:** After you create a target tracking scaling rule in a scaling group, Auto Scaling automatically creates an event-triggered task and associates this task with the target tracking scaling rule. When the metric of the scaling group reaches the target value, the event-triggered task is triggered to execute the associated target tracking rule. If the event-triggered task is no longer needed, you must delete the associated target tracking scaling rule. Then, Auto Scaling automatically deletes the event-triggered task. |
|Simple scaling rule|A simple scaling rule is used to trigger a scaling activity.|You can specify a simple scaling rule to increase or decrease the number of ECS instances in a scaling group by or to a specific number.|

A predictive scaling rule can be used together with a target tracking scaling rule or a simple scaling rule. When a predictive scaling rule is used with a target tracking scaling rule, we recommend that you set the same metric and target value for both rules. Otherwise, the number of instances in the scaling group may frequently change due to the difference in metrics.

## Limits

The following limits apply when you use scaling rules:

-   You can create only a limited number of scaling rules for a scaling group. For more information, see [Limits](/intl.en-US/Product Introduction/Limits.md).
-   After a scaling rule is executed, the actual number of ECS instances in the scaling group may fall outside of the specified range. In this case, Auto Scaling automatically adjusts the number of ECS instances to be added or removed to ensure that the number of ECS instances in the scaling group is within the specified range. Examples:
    -   You have a scaling group named asg-bp19ik2u5w7esjcu\*\*\*\*. The scaling group can contain up to three instances. One of its scaling rules named add3 specifies that three instances are added during a scaling activity. The scaling group contains two instances. If the add3 scaling rule is executed, only one ECS instance is added to the scaling group.
    -   You have a scaling group named asg-bp19ik2u5w7esjcu\*\*\*\*. The scaling group must contain at least two instances. One of its scaling rules named reduce2 specifies that two instances are removed during a scaling activity. The scaling group contains three instances. If the reduce2 scaling rule is executed, only one ECS instance is removed from the scaling group.
-   If you have overdue payments within your account, all scaling rules fail to be executed.

    **Note:** Make sure that you have sufficient balance within your account to ensure the service availability of Auto Scaling.


