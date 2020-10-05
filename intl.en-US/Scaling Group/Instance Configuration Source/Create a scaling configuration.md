---
keyword: [instance configuration source, scaling configuration, ECS instance]
---

# Create a scaling configuration

This topic describes how to create a scaling configuration for a scaling group. Auto Scaling automatically scales out Elastic Compute Service \(ECS\) instances based on the specified scaling configuration.

A security group is created. If you create a scaling configuration for a VPC-type scaling group, make sure that the security group and the scaling group are in the same VPC. If no security group exists in the VPC where the scaling group is located, you must create a security group. For more information, see [Create a security group](/intl.en-US/Security/Security groups/Create a security group.md).

The process of creating a scaling configuration is similar to that of creating an ECS instance. However, ECS instances are not automatically created after you create a scaling configuration. Scale-out events must be triggered and then Auto Scaling uses the scaling configuration as a template to automatically create ECS instances. For example, scale-out events can be triggered by using scheduled or event-triggered tasks.

## Procedure

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the top navigation bar, select a region.

3.  Find the target scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   Click **Manage** in the **Actions** column.
4.  In the left-side navigation pane, click **Instance Configuration Source**.

5.  In the upper-left corner of the page, click the **Scaling Configurations** tab.

6.  Click **Create Scaling Configuration**.

7.  In the Basic Configurations step, configure the parameters and click **Next: System Configurations**.

    The following table describes the parameters.

    |Parameter|Description|Reference|
    |---------|-----------|---------|
    |**Billing Method**|The following billing methods are supported in a scaling configuration:    -   **Pay-As-You-Go**: provisions and releases resources on demand. You pay for the resources that you used, and do not need to purchase a large number of resources in advance.
    -   **Preemptible Instance**: The market price of a preemptible instance fluctuates based on changes to the supply and demand of its instance type. Compared with pay-as-you-go instances, preemptible instances offer discounts but may be automatically reclaimed. You can use preemptible instances to reduce costs.
|    -   [Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md)
    -   [Overview](/intl.en-US/Instance/Instance purchasing options/Preemptible instances/Overview.md) |
    |**Instance Type**|Different instance types can meet the requirements of different scenarios. You can select multiple instance types in a scaling configuration. If resources of an instance type are insufficient, Auto Scaling automatically uses another instance type to create ECS instances. This increases the success rate of creating instances.If you select a burstable instance type, you can set the default performance mode. For more information about burstable instances, see [Overview](/intl.en-US/Instance/Instance type families/Burstable performance instances/Overview.md).

|[Instance families](/intl.en-US/Instance/Instance families.md)|
    |**Image**|An image provides the data required to create ECS instances, such as the system and application environments, and related software configurations.|[Image overview](/intl.en-US/Images/Image overview.md)|
    |**Storage**|Select a system disk or one or more data disks for ECS instances to store data.|[Block Storage overview](/intl.en-US/Block Storage/Block Storage overview/Block Storage overview.md)|
    |**Public IP Address**|Assign IPv4 addresses to ECS instances for access to the Internet. If you select Assign Public IP Address, you must configure the billing method for network usage.|    -   [IP addresses of ECS instances within VPCs](/intl.en-US/Network/Instance IP addresses/IP addresses of ECS instances within VPCs.md)
    -   [IP addresses of a classic network-connected ECS instance](/intl.en-US/Network/Instance IP addresses/IP addresses of a classic network-connected ECS instance.md)
    -   [Billing methods of public bandwidth](/intl.en-US/Pricing/Billing items/Billing methods of public bandwidth.md) |
    |**Security Group**|A security group is a virtual firewall that controls network access of ECS instances.|    -   [Overview](/intl.en-US/Security/Security groups/Overview.md)
    -   [Create a security group](/intl.en-US/Security/Security groups/Create a security group.md) |

8.  In the System Configurations \(Optional\) step, configure the parameters and click **Next: Preview**.

    The following table describes the parameters.

    |Parameter|Description|Reference|
    |---------|-----------|---------|
    |Tags|Tags are used to identify resources. You can use tags to classify ECS instances and related resources for easy management and search.|    -   [Overview](/intl.en-US/Tag & Resource/Tags/Overview.md)
    -   [Create or bind a tag](/intl.en-US/Tag & Resource/Tags/Create or bind a tag.md) |
    |Resource Group|Resource groups are used to categorize your resources based on usage, permissions, and regions. This way, you can manage the resources in a hierarchical manner based on users and projects.|[Resource groups](/intl.en-US/Tag & Resource/Resource/Resource groups.md)|
    |Logon Credentials|The supported logon credentials are subject to the operating system type.    -   Linux: You can select an SSH key pair when you create a scaling configuration, or configure logon credentials after ECS instances are created.
    -   Windows: You can configure logon credentials only after ECS instances are created.
|    -   [Overview](/intl.en-US/Security/Key pairs/Overview.md)
    -   [Reset the logon password of an instance](/intl.en-US/Instance/Manage instances/Reset the logon password of an instance.md) |
    |Instance Name|Specifies the name for ECS instances that are created based on the current scaling configuration. If you do not specify this parameter, a default name is used.|None|
    |RAM Role|Instance RAM roles allow you to attach a role to ECS instances. You can use temporary tokens issued by Security Token Service \(STS\) to call API operations of other Alibaba Cloud services. This ensures the security of your AccessKey pair and helps you implement fine-grained permission control and management by using RAM.**Note:** You can select instance RAM roles only for scaling configurations in the VPC-type scaling group.

|    -   [Overview](/intl.en-US/Security/Instance RAM roles/Overview.md)
    -   [Bind an instance RAM role](/intl.en-US/Security/Instance RAM roles/Bind an instance RAM role.md) |
    |User Data|User data is used to customize the startup behavior of an ECS instance or pass data to the ECS instance, such as automatically obtaining software resource packages, activating services, and displaying logs. You must prepare a custom script in advance and pass data in the script by using the User Data feature.**Note:** You can specify user data only for scaling configurations in the VPC-type scaling group.

|    -   [Prepare user data](/intl.en-US/Instance/Manage instances/User data/Prepare user data.md)
    -   [Configure user data](/intl.en-US/Instance/Manage instances/User data/Configure user data.md) |

9.  In the Preview step, check your configurations, enter a scaling configuration name, and then click **Create**.

10. In the Created dialog box, click **Enable Configuration**.


**References**  


[Create an instance by using the provided wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the provided wizard.md)

[CreateScalingConfiguration](/intl.en-US/API Reference/Scaling configuration/CreateScalingConfiguration.md)

