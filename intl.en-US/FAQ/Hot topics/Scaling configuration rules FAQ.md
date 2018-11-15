# Scaling configuration rules FAQ {#concept_25969_zh .concept}

-   [What information should I provide for Auto Scaling troubleshooting?](#)
-   [Can I add different ECS instance types in an Auto Scaling groups?](#)
-   [How many ECS instances can be added to a scaling group at most? Can I increase the maximum number of instances in the Auto Scaling service?](#)
-   [Can I add ECS instances that I have already created to a scaling group?](#)
-   [Can I create 8vCPU and 16vCPU ECS instances in a scaling group?](#)
-   [Is Auto Scaling vertical scalable?](#)
-   [Can I create periodic tasks in Auto Scaling?](#)
-   [Can I add existing subscription instances to scaling groups?](#)
-   [Can I add an ECS instance to more than one scaling group?](#)
-   [When I remove an ECS instance from a scaling group and release the instance, can I save the ECS instance data?](#)
-   [If I disable a scaling group, are instances created by Auto Scaling released?](#)
-   [Does Auto Scaling automatically include or exclude a new or removed ECS instances into or from the IP address whitelists of the configured RDS or Memcache?](#)
-   [How can I make sure that ECS instances are not removed from the scaling group?](#)

## What information should I provide for Auto Scaling troubleshooting? {#section_xtp_hrs_sfb .section}

When you open a ticket, we recommend that you provide your Auto Scaling activity ID \(`ScalingActivityId`\) and relevant logs to facilitate troubleshooting.

## Can I add different ECS instance types in an Auto Scaling groups? {#section_zl4_lzs_sfb .section}

No, you cannot. However, each scaling group can be set with a different configuration type.

## How many ECS instances can be added to a scaling group at most? Can I increase the maximum number of instances in the Auto Scaling service? {#section_am4_lzs_sfb .section}

Yes, you can. The default maximum number of ECS instance in a scaling group is 1,000. Open a ticket for a higher instance quota.

## Can I add ECS instances that I have already created to a scaling group? {#section_cm4_lzs_sfb .section}

Yes. However, the ECS instances:

-   Must be in the same region as the scaling group. For more information, see [regions and zones](../../../../reseller.en-US/General Reference/Regions and zones.md#).
-   Must be in the **Running** status. For more information, see [ECS instance life cycle](../../../../reseller.en-US/Product Introduction/Instances/ECS instance life cycle.md#).
-   Cannot exist in more than one scaling group.

## Can I add existing subscription instances to scaling groups? {#section_em4_lzs_sfb .section}

Yes, you can. Auto Scaling automatically creates Pay-As-You-Go or spot instances by default, and you can also add your existing Subscription or Pay-As-You-Go instances to a scaling group.

## Can I add an ECS instance to more than one scaling group? {#section_fm4_lzs_sfb .section}

No, you cannot. This feature is not currently supported.

## Can I create 8vCPU and 16vCPU ECS instances in a scaling group? {#section_gm4_lzs_sfb .section}

Yes, you can. Open a ticket to use more ECS instance types when you [create ECS instances](../../../../reseller.en-US/User Guide/Instances/Create an instance/Create an instance of the same configuration.md#).

## Is Auto Scaling vertical scalable? {#section_im4_lzs_sfb .section}

No, it is not. Auto Scaling does not support automatically upgrade or downgrade the vCPU, memory, or bandwidth of an ECS instance.

## Can I create periodic tasks in Auto Scaling? {#section_jm4_lzs_sfb .section}

Yes, you can. For more information, see [create a scheduled task](../../../../reseller.en-US/User Guide/Scheduled tasks/Create a scheduled task.md#).

## When I remove an ECS instance from a scaling group and release the instance, can I save the ECS instance data? {#section_km4_lzs_sfb .section}

No, you cannot. Therefore, do not establish application status information \(for example, session\) or related data \(such as databases and logs\) in an Auto Scaling ECS instances. We recommend that you save the status information to an independent state server \(for example, ECS\), database \(for example, RDS\), or standardized log storage \(for example, Log Service\).

## If I disable a scaling group, are instances created by Auto Scaling released? {#section_lm4_lzs_sfb .section}

No. After you disable a scaling group \([DisableScalingGroup](../../../../reseller.en-US/API-Reference/Scaling group/Disable a scaling group.md#)\), instances created by Auto Scaling are not automatically released.

## Does Auto Scaling automatically include or exclude a new or removed ECS instances into or from the IP address whitelists of the configured RDS or Memcache? {#section_mm4_lzs_sfb .section}

Auto Scaling automatically includes a new or removed ECS instances into or from the IP address whitelists of a RDS. However, Memcache whitelists are not supported.

## How can I make sure that manually added ECS instances are not removed from the scaling group? {#section_nm4_lzs_sfb .section}

-   For automatically created ECS instances, supposing that you want to retain the specified 100 ECS instances in a scaling group, and pay attention to the following when you [create a scaling configuration](../../../../reseller.en-US/User Guide/Scaling configurations/Create a scaling configuration.md#)\([CreateScalingConfiguration](../../../../reseller.en-US/API-Reference/Scaling configuration/CreateScalingConfiguration.md#)\):

    -   Set the minimum number of instances to greater than 100.

    -   Set the first Removal Policy to The instances with the oldest configuration.

-   For manually created ECS instances, do not [stop the specified ECS instance](../../../../reseller.en-US/User Guide/Instances/Start or stop an instance.md#). Because the manually created and added ECS instances are not released if they are removed from a scaling group.


**Note:** Since manually added ECS instances were not created by a scaling group, Auto Scaling removes the automatically created ECS instances from the scaling group. Manually added ECS instances are removed only after all the automatically created ECS instances have been removed.

