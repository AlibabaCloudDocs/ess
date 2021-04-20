# Use performance metrics to measure Auto Scaling

You can set weights for different instance types based on performance metrics such as the number of vCPUs. You can specify the capacity of a single instance of a specific instance type in a scaling group. After the weights are set, Auto Scaling can measure the capacity of a scaling group by using performance metrics. This helps you determine the overall performance of a scaling group in a more precise manner.

By default, Auto Scaling measures the capacity of a scaling group based on the number of ECS instances in the scaling group. If you specify only a single instance type in the active scaling configuration of a scaling group, the number of instances in the scaling group is proportional to the overall performance of the scaling group. However, if you specify multiple instance types that have different specifications in the active scaling configuration of a scaling group and create instances of multiple instance types, the number of instances in the scaling group cannot precisely reflect the overall performance of the scaling group. For example, the performance of 10 ecs.c5.xlarge \(4 vCPUs and 8 GiB memory\) instances is twice that of 10 ecs.c5.large \(2 vCPUs and 4 GiB memory\) instances.

You can specify the weights of instance types. Even if Auto Scaling creates multiple instances of different instance types in a scaling group, you can precisely measure the performance of the scaling group. For example, if you set the weights of instance types based on the number of vCPUs in a scaling group, the capacity of the scaling group indicates the total number of vCPUs of all instances in the scaling group.

## Terms

|Term|API parameter|Description|
|----|-------------|-----------|
|weight|WeightedCapacity|The weight of an instance type. You can set the weight of an instance type based on performance metrics such as the number of vCPUs. You can specify the capacity of a single instance of a specific instance type in a scaling group.|
|total capacity|TotalCapacity|The total capacity of all instances in a scaling group.|
|maximum capacity|MaxSize|The maximum value of the total capacity of a scaling group. **Note:** After a scale-out event is executed in a scaling group, the total capacity of the scaling group may exceed the maximum capacity. This is because the maximum capacity may not be divisible by the weight of a single instance type. However, the extra capacity is less than the maximum weight. |
|minimum capacity|MinSize|The minimum value of the total capacity of a scaling group.|
|expected capacity|DesiredCapacity|The expected value of the total capacity of a scaling group. Auto Scaling ensures that the total capacity is no less than the expected capacity. **Note:** After a scale-out event is executed in a scaling group, the total capacity of the scaling group may exceed the expected capacity. This is because the expected capacity may not be divisible by the weight of a single instance type. However, the extra capacity is less than the maximum weight. |

## Rules for scaling

-   When the total capacity of a scaling group is less than the expected capacity or the minimum capacity, scale-out events are triggered.
-   When the total capacity of a scaling group is greater than or equal to the sum of the expected capacity and the maximum weight, scale-in events are triggered.

**Note:** Auto Scaling performs automatic scaling based preferentially on the scaling policy specified for a scaling group. If you configure a cost optimization policy for a scaling group, Auto Scaling creates instances based on the weighted unit prices in ascending order. Auto Scaling releases instances based on the weighted unit prices in descending order. For information about how to calculate weighted unit prices, see [Calculation of weighted unit prices](#section_ldj_gae_z0y).

## Usage notes

-   You must set weights for all instance types in a scaling group.
-   If you delete an instance type specified in the active scaling configuration of a scaling group, the weights of instances of this instance type remain unchanged in the scaling group.
-   After you modify the weight of an instance type in a scaling group, Auto Scaling recalculates the capacity of the scaling group based on the modified weight if instances of this instance type have been created. **Scaling activities may be triggered**.

## Procedure

In this example, a scaling configuration is used as the configuration source of a scaling group to set the weights of instance types.

**Note:** You can also use a launch template as the configuration source. You can specify the LaunchTemplateOverride.N.InstanceType and LaunchTemplateOverride.N.WeightedCapacity parameters in the CreateScalingGroup operation to set the weights of instance types. For more information, see [CreateScalingGroup](/intl.en-US/API Reference/Scaling group/CreateScalingGroup.md).

1.  Create a scaling group.

    This step describes the parameters related to the multi-zone scaling policy. For information about other parameters of a scaling group, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md).

    1.  Set Network Type to **VPC** and select multiple vSwitches in the same VPC.

        One vSwitch belongs to only one zone. After you configure multiple vSwitches for the scaling group, Auto Scaling can create ECS instances in multiple zones. This helps you utilize available ECS resources in different zones.

    2.  Set Multi-zone Scaling Policy to **Cost Optimization Policy**.

    3.  Configure other parameters for the scaling group.

2.  Create a scaling configuration.

    This step describes the parameters for setting the weight of an instance type based on the number of vCPUs. For information about other parameters of a scaling configuration, see [Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md).

    1.  Set Billing Method to **Pay-As-You-Go**.

    2.  Select multiple instance types. You can select up to 10 instance types.

    3.  Select **Set vCPU Capacity**. By default, the system sets weights for all selected instance types based on the number of vCPUs.

        ![Set weights](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1630198161/p240942.png)

        You can customize the weights of instance types. When you customize weights, we recommend that you take note of the following items:

        -   Use performance metrics related to instance types to set weights. For example, you can set weights based on the number of CPU cores or the amount of memory. You can use an instance type that has 1 vCPU and 1 GiB memory or provides the minimum performance as the capacity unit of a scaling group. The capacity of the scaling group is calculated based on the capacity unit.
        -   Set appropriate weight values to ensure that the current capacity of a scaling group is two to three times the maximum weight of instance types.
        -   Set the weights of different instance types to values that have small differences. For example, do not set the weight of an instance type that has lower specifications to 1 and the weight of an instance type that has higher specifications to 200. If the difference between the weights of instance types in a scaling group is large, the overall costs of the scaling group may increase.
        For information about the priority of multiple instance types when they are used to create instances, see [Calculation of weighted unit prices](#section_ldj_gae_z0y).

    4.  Configure other parameters for the scaling configuration.

3.  Enable the scaling group.

4.  Create a scaling rule.

    This step describes the parameters for creating a simple scaling rule to verify the cost optimization policy. For information about other parameters of a scaling rule, see [Create a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Create a scaling rule.md).

    1.  Set Rule Type to **Simple Scaling Rule**.

    2.  Set Operation to **Add 10 Capacity Unit**.

    3.  Configure other parameters for the scaling rule.

5.  Execute the scaling rule.

    In this example, the weighted unit price of the ecs.c5.2xlarge instance type is the lowest. Therefore, Auto Scaling creates two instances of the ecs.c5.2xlarge instance type for the scaling group. This adds 16 capacity units to the scaling group.


## Calculation of weighted unit prices

If you set the multi-zone scaling policy to **Cost Optimization Policy** for a scaling group and set the weights of instance types, Auto Scaling attempts to create instances based on the weighted unit prices in ascending order. For more information, see [Reduce costs by configuring a cost optimization policy](/intl.en-US/Best practices/Reduce costs by configuring a cost optimization policy.md).

The following table provides examples on how to calculate weighted unit prices of different instance types.

**Note:** The market prices of instance types in the following table are for reference only. For information about the actual market prices, see the [Pricing](https://www.alibabacloud.com/product/ecs) tab on the Elastic Compute Service page.

|Instance type|vCPU|Market price|Weight|Weighted unit price|
|-------------|----|------------|------|-------------------|
|ecs.c5.large|2|USD 0.073/Hour|2|USD 0.037/Hour|
|ecs.c5.xlarge|4|USD 0.144/Hour|4|USD 0.036/Hour|
|ecs.c5.2xlarge|8|USD 0.288/Hour|8|USD 0.036/Hour|

