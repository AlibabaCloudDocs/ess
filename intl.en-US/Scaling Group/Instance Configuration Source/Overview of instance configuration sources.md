# Overview of instance configuration sources

This topic provides an overview of instance configuration sources. During a scale-out event, Auto Scaling creates ECS instances based on the instance configuration source and adds the created instances to the scaling group. Instance configuration sources of scaling groups include scaling configurations and launch templates.

## Operations on instance configuration sources

Each scaling group can have only one instance configuration source in effect. For example, after you enable a new scaling configuration, the current launch template or scaling configuration in effect becomes invalid.

The launch template is a feature of ECS. If you want to use a launch template, you must create the template by using the ECS console or calling an API operation. For more information, see [Launch templates](/intl.en-US/Elasticity/Launch template/Launch templates.md).

The following table describes the common operations on instance configuration sources.

|Phase|Scenario|Operation|Reference|
|-----|--------|---------|---------|
|When a scaling group is being created|You want to use an existing ECS instance as a template to create instances.|Select the ECS instance as the instance configuration source. After the scaling group is created, Auto Scaling automatically creates a scaling configuration based on some parameters of the instance, and the scaling group automatically enters the enabled state.**Note:** The image of the scaling configuration is derived from that of the ECS instance. If the image ID that corresponds to the image of the ECS instance does not exist, the ECS instance cannot be used as a template.

|-   [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md)
-   [Create a scaling group based on an existing ECS instance](/intl.en-US/Elasticity/Create a scaling group based on an existing ECS instance.md) |
|You want to use a launch template to create ECS instances.|Select the launch template as the instance configuration source. After the scaling group is created, it automatically enters the enabled state.|[Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md)|
|You do not have an appropriate instance configuration to create ECS instances.|Do not specify the instance configuration source. After the scaling group is created, it enters the stopped state.|[Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md)|
|After a scaling group is created|You do not specify the instance configuration source.|Manually create a scaling configuration or select a launch template, and then enable the scaling group.|-   [Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md)
-   [Modify a scaling group](/intl.en-US/Scaling Group/Scaling group/Modify a scaling group.md)
-   [Enable a scaling group](/intl.en-US/Scaling Group/Scaling group/Enable a scaling group.md) |
|You want to use other scaling configurations.|Create and enable a scaling configuration, or select an existing scaling configuration.|-   [Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md)
-   [Apply a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Apply a scaling configuration.md) |
|You want to use other launch templates or template versions.|Select another launch template or template version to modify the scaling group.|[Modify a scaling group](/intl.en-US/Scaling Group/Scaling group/Modify a scaling group.md)|

## Comparison between scaling configurations and launch templates

|Comparison item|Scaling configuration|Launch template|
|---------------|---------------------|---------------|
|Parameter verification|Scaling configurations support parameter verification. You cannot create a scaling configuration if the required parameters such as image parameters are missing. Therefore, when you create ECS instances based on a scaling configuration, the instances will not fail to be created due to missing parameters.|Launch templates do not support parameter verification. All parameters are optional. When you create ECS instances based on a launch template in which the required parameters such as image parameters are missing, the ECS instances fail to be created.|
|Configuration method|You can select an existing ECS instance to be used to automatically create a scaling configuration when you create a scaling group, or manually create a scaling configuration after you create a scaling group.|Create a launch template by using the ECS console or by calling an API operation, and then use this template as the instance configuration source to create a scaling group.|
|Modification|You can create multiple scaling configurations based on different needs. You can modify scaling configurations. All modifications are irreversible.If you need to frequently publish applications, we recommend that you create an image update task to replace images in multiple scaling configurations. For more information, see [Replace images in multiple scaling configurations at a time](/intl.en-US/Scaling Group/Instance Configuration Source/Replace images in multiple scaling configurations at a time.md).

**Note:** Only a limited number of scaling configurations can be created for a scaling group. For more information, see [Limits](/intl.en-US/Product Introduction/Limits.md).

|You cannot modify launch templates, but you can create and use new template versions.|
|Multiple instance types|You can select multiple instance types. If you focus on instance specifications, we recommend that you use scaling configurations. This increases the success rate of creating ECS instances. **Note:** Only a limited number of instance types can be selected for a scaling configuration. For more information, see [Limits](/intl.en-US/Product Introduction/Limits.md).

|You cannot select multiple instance types.|

