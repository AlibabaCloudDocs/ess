# Billing

Auto Scaling is free of charge. However, you must pay for the resources of other Alibaba Cloud services used in Auto Scaling, such as Elastic Compute Service \(ECS\), Server Load Balancer \(SLB\), and ApsaraDB RDS \(RDS\) instances.

## ECS instances

Auto Scaling manages ECS instances. You are charged for instance-related resources such as instance types, Elastic Block Storage devices, and public bandwidth.

|Service|Description|Reference|
|-------|-----------|---------|
|ECS|ECS instances in scaling groups are categorized into the following types: -   ECS instances that are manually added to scaling groups
-   ECS instances that are automatically created by Auto Scaling during scale-out events

**Note:** Only pay-as-you-go and preemptible instances can be automatically created.


|-   [Billing overview](/intl.en-US/Pricing/Billing overview.md)
-   [Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md)
-   [Overview](/intl.en-US/Instance/Instance purchasing options/Preemptible instances/Overview.md)
-   [No Fees for Stopped Instances \(VPC-Connected\)](/intl.en-US/Pricing/Billing methods/No Fees for Stopped Instances (VPC-Connected).md)
-   [ECS instance lifecycle](/intl.en-US/Instance Management/ECS instance/ECS instance lifecycle.md)

**Note:** By default, Auto Scaling considers stopped ECS instances to be unhealthy, removes these instances from a scaling group, and may release them. If you want to retain some ECS instances, you must put these instances into the Protected state. For more information, see [Put an ECS instance into the Protected state](/intl.en-US/Instance Management/ECS instance/Put an ECS instance into the Protected state.md). |

## Other Alibaba Cloud services

Auto Scaling does not create resources listed in the following table. Auto Scaling must associate scaling groups with these resources during the usage. You must create and pay for these resources in advance by using the consoles of other Alibaba Cloud services or by calling API operations of other Alibaba Cloud services.

|Service|Description|Reference|
|-------|-----------|---------|
|SLB|If you want to associate a scaling group with SLB instances, you must create and pay for the SLB instances in advance.|[Pay-as-you-go](/intl.en-US/Classic Load Balancer/CLB Pricing/Pay-as-you-go.md)|
|RDS|If you want to associate a scaling group with RDS instances, you must create and pay for the RDS instances in advance.|[Pricing, billable items, and billing methods](/intl.en-US/Purchase Guide/Pricing, billable items, and billing methods.md)|

