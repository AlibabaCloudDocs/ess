# Reduce costs by configuring scaling policies {#concept_ox4_sfh_mgb .concept}

This topic describes how to configure policies to reduce application costs by using multiple ECS instance types and multiple available zones. These policies increase the success rate of automatic scaling and also reduce costs.

## Background information {#section_r5x_j23_mgb .section}

Auto Scaling supports multiple instance types and allows you to specify alternative ECS instance types in a scaling configuration. Auto Scaling will attempt to create the ECS instance type that has the highest priority. If the ECS instance type of the highest priority is unavailable, Auto Scaling will attempt to create an ECS instance type of the next highest priority, until the specified number of ECS instances are created. If you configure multiple ECS instance types, Auto Scaling can still create instances when certain instance types are unavailable. This ensures that scaling activities can still be executed. During peak traffic periods, you may need to quickly create ECS instances to bear traffic. In this case, performance is prioritized over creating instances that comply with your cost requirements. You can set multiple instance types so that Auto Scaling can scale out to meet urgent demands.

Auto Scaling supports multiple zones. You can specify multiple VSwitches when creating a scaling group. If the zone where a VSwitch is located does not have sufficient ECS instances in stock, Auto Scaling will create ECS instances in other zones to ensure that instances are sufficient to execute scaling activities. After configuring multiple zones, you can also configure scaling policies based on your actual business needs. Multi-zone scaling policies include priority policies, distribution balancing polices, and cost optimization policies. For more information, see [Multi-zone scaling policies](../../../../reseller.en-US/User Guide/Use custom scaling configurations to create scaling groups.md#hxfive).

As [preemptible instances](../../../../reseller.en-US/Instances/Instance purchasing options/Preemptible instances/Preemptible instances.md#) are subject to market prices, failures of bidding such instances may delay scale-out activities, affecting your businesses. To avoid negative impact on your businesses, you can choose to configure a cost optimization policy. When Auto Scaling fails to create preemptible instances, the scaling group will automatically create the same number of Pay-As-You-Go instances of the same type as the preemptible instances. This ensures a high success rate for scaling activities and controls costs. You can configure a cost optimization policy and multiple instances types at the same time to increase the scaling success rate. Scaling groups that apply cost optimization policies will attempt to create ECS instances based on the unit price of vCPUs, from low to high. Even if you have not specified any preemptible instances, this method ensures that you can use ECS instance resources at the lowest cost.

## Notes {#section_ebr_k23_mgb .section}

-   Multi-zone scaling policies are available only for scaling groups whose network type is set to VPC.
-   The multi-zone scaling policy of a scaling group cannot be modified.

## Preparations {#section_spx_ktn_mgb .section}

Before creating a scaling group that applies a cost optimization policy, make sure you have completed the following preparations:

-   You have created a VPC. For more information, see [Create a VPC](../../../../reseller.en-US/User Guide/VPC and subnets/Manage a VPC.md#).
-   You have created multiple VSwitches in different zones of the created VPC. For more information, see [Create VSwitches](../../../../reseller.en-US/User Guide/VPC and subnets/Manage VSwitches.md#).

## Procedure {#section_hxj_4f3_mgb .section}

**Note:** The following section introduces multi-zone scaling polices. For more information about creating a scaling group, see [Use custom scaling configurations to create scaling groups](../../../../reseller.en-US/User Guide/Use custom scaling configurations to create scaling groups.md#) or [Use launch templates to create scaling groups](../../../../reseller.en-US/User Guide/Use launch templates to create scaling groups.md#).

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  On the Create Scaling Group page, set **Network Type** to **VPC** and select multiple VSwitches belonging to a VPC.

    **Note:** Because a VSwitch belongs to only one zone, you can create ECS instances in multiple zones after selecting multiple VSwitches. This helps you make use of ECS instance inventory in different zones.

3.  On the Create Scaling Group page, set **Multi-Zone Scaling Policy** to **Cost Optimization**.
4.  Configure other parameters as required.
5.  [Create a scaling configuration](../../../../reseller.en-US/User Guide/Scaling configurations/Create a scaling configuration.md#) for the scaling group. In the configuration, set **Billing Method** to **Preemptible Instance** and choose multiple instance types \(no more than 10 types\).

    **Note:** 

    -   We recommend that you choose multiple similar instance types, taking into consideration factors such as vCPU, memory, processor frequency, internal network bandwidth, and packet transmission rate of the internal network.
    -   We recommend that you set an upper limit to the price. If you use automatic bidding, the scaling group will bid for and create preemptible instances at the market price.
    -   The specifications of I/O optimized instances and non-I/O optimized instances vary greatly from each other. Even if you choose these two types of instances at the same time, the scaling success rate cannot be increased significantly.
6.  Configure other parameters as required.
7.  Enable the created scaling group.
8.  [Create a scaling rule](../../../../reseller.en-US/User Guide/Realize Auto Scaling/Create a scaling rule.md#) that adds an ECS instance to the scaling group.

## Cost control result {#section_bk1_rh3_mgb .section}

Assume that in the preceding [procedure](#ol_mtn_rf3_mgb), you have specified VSwitches in Qingdao Zone B and Qingdao Zone C for the scaling group, and specified instance types ecs.sn1.large and ecs.sn1.xlarge for the scaling configuration. As Billing Method was set to Preemptible Instance, each instance type has two prices: the vCPU unit price for preemptible instances and the vCPU unit price for Pay-As-You-Go instances.

**Note:** The prices listed in this topic are only used as examples. Refer to the instance purchase page for actual prices.

After the instance types and billing method are set, you now have four instance creation plans that are sorted by vCPU unit price from low to high. The following table lists the plans.

|No.|Instance type|Billing method|vCPU|Market price|vCPU unit price|
|---|-------------|--------------|----|------------|---------------|
|Plan 1|ecs.sn1.xlarge|Preemptible instance|8|0.158/hour|0.01975/hour|
|Plan 2|ecs.sn1.large|Preemptible instance|4|0.088/hour|0.022/hour|
|Plan 3|ecs.sn1.xlarge|Pay-As-You-Go|8|1.393/hour|0.174125/hour|
|Plan 4|ecs.sn1.large|Pay-As-You-Go|4|0.697/hour|0.17425/hour|

Expected instance creation process: When a scaling activity starts, the scaling group first attempts to create instances based on plan 1. If the group fails to create instances in Zone B and Zone C, it attempts to create instances based on plan 2, plan 3, and plan 4 in sequence until instance creation succeeds.

[Execute a scaling rule](../../../../reseller.en-US/User Guide/Realize Auto Scaling/Execute scaling rules.md#) to trigger the scaling activity of adding one ECS instance to the scaling group. Then, log on to the Auto Scaling console and navigate to he ECS Instances page of the scaling group. Click the ECS instance that has been created to view details. The billing method is **Preemptible Instance** and the instance type is **ecs.sn1.xlarge**, which indicates reduced costs.