A scaling configuration can support multiple instance types. A scaling group in a VPC can support multiple zones. This can reduce the risk of insufficient resources and increase the success rate of creating ECS instances. For more information, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md).

## Comparison between parameter settings

You can use an existing instance or launch template as the instance configuration source to create a scaling group. Alternatively, you can manually create a scaling configuration as the instance configuration source after the scaling group is created. The following table describes the parameter settings of three methods that can be used to configure an instance configuration source for a scaling group.

|Manually create a scaling configuration|Use an existing ECS instance|Use a launch template|
|---------------------------------------|----------------------------|---------------------|
|You can specify the following parameters to manually create a scaling configuration. For more information about the parameters, see [CreateScalingConfiguration](/intl.en-US/API Reference/Scaling configuration/CreateScalingConfiguration.md). -   ImageId
-   ImageName
-   InstanceType
-   Cpu
-   Memory
-   DeploymentSetId
-   InstanceTypes.N
-   SecurityGroupId
-   IoOptimized
-   InternetChargeType
-   InternetMaxBandwidthIn
-   InternetMaxBandwidthOut
-   SystemDisk.Category
-   SystemDisk.Size
-   SystemDisk.DiskName
-   SystemDisk.Description
-   SystemDisk.AutoSnapshotPolicyId
-   ScalingConfigurationName
-   DataDisk.N.Size
-   DataDisk.N.SnapshotId
-   DataDisk.N.Category
-   DataDisk.N.Device
-   DataDisk.N.DeleteWithInstance
-   DataDisk.N.Encrypted
-   DataDisk.N.KMSKeyId
-   DataDisk.N.DiskName
-   DataDisk.N.Description
-   DataDisk.N.AutoSnapshotPolicyId
-   LoadBalancerWeight
-   Tags
-   UserData
-   KeyPairName
-   RamRoleName
-   SecurityEnhancementStrategy
-   InstanceName
-   HostName
-   SpotStrategy
-   PasswordInherit
-   SpotPriceLimit.N.InstanceType
-   SpotPriceLimit.N.PriceLimit
-   Password
-   ResourceGroupId
-   SecurityGroupIds.N
-   HpcClusterId
-   InstanceDescription
-   ClientToken
-   Ipv6AddressCount

|Auto Scaling automatically creates a scaling configuration based on the parameters of an existing ECS instance. **Note:** For more information about all parameters supported by an ECS instance, see [RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md).

-   ImageId
-   InstanceType
-   SecurityGroupIds
-   IoOptimized
-   InternetChargeType
-   InternetMaxBandwidthIn
-   InternetMaxBandwidthOut
-   KeyPairName
-   SpotStrategy
-   SpotPriceLimit
-   ResourceGroupId
-   HpcClusterId
-   DeploymentSetId
-   SystemDisk.Category
-   SystemDisk.Size
-   SystemDisk.Description
-   DataDisk.Category
-   DataDisk.Size
-   DataDisk.Device
-   DataDisk.DeleteWithInstance
-   DataDisk.Encrypted
-   DataDisk.KMSKeyId
-   DataDisk.DiskName
-   DataDisk.Description
-   DataDisk.SourceSnapshotId
-   UserData
-   RamRoleName
-   ResourceGroupId

|You can create a scaling group based on the parameters of a launch template. **Note:** For more information about all parameters supported by a launch template, see [CreateLaunchTemplateVersion](/intl.en-US/API Reference/Launch templates/CreateLaunchTemplateVersion.md).

-   ImageId
-   InstanceType
-   SecurityGroupId
-   IoOptimized
-   InstanceName
-   InternetMaxBandwidthIn
-   InternetMaxBandwidthOut
-   HostName
-   PasswordInherit
-   InternetChargeType
-   SystemDisk.Size
-   SystemDisk.Category
-   SystemDisk.DiskName
-   SystemDisk.Description
-   DataDisk.N.Size
-   DataDisk.N.SnapshotId
-   DataDisk.N.Category
-   DataDisk.N.Encrypted
-   DataDisk.N.DiskName
-   DataDisk.N.Description
-   DataDisk.N.Device
-   DataDisk.N.DeleteWithInstance
-   UserData
-   KeyPairName
-   RamRoleName
-   SpotStrategy
-   SpotPriceLimit
-   SecurityEnhancementStrategy
-   Tag.N.Key
-   Tag.N.Value
-   ResourceGroupId |

