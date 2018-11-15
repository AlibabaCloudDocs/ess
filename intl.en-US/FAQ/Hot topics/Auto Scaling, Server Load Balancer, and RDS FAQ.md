# Auto Scaling, Server Load Balancer, and RDS FAQ {#concept_25970_zh .concept}

-   [After Auto Scaling creates an ECS instance, will the new instance be automatically added to a Sever Load Balancer instance?](#)
-   [When a scaling group is added in Auto Scaling, can I bind multiple Sever Load Balancer instances to the group?](#)
-   [When Auto Scaling creates an ECS instance, can the instance be added to multiple Server Load Balancer instances?](#)
-   [Can I modify the weights of ECS instances added to an Auto Scaling group Server Load Balancer Instance?](#)
-   [I have a public network Server Load Balancer instance. If I create a scaling configuration, will its ECS instances need public bandwidth?](#)
-   [Do I need to use Server Load Balancer, CloudMonitor, and RDS in combination with Auto Scaling?](#)

## After Auto Scaling creates an ECS instance, will the new instance be automatically added to a Sever Load Balancer instance? {#section_dsy_kps_sfb .section}

If a [Server Load Balancer](../../../../reseller.en-US/Product Introduction/What is Server Load Balancer?.md#) instance is specified in a scaling group, the scaling group will automatically add the ECS instances in the group to the specified Server Load Balancer instance.

## When a scaling group is added in Auto Scaling, can I bind multiple Sever Load Balancer instances to the group? {#section_odj_qys_sfb .section}

By default, you can only bind five Server Load Balancer instances to each scaling group. To bind more Server Load Balancer instances, open a ticket to apply for a higher quota to Alibaba Cloud Technical Support.

## When Auto Scaling creates an ECS instance, can the instance be added to multiple Server Load Balancer instances? {#section_qdj_qys_sfb .section}

Yes. You can bind five Server Load Balancer instances to each ECS instance.

## Can I modify the weights of ECS instances added to an Auto Scaling group Server Load Balancer Instance? {#section_rdj_qys_sfb .section}

Yes. You can modify the weights in the [Server Load Balancer console](https://partners-intl.console.aliyun.com/#/slb). The Server Load Balancer also distributes traffic based on the weight ratio, not the actual number. This means that, if you have two backend ECS instances weighted 50 and 50 \(with a ratio of 1:1\), this is the same as if they were weighted 100 and 100. This is suitable for most scenarios, as backend ECS instances of Auto Scaling groups normally carry the same services and are the same type. By default, ECS instances under Auto Scaling Sever Load Balancer instances have a weight of 50.

## I have a public network Server Load Balancer instance. If I create a scaling configuration, will its ECS instances need public bandwidth? {#section_sdj_qys_sfb .section}

When a scaling configuration is created, you do not have to allocate public bandwidth to its ECS instances. However, we recommend that you set at least 1 Mbit/s of ECS bandwidth when [creating a scaling configuration](../../../../reseller.en-US/User Guide/Scaling configurations/Create a scaling configuration.md#), for easier ECS instance management.

## Do I need to use Server Load Balancer, CloudMonitor, and RDS in combination with Auto Scaling? {#section_tdj_qys_sfb .section}

No. Auto Scaling is an open elastic scaling platform, and can independently scale up or down ECS instances. It can be deployed either separately or in combination with the [Server Load Balancer](../../../../reseller.en-US/Product Introduction/What is Server Load Balancer?.md#) and [ApsaraDB for RDS](../../../../reseller.en-US/Product Introduction/What is RDS.md#).

Auto Scaling allows the [CloudMonitor](../../../../reseller.en-US/Product Introduction/Overview.md#) to trigger scaling up or scaling down actions for ECS instances.

