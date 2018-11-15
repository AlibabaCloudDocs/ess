# Move ECS instance to Standby {#concept_ovc_1d2_sfb .concept}

This topic describes how to move ECS instance to Standby.

Auto Scaling allows you to set the Standby status for one or more ECS instances. After an ECS instance is in the Standby status, you can upgrade or maintain the ECS instance. Meanwhile, we do not either perform health check for the specified instance or release it.

## Features {#section_rdh_dd2_sfb .section}

-   If an ECS instance is set to the Standby status:
    -   It is not in service until you resume the ECS instance.
    -   Its lifecycle is controlled by you rather than Auto Scaling service.
    -   The weight of the ECS instance is deregistered to zero if the scaling group has Server Load Balancer instances attached.
    -   You can [stop](../../../../reseller.en-US/User Guide/Instances/Start or stop an instance.md#) instance, [restart](../../../../reseller.en-US/User Guide/Instances/Restart an instance.md#) instance, or do other maintenance operations, such [upgrade the instance configurations](../../../../reseller.en-US/User Guide/Change configurations/Overview of configuration changes.md#), [change the operating system](../../../../reseller.en-US/User Guide/Instances/Change the operating system.md#), [reinitialize the cloud disk](../../../../reseller.en-US/User Guide/Cloud disks/Reinitialize a cloud disk.md#), or [migrate from the classic network to a VPC](../../../../reseller.en-US/Best practices/Migrate from the classic network to VPC/Migration overview.md#).
    -   It is not removed from the scaling group whenever a scaling event happens.
    -   The health status is not updated even the specified instance is stopped or restarted.
    -   It must be removed from the scaling group before you release the instance.
    -   It is resumed for a short while when you delete the related scaling group and then it is release along with the scaling group.
-   If an ECS instance is back to the in service status:
    -   It handles application traffic actively again.
    -   The weight of the ECS instance is set to a predefined value if the scaling group has Server Load Balancer instances attached.
    -   The health status is updated if the specified instance is stopped or restarted.
    -   Its lifecycle is controlled by Auto Scaling service rather than you.

## Move to Standby {#section_dgz_gd2_sfb .section}

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  Select a region, such as China East 2 \(Shanghai\).
3.  Find and click the target scaling group.
4.  In the left-side navigation pane, click **ECS instances**.
5.  Find and click the target ECS instance, click **Move to Standby**.

## Remove from Standby {#section_j3c_ld2_sfb .section}

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  Select a region, such as China East 2 \(Shanghai\).
3.  Find and click the target scaling group.
4.  In the left-side navigation pane, click **ECS instances**.
5.  Find and click the target ECS instance, click **Remove from Standby**.

## API operations {#section_kdz_4d2_sfb .section}

-   Move to Standby: [EnterStandby](../../../../reseller.en-US/API-Reference/Instance/EnterStandby.md#)
-   Remove from Standby: [ExitStandby](../../../../reseller.en-US/API-Reference/Instance/ExitStandby.md#)

## References {#section_kf1_qd2_sfb .section}

-   [What is Server Load Balancer](../../../../reseller.en-US/Product Introduction/What is Server Load Balancer?.md#)
-   [Remove an unhealthy ECS instance](reseller.en-US/User Guide/Usage notes/Remove an unhealthy ECS instance.md#)

