# Limits

This topic describes the feature and quantity limits of Auto Scaling.

## Feature limits

Auto Scaling has the following feature limits:

-   Auto Scaling can automatically scale the number of ECS instances in a scaling group, but cannot automatically upgrade or downgrade configurations of ECS instances, such as vCPUs, memory, and bandwidth.
-   Applications deployed on ECS instances in a scaling group must be stateless and horizontally scalable.
-   ECS instances in a scaling group can be automatically released. We recommend that you do not store information such as sessions, application data, or logs on ECS instances in a scaling group. If applications deployed on these ECS instances require data to be stored, store status information such as sessions on ECS instances that are not in a scaling group, store application data in ApsaraDB for RDS, and store logs in Log Service. For more information, see [What is ApsaraDB for RDS?](/intl.en-US/Product Introduction/What is ApsaraDB for RDS?.md) and [What is Log Service?](/intl.en-US/Product Introduction/What is Log Service?.md)
-   Auto Scaling cannot automatically add ECS instances to the whitelist of an ApsaraDB for Memcache instance. You must manually add these ECS instances to the whitelist. For more information, see[Set IP firewall](https://www.alibabacloud.com/help/doc-detail/48234.htm).

## Quantity limits

The following table describes the quantity limits that apply to Auto Scaling in a single account.

|Item|Limit|
|----|-----|
|Total number of scaling groups in a region|The quota is based on the resource usage of Auto Scaling. Go to the [Quotas](https://quotas.console.aliyun.com/products/ess/quotas) page to view the quota.**Note:** You can submit a ticket to apply for increasing the quota. |
|Total number of scaling configurations in a scaling group|
|Total number of scaling rules in a scaling group|
|Total number of ApsaraDB for RDS instances that can be associated with a scaling group|
|Total number of SLB instances that can be associated with a scaling group|
|Total number of VServer groups that can be associated with a scaling group|
|Maximum number of ECS instances that can be configured for a scaling group|
|Total number of scheduled tasks in a region|
|Total number of ECS instances that can be added to or deleted from a scaling group during a scaling activity|500|
|Total number of instance types in a scaling configuration|10|
|Total number of event notifications in a scaling group|6|
|Total number of lifecycle hooks in a scaling group|6|

