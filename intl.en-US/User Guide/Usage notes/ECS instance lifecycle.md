# ECS instance lifecycle {#concept_kbm_xym_qfb .concept}

This topic introduces the life cycle management of ECS instances.

There are two types of ECS instances that are added to scaling groups: automatically created and manually added instances.

## Automatically created ECS instances {#section_ibt_1zm_qfb .section}

Automatically created ECS instances are automatically created according to scaling configuration and rules.

Auto Scaling manages the lifecycle of this ECS instance type. It creates ECS instances during scale-up and stops and releases them during scale-down.

## Manually added ECS instances {#section_oks_pzm_qfb .section}

Manually added ECS instances are manually attached to a scaling group.

Auto Scaling does not manage the lifecycle of this ECS instance type. When this ECS instance is removed from a scaling group, either manually or as the result of a scaling-down activity, Auto Scaling does not stop or release the instance.

## Instance status {#section_h25_qzm_qfb .section}

During its lifecycle, an ECS instance is in one of the following states: Pending:

-   The ECS instance is being added to a scaling group. For example, Auto Scaling creates the ECS instance and adds it to the Server Load Balancer instance, or to the RDS access whitelist.
-   InService: The ECS instance has been added to a scaling group and is functioning correctly.
-   Removing: The ECS instance is being removed from a scaling group.

## Instance health status {#section_wnf_wzm_qfb .section}

An ECS instance may be in the following health conditions:

-   Healthy
-   Unhealthy

ECS instances are regarded as unhealthy when they are not **Running**\(`Running`\). Auto Scaling automatically removes unhealthy ECS instances from scaling groups.

-   Auto Scaling only stops and releases automatically created unhealthy instances.
-   It does not stop and release manually added ones.

