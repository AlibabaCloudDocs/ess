# Create a scaling group and a scaling configuration

You must first create a scaling group and a scaling configuration to implement automatic scaling. A scaling group is a group of ECS instances that provide the same service. A scaling configuration is a template used by a scaling group to create ECS instances. This topic describes how to create a scaling group, create a scaling configuration for the scaling group, and enable the scaling group. The minimum number of ECS instances in the scaling group is set to one.

The following operations are performed:

-   [Grant permissions to Auto Scaling]()
-   [Create a security group](/intl.en-US/Security/Security groups/Create a security group.md)

    **Note:** The security group and the scaling group must be located in the same region.


After a scaling group is created, its region cannot be changed. For more information, see [Regions and zones](https://www.alibabacloud.com/help/doc-detail/40654.htm).

## Step 1: Create a scaling group

In this example, a scaling group is created with simple settings. For more information about the parameters, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md).

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the top navigation bar, select a region.

3.  In the left-side navigation pane, click **Scaling Groups**.

4.  In the upper-left corner of the Scaling Groups page, click **Create**.

5.  Configure parameters for the scaling group and then click **OK**.

    The following table describes the parameters used in this example. For parameters that are not described in the following table, use the default values.

    |Configuration type|Parameter|Example|Description|
    |------------------|---------|-------|-----------|
    |**Instance Template Source**|**Source Type**|Create from Scratch|If you create a scaling group from scratch, the scaling group will not have scaling configurations after the scaling group is created. You must create a scaling configuration for the scaling group.|
    |**Scaling Group Basic Information**|**Scaling Group Name**|MyFirstScalingGroup|None|
    |**Maximum Number of Instances**|3|A maximum of three ECS instances can be created for the scaling group. Excess ECS instances will be automatically removed from the scaling group.|
    |**Minimum Number of Instances**|1|The scaling group must contain at least one ECS instance. If the number of ECS instances in the scaling group is zero, an instance is automatically created for the scaling group.|
    |**Tag**|ESS:Documentation|Tags are used to categorize the scaling group for easy management.|
    |**Scaling Configuration**|**Network Type**|Classic Network|When you create a scaling configuration for the scaling group, you can select only instance types that support the classic network.|

6.  In the **Create Scaling Group Status Wizard** message, click **View Scaling Groups**.


## Step 2: Create a scaling configuration and enable the scaling group

In this example, a scaling configuration is created with simple settings. For more information about the parameters, see [Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md).

1.  In the upper part of the page, click the **Configuration Source** tab.

2.  In the upper-left corner of the page, click the **Scaling Configurations** tab.

3.  Click **Create Scaling Configuration**.

4.  Enter a name for the scaling configuration and click **Create**.

    The following table describes the parameters used in this example. For parameters that are not described in the following table, use the default values.

    |Configuration type|Parameter|Examples|Description|
    |------------------|---------|--------|-----------|
    |**Basic Configurations**|**Billing Method**|Pay-As-You-Go|Auto Scaling is free of charge. However, you must pay for the ECS instances added to the scaling group based on the pricing of ECS. For more information, see [Billing overview](/intl.en-US/Pricing/Billing overview.md).|
    |**Instance Type**|Shared balanced type: ecs.mn4.small|Scaling groups in a VPC support more newly released instance types. For more information about how to create a scaling group in a VPC, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md).|
    |**Image**|Public image: CentOS 7.6 64-bit|After the instance is started, the operating system and application data of the image are copied to the system disk.|
    |**Public IP Address**|Pay-by-traffic. A peak bandwidth of 1 Mbit/s|You are charged for the outbound public traffic based on the traffic volume. The peak bandwidth is 1 Mbit/s.|
    |**Security Group**|sg-bp18kz60mefsicfg\*\*\*\*|Select the security group that you created in advance.|
    |**System Configurations \(Optional\)**|**Logon Credentials**|Set Later|You can manually set the password for ECS instances after the ECS instances are created.|
    |**Create**|**Scaling Configuration Name**|MyFirstScalingConfiguration|None|

5.  In the **Created** dialog box, click **Enable Configuration**.

6.  In the **Enable Scaling Configuration** message, click **OK**.

7.  In the **Enable Scaling Group** message, click **OK**.


The minimum number of ECS instances in the scaling group is one. Therefore, Auto Scaling automatically creates an ECS instance for the scaling group after the scaling group is enabled. You can view the ECS instance in the ECS instance list. The automatically created ECS instance applies configurations specified in the scaling configuration. For more information, see [View ECS instances](/intl.en-US/Instance Management/ECS instance/View ECS instances.md).

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6940317951/p61234.png)

After the scaling group is enabled, you can create scaling rules for the scaling group and create scheduled tasks and event-triggered tasks to automatically scale ECS instances in the scaling group. For more information, see the following topics:

-   [Automatically add ECS instances](/intl.en-US/Quick Start/Automatically add ECS instances.md)
-   [Automatically remove ECS instances](/intl.en-US/Quick Start/Automatically remove ECS instances.md)

