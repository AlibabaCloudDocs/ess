# ECS instance templates {#concept_87761_zh .concept}

Auto Scaling can automatically create ECS instances based on preconfigured templates and add them to scaling groups as the needs of your business grow. Currently, ECS instance templates include the following two types: custom scaling configurations and launch templates.

## Custom scaling configurations {#section_pkk_q14_1gb .section}

Scaling configurations allow you to create ECS instance launch templates for scaling groups. When creating a scaling configuration, you can set ECS instance parameters, such as instance types, image types, storage size, and the SSH key pairs that are used to log on to the ECS instances. You can also modify an existing scaling configuration to meet your business needs.

**Note:** A scaling configuration requires a scaling group. You need to create at least one scaling group before creating a scaling configuration. There is a limit to the number of scaling configurations that you can create in a scaling group. For more information, see [Quantity restrictions](reseller.en-US/User Guide/Usage notes/Quantity restrictions.md#).

Currently, you can perform the following operations on a scaling configuration:

-    [Create a scaling configuration](reseller.en-US/User Guide/Scaling configurations/Create a scaling configuration.md#) 
-    [View a scaling configuration](reseller.en-US/User Guide/Scaling configurations/View a scaling configuration.md#) 
-    [修改伸缩配置](reseller.en-US/User Guide/Scaling configurations/修改伸缩配置.md#) 
-    [Delete scaling configuration](reseller.en-US/User Guide/Scaling configurations/Delete scaling configuration.md#)
-    [导出伸缩配置](reseller.en-US/User Guide/Scaling configurations/导出伸缩配置.md#)
-   [导入伸缩配置](reseller.en-US/User Guide/Scaling configurations/导入伸缩配置.md#)

## Launch templates {#section_ucn_s14_1gb .section}

Launch templates are a tested feature of ECS. You can use existing launch templates to configure scaling groups. For more information, see [Launch templates](../../../../../reseller.en-US/Product Introduction/Instances/Launch templates.md#).

**Note:** Launch templates allow you to immediately enable a scaling group after it is created.

## Differences between custom scaling configurations and launch templates {#section_eqc_324_1gb .section}

|Item|Custom scaling configuration|Launch template|
|----|----------------------------|---------------|
|Parameters supported by scaling groups|All parameters of custom scaling configurations.|Certain parameters of launch templates are not supported. Instances created by launch templates may have missing configurations.|
|Parameter verification|Supported. You cannot create a custom scaling configuration when required parameters such as image type are missing. In this case, ECS instance creation failures will not occur.|Launch templates do not verify the parameters. All parameters are optional. Therefore, instance may fail to be created if required parameters such as image type are not specified.|
|Configuration procedure|You must first create a scaling group.|You do not need to create a scaling group.|
|Creation method|Can only be created in a scaling group.|Can be created on the buy page of ECS, the Launch Templates page, and the Instance Settings page.|
|Modification|You must manually modify scaling configurations. All modifications are irreversible. However, you can create multiple scaling configurations based on different needs.|Cannot be modified. You can create templates based on your needs.|
|Multiple instance types|Supported. Applied in scenarios where performance rather than a specified instance type is required, with a bigger chance of successfully scaling out.|Unsupported.|

For more information, see [Use custom scaling configurations to create scaling groups](reseller.en-US/User Guide/Scaling groups/Use custom scaling configurations to create scaling groups.md#) and [Use launch templates to create scaling groups](reseller.en-US/User Guide/Scaling groups/Use launch templates to create scaling groups.md#).

