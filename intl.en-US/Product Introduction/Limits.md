# Limits {#concept_s3q_zgm_qfb .concept}

This article introduces the limits for Auto Scaling.

Auto Scaling has the following limits:

-   Applications deployed in the [ECS](../../../../reseller.en-US/Product Introduction/What is ECS?.md#) instances for Auto Scaling must be stateless and scalable.
-   Auto Scaling automatically releases ECS instances, so the application status \(such as sessions\) or data \(such as databases and logs\) must not be saved in the ECS instances. If necessary, you can save this kind of data in independent state servers, databases \(such as [RDS](../../../../reseller.en-US/Product Introduction/What is RDS.md#)\), or centralized log storage \(such as [Log Service](../../../../reseller.en-US/Product Introduction/What is Log Service.md#)\).
-   The instances added by Auto Scaling cannot be automatically added to ApsaraDB for [Memcache](https://partners-intl.aliyun.com/help/faq-detail/26530.htm) whitelist, you must do it manually.
-   Auto Scaling cannot scale the specifications of your instances, such as CPU, RAM, and bandwidth.
-   You can create a limited number of scaling groups, scaling configurations, scaling rules, ECS instances, and scheduled tasks.

