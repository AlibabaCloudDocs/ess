# Limits

This topic describes the feature and quantity limits of Auto Scaling.

## Feature limits

Auto Scaling has the following feature limits:

-   Auto Scaling can automatically scale the number of ECS instances in a scaling group, but cannot automatically upgrade or downgrade configurations of ECS instances, such as vCPUs, memory, and bandwidth.
-   Applications deployed on ECS instances in a scaling group must be stateless and horizontally scalable.
-   ECS instances in a scaling group can be automatically released. We recommend that you do not store information such as sessions, application data, or logs on ECS instances in a scaling group. If applications deployed on these ECS instances require data to be stored, store status information such as sessions on ECS instances that are not in a scaling group, store application data in ApsaraDB for RDS, and store logs in Log Service. For more information, see [What is ApsaraDB for RDS?](/intl.en-US/Product Introduction/What is ApsaraDB for RDS?.md) and [What is Log Service?](/intl.en-US/Product Introduction/What is Log Service?.md)
-   Auto Scaling cannot automatically add ECS instances to the whitelist of an ApsaraDB for Memcache instance. You must manually add these ECS instances to the whitelist. For more information, see[Set IP firewall](https://www.alibabacloud.com/help/doc-detail/48234.htm).

## Quantity limits

The following table describes the quantity limits of Auto Scaling.

|Item|Limit|Adjustable|
|----|-----|----------|
|Scaling groups per region in an account|100|Auto Scaling automatically increases the quota based on your usage. A maximum of 440 scaling groups can be created per region in an account.|
|ECS instances in a scaling group|2,000|N/A|
|ECS instances that can be added to a scaling group or deleted during a scale-out event|500|N/A|
|Scaling configurations in a scaling group|20|Auto Scaling automatically increases the quota based on your usage. A maximum of 140 scaling configurations can be created for a scaling group.|
|Scaling rules in a scaling group|20|Auto Scaling automatically increases the quota based on your usage. A maximum of 140 scaling rules can be created for a scaling group.|
|Event notifications in a scaling group|6|N/A|
|Lifecycle hooks in a scaling group|6|N/A|
|SLB instances associated with a scaling group|5|Auto Scaling automatically increases the quota based on your usage. A maximum of 20 SLB instances can be associated with a scaling group.|
|VServer groups specified when you associate a scaling group with SLB instances|5|N/A|
|ApsaraDB for RDS instances associated with a scaling group|5|Auto Scaling automatically increases the quota based on your usage. A maximum of 20 ApsaraDB for RDS instances can be associated with a scaling group.|
|Scheduled tasks per region in an account|60|Auto Scaling automatically increases the quota based on your usage. A maximum of 140 scheduled tasks can be created per region in an account.|
|Instance types in a scaling configuration|10|N/A|

