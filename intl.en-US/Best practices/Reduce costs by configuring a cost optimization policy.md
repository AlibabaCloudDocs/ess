# Reduce costs by configuring a cost optimization policy

This topic describes how to configure a cost optimization policy for a scaling group. A cost optimization policy can be used to create multiple types of ECS instances across different zones. This increases the success rate of creating ECS instances and reduces costs.

-   Before you perform the operations provided in the tutorial, you must have registered an Alibaba Cloud account. To create an Alibaba Cloud account, click [Create a new Alibaba Cloud account](https://account.alibabacloud.com/register/intl_register.htm).
-   A virtual private cloud \(VPC\) is created. For more information, see [Create a VPC](/intl.en-US/VPCs and VSwitches/VPC management/Create a VPC.md).
-   Multiple VSwitches are created across different zones of the VPC. For more information, see [Create a VSwitch](/intl.en-US/VPCs and VSwitches/VSwitch management/Create a VSwitch.md).

Auto Scaling supports creating ECS instances of multiple instance types in a scaling group. You can specify multiple instance types in a scaling configuration. Auto Scaling creates instances based on the priorities of the instance types. If resources of the instance type with the highest priority are insufficient, Auto Scaling automatically attempts to use the instance type with the next highest priority to create instances. This increases the success rate of creating ECS instances when resources of a specific instance type are insufficient. During business peaks, ECS instances of instance types that have higher specifications are required to respond to business requirements in a timely manner. In this case, Auto Scaling must focus on creating ECS instances with sufficient performance, instead of creating ECS instances of a specific instance type.

Auto Scaling supports creating ECS instances across different zones. You can select multiple VSwitches that are located in different zones when you create a scaling group. If the zone where a VSwitch resides does not have sufficient ECS instance resources, Auto Scaling automatically attempts to create instances in other zones. This increases the success rate of creating ECS instances. After you configure multiple zones, you can also configure a multi-zone scaling policy based on your actual business needs. Multi-zone scaling policies include priority policies, balanced distribution policies, and cost optimization policies.

**Note:**

-   Multi-zone scaling policies are available only for VPC-connected scaling groups.
-   The multiple-zone scaling policy of a scaling group cannot be modified.

Auto Scaling cannot create a preemptible instance when the market price of the instance exceeds your bid. This may affect your service. To avoid this issue, you can set your multi-zone scaling policy to cost optimization policy. If a preemptible instance fails to be created, Auto Scaling automatically attempts to create a pay-as-you-go instance of the same instance type. This increases the success rate of creating ECS instances and reduces costs. You can configure a cost optimization policy and multiple instance types at the same time to further increase the success rate of scaling. Auto Scaling attempts to create ECS instances in the scaling group that applies the cost optimization policy based on the unit prices of vCPUs in ascending order. Even if you set the billing method to pay-as-you-go, the cost optimization policy ensures that you can use ECS instance resources at the lowest cost.

## Procedure

1.  Create a scaling group.

    This step describes parameters related to the multi-zone scaling policy. For more information about other parameters of the scaling group, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md).

    1.  Set the network type to **VPC** and select multiple VSwitches in the same VPC.

        A VSwitch belongs to only one zone. After you configure multiple VSwitches for the scaling group, the scaling group can create ECS instances in multiple zones. This helps you utilize available ECS resources in different zones based on your requirements.

    2.  Set the multi-zone scaling policy to **Cost Optimization Policy**.

    3.  Configure other parameters.

2.  Create a scaling configuration.

    This step describes parameters related to the multi-zone scaling policy. For more information about other parameters of the scaling configuration, see [Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md).

    1.  Set the billing method to **Preemptible Instance**.

    2.  Select multiple instance types. You can select up to 10 instance types.

        -   We recommend that you select instance types with similar performance in terms of the vCPU, memory, physical processor, clock speed, internal network bandwidth, or packet forwarding rate.
        -   We recommend that you set a maximum bid for each instance type. If you use automatic bidding, Auto Scaling bids for and creates preemptible instances at the market price.
        -   The configurations of I/O optimized instances vary greatly from those of non-I/O optimized instances. If you choose these two types of instances at the same time, the success rate of creating instances cannot be significantly increased.
    3.  Configure other parameters.

3.  Enable the scaling group.

4.  Create a scaling rule.

    This step describes parameters for creating a simple scaling rule to verify the cost optimization policy. For more information about other parameters of the scaling rule, see [Create a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Create a scaling rule.md).

    1.  Set Rule Type to **Simple Scaling Rule**.

    2.  Set Operation to **Add 1 Instances**.

    3.  Configure other parameters.

5.  Execute the scaling rule.


## Verification

Assume that in the preceding procedure, you have specified a VSwitch in Qingdao Zone B and a VSwitch in Qingdao Zone C for the scaling group, and specified the ecs.sn1.large and ecs.sn1.xlarge instance types for the scaling configuration. The billing method is set to Preemptible Instance. Therefore, instances of a specific instance type have two unit prices of vCPUs. One is for preemptible instances, and the other is for pay-as-you-go instances.

**Note:** The prices listed in this topic are only for reference. Refer to the buy page of ECS instances for actual prices.

![Example of preemptible instance prices](../images/p37634.png)

Based on the preceding settings of the instance types and billing method, you have four plans for creating instances. The following table lists the four plans by vCPU unit price in ascending order.

|No.|Instance Type|Billing method|vCPU|Market price of instance \(RMB per hour\)|Unit price of vCPU \(RMB per hour\)|
|---|-------------|--------------|----|-----------------------------------------|-----------------------------------|
|Plan 1|ecs.sn1.xlarge|Preemptible instance|8|0.158|0.01975|
|Plan 2|ecs.sn1.large|Preemptible instance|4|0.088|0.022|
|Plan 3|ecs.sn1.xlarge|Pay-as-you-go|8|1.393|0.174125|
|Plan 4|ecs.sn1.large|Pay-as-you-go|4|0.697|0.17425|

Expected process for creating instances: During a scale-out event, Auto Scaling preferentially creates ECS instances based on Plan 1. If instances fails to be created in both Zone B and Zone C due to insufficient resources, Auto Scaling attempts to create ECS instances based on Plan 2, Plan 3, and Plan 4 in sequence.

Execute the scaling rule to trigger a scale-out event during which an ECS instance is created and added to the scaling group. In the Auto Scaling console, go to the ECS Instances page of the scaling group and click the created ECS instance to view its instance type and billing method. In this example, the instance type is **ecs.sn1.xlarge** and the billing method is **Pay-As-You-Go-Preemptible Instance**. This indicates that costs are reduced.

![Reduce costs by configuring a cost optimization policy - verification](../images/p37797.png)

