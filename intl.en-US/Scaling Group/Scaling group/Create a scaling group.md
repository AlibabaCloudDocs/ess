# Create a scaling group

This topic describes how to create a scaling group. A scaling group is a group of Elastic Compute Service \(ECS\) instances that are dynamically scaled based on preconfigured rules. A scaling group allows you to set the minimum and maximum numbers of ECS instances, templates used to automatically create ECS instances, and policies for removing ECS instances. You can use a scaling group to maintain a group of ECS instances based on your business requirements.

-   Auto Scaling is activated as prompted if you are using it for the first time.
-   A launch template is created if you want to use it to create ECS instances. For more information, see [Create a launch template](/intl.en-US/Elasticity/Launch template/Create a launch template.md).
-   Before you associate a scaling group with Server Load Balancer \(SLB\) instances, make sure that the following conditions are met:
    -   You have at least one SLB instance in the **Active** state. For more information, see [Create a CLB instance](/intl.en-US/Classic Load Balancer/User Guide/Instance/Create a CLB instance.md).
    -   The SLB instance and the scaling group are in the same region.
    -   The SLB instance and the scaling group are in the same VPC if their network type is VPC.
    -   If the network type of the SLB instance is classic network, the network type of the scaling group is VPC, and the backend server group of the SLB instance contains VPC-type ECS instances, the ECS instances and the scaling group must be in the same VPC.
    -   At least one listener is configured on the SLB instance. For more information, see [Listener overview](/intl.en-US/Classic Load Balancer/User Guide/Listeners/Listener overview.md).
    -   Health check is enabled on the SLB instance. For more information, see [Configure health check](/intl.en-US/Classic Load Balancer/User Guide/Health check/Configure health checks.md).
-   Before you associate a scaling group with ApsaraDB RDS instances, make sure that the following conditions are met:
    -   You have at least one ApsaraDB RDS instance in the **Running** state. For more information, see [What is ApsaraDB RDS?](/intl.en-US/Product Introduction/What is ApsaraDB RDS?.md)
    -   The ApsaraDB RDS instances and the scaling group reside in the same region.

You can create only a limited number of scaling groups. For more information, see [Limits](/intl.en-US/Product Introduction/Limits.md).

## Procedure

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  In the upper-left corner of the Scaling Groups page, click **Create**.

5.  Configure parameters for the scaling group and click **OK**.

    The following table describes the parameters of the scaling group.

    |Parameter|Applicable network type|Description|
    |---------|-----------------------|-----------|
    |**Scaling Group Name**|VPC and classic network|The name must be 2 to 64 characters in length, and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter or a digit.|
    |**Instance Configuration Source**|VPC and classic network|You can specify one of the following configuration sources for the scaling group:    -   **Launch Templates**: uses a launch template to create ECS instances.
    -   **Select Existing Instance**: uses the configurations of an existing ECS instance as a template to create ECS instances. The configurations include the instance type, image, network type, security group, logon password, and tags.
    -   **Create from Scratch**: creates a scaling group without specifying a template. After the scaling group is created, it is in the Disabled state. You must create a scaling configuration or specify a launch template to create ECS instances before you can enable the scaling group.
Then, you must perform the following operations based on the type of the instance configuration source:

    -   If **Instance Configuration Source** is set to **Launch Templates**, select an existing launch template and a template version. You can also select multiple instance types by specifying **Extend Configurations of Launch Template** and set weights for these instance types. For information about weights, see [Use performance metrics to measure Auto Scaling](/intl.en-US/Best practices/Use performance metrics to measure Auto Scaling.md).
    -   If **Instance Configuration Source** is set to **Select Existing Instance**, select an existing ECS instance. |
    |**Tag**|VPC and classic network|You can add tags to search for and manage scaling groups. For more information, see [Overview](/intl.en-US/Tag & Resource/Tags/Overview.md). **Note:** The tags are added to the scaling group. If you want to add tags to an ECS instance in the scaling group, you must specify the tags in the scaling configuration or in the launch template. |
    |**Instance Removing Policy**|VPC and classic network|This policy is used to filter and remove ECS instances from a scaling group based on multiple filter conditions. If multiple ECS instances meet the conditions of the policy, one instance is removed at random. The Instance Removing Policy parameter contains the **Filter First** and **Then Remove from Results** fields. You cannot specify the same value for the two fields. Valid values:

    -   **Earliest Instance Created Using Scaling Configuration**: filters instances to find the ones that were created based on the earliest scaling configuration and launch template. Manually added instances are not associated with scaling configurations or launch templates. Therefore, manually added instances are not filtered first. If all instances associated with all scaling configurations and launch templates have been removed but Auto Scaling must remove more instances from the scaling group, manually added instances are removed at random.

**Note:** Scaling Configuration in **Earliest Instance Created Using Scaling Configuration** indicates the instance configuration source, which includes scaling configurations and launch templates.

The version of a launch template does not indicate the order in which the template was added. For example, you select the lt-foress V2 template when you create a scaling group. Then, you select the lt-foress V1 template to modify the scaling group. The scaling group considers the lt-foress V2 launch template as the template that was added earlier.

    -   **Earliest Created Instance**: filters instances to find the instances that were created at the earliest point in time.
    -   **Most Recent Created Instance**: filters instances to find the most recently created instances.
    -   **No Policy**: This value is available only for **Then Remove from Results**. This value indicates that Auto Scaling does not filter instances based on the Then Remove from Results field.
For example, if Auto Scaling filters instances based on the **Earliest Instance Created Using Scaling Configuration** value of the Filter First field, you can select one of the following values for the Then Remove from Results field:

    -   **No Policy**: This value indicates that Auto Scaling does not filter instances based on the Then Remove from Results field.
    -   **Earliest Created Instance**: filters the instances obtained based on the Filter First field to find the instances that were created at the earliest point in time.
    -   **Most Recent Created Instance**: filters the instances obtained based on the Filter First field to find the most recently created ones. |
    |**Suspended Processes**|VPC and classic network|This parameter allows you to suspend specified processes before you perform some operations. For example, before you stop an ECS instance, you must suspend the health check process to ensure that the instance is not removed from the scaling group if a health check fails. You can suspend the following processes for a scaling group:    -   **Scale-out**: Auto Scaling rejects all scale-out requests.
    -   **Scale-in**: Auto Scaling rejects all scale-in requests.
    -   **Health Check**: Auto Scaling suspends the health check and does not remove unhealthy ECS instances.
    -   **Scheduled Task**: When the execution time of a scheduled task is reached, the scaling rules that are associated with the task are not triggered.
    -   **Event-triggered Task**: When an event-triggered task enters the alert state, the scaling rules that are associated with the task are not triggered.
For more information, see [Suspend a scaling process](/intl.en-US/Scaling Group/Scaling group/Suspend a scaling process.md) and [Resume a scaling process](/intl.en-US/Scaling Group/Scaling group/Resume a scaling process.md). |
    |**Enable Deletion Protection for Scaling Group**|VPC and classic network|After this feature is enabled, the scaling group cannot be deleted by using the Auto Scaling console or by calling API operations.|
    |**Health Check for Instances**|VPC and classic network|After this feature is enabled, Auto Scaling checks the status of ECS instances on a regular basis. If an ECS instance is not in the Running state, the instance is considered to be unhealthy and is removed from the scaling group. For more information, see [ECS instance lifecycle](/intl.en-US/Instance Management/ECS instance/ECS instance lifecycle.md).|
    |**Minimum Number of Instances**|VPC and classic network|When the number of existing ECS instances in a scaling group is less than the minimum number of instances, Auto Scaling automatically adds instances to the scaling group to maintain the minimum number.|
    |**Maximum Number of Instances**|VPC and classic network|When the number of existing ECS instances in a scaling group is greater than the maximum number of instances, Auto Scaling automatically removes ECS instances from the scaling group to maintain the maximum number.|
    |**Expected Number of Instances**|VPC and classic network|Enter the expected number of instances to enable this feature. Auto Scaling automatically maintains the number of ECS instances at the expected number. For more information, see [Expected number of instances](/intl.en-US/Scaling Group/Scaling group/Expected number of instances.md). **Note:** The Expected Number of Instances feature can be enabled only when you create a scaling group. You cannot enable this feature by modifying the number of instances in an existing scaling group. |
    |**Default Cooldown Time \(Seconds\)**|VPC and classic network|This parameter specifies the default cooldown time of a scaling group in seconds. During the cooldown time, Auto Scaling rejects all scaling activity requests triggered by event-triggered tasks. However, scaling activities triggered by other types of tasks such as scheduled tasks and manually executed tasks are not subject to the cooldown time and are immediately executed.|
    |**Network Type**|VPC and classic network|You can specify the **Multi-zone Scaling Policy** and **Instance Reclaim Mode** parameters only for scaling groups in virtual private clouds \(VPCs\). The instances to be added to a scaling group and the scaling group must have the same network type.     -   **VPC**
        -   When you create a scaling configuration, you can select only instance types that support VPCs.
        -   When you manually add existing ECS instances to the scaling group, you can select only instances that are located in the same VPC as the scaling group.
    -   **Classic Network**
        -   When you create a scaling configuration, you can select only instance types that support the classic network.
        -   When you manually add existing ECS instances to the scaling group, you can select only instances that are located in the classic network.
**Note:** The network type of a scaling group cannot be changed after the scaling group is created. |
    |**Multi-zone Scaling Policy**|VPC|You can specify one of the following polices for the scaling group:    -   **Priority Policy**: Instances are created in priority in the region where the vSwitch with the highest priority resides. When an ECS instance cannot be created in the zone where the vSwitch with the highest priority resides, Auto Scaling automatically uses the vSwitch that has the second highest priority to create the ECS instance.
    -   **Balanced Distribution Policy**: The balanced distribution policy is valid only when the scaling group is associated with multiple vSwitches that are distributed across more than two zones. The policy evenly distributes ECS instances across the zones where the vSwitches reside. If the ECS instances are not evenly distributed across zones due to insufficient resources, you can use the Rebalance Distribution feature to evenly distribute the ECS instances. For more information, see [Rebalance the distribution of ECS instances](/intl.en-US/Instance Management/ECS instance/Rebalance the distribution of ECS instances.md).
    -   **Cost Optimization Policy**: The cost optimization policy is valid only when you specify multiple instance types in the scaling configuration. Auto Scaling creates ECS instances based on the unit prices of vCPUs in ascending order. If you select Preemptible Instance as the billing method in the scaling configuration, preemptible instances are preferentially created. If preemptible instances cannot be created due to insufficient resources, Auto Scaling automatically attempts to create pay-as-you-go instances.
If you select **Cost Optimization Policy**, you can continue to configure the following parameters:

    -   **Minimum Pay-as-you-go Instances**: the minimum number of pay-as-you-go ECS instances in the scaling group. Default value: 0. If the number of pay-as-you-go ECS instances in the scaling group is less than this value, Auto Scaling preferentially creates pay-as-you-go instances.
    -   **Percentage of Pay-as-you-go Instances**: the percentage of pay-as-you-go ECS instances among all automatically created instances. Default value: 70. The percentage is calculated based on the difference between the total number of instances and the minimum number of pay-as-you-go instances.
    -   **Lowest Cost Instance Types**: the number of instance types with the lowest cost. Default value: 1. This parameter is valid when multiple instance types are specified in the scaling configuration. When preemptible instances are created, Auto Scaling evenly creates ECS instances by using the lowest-cost instance types.
    -   **Enable Supplemental Preemptible Instances**: After the Supplemental Preemptible Instances feature is enabled, Auto Scaling automatically creates preemptible instances 5 minutes before the existing instances are reclaimed. |
    |**Instance Reclaim Mode**|VPC|You can specify one of the following reclaim modes for a scaling group in a VPC:    -   **Release Mode**: When a scale-in event is triggered, Auto Scaling automatically releases a specific number of ECS instances. When a scale-out event is triggered, Auto Scaling automatically creates a specific number of ECS instances.
    -   **Shutdown and Reclaim Mode**: This mode makes scaling more efficient.
        -   When a scale-in event is triggered, the status of the removed ECS instances becomes No Fees for Stopped Instances \(VPC-Connected\), and their vCPUs, memory, and public IP addresses are reclaimed. You are no longer charged for these resources. However, you are still charged for other resources such as disks and elastic IP addresses \(EIPs\). These stopped ECS instances form a stopped instance pool.

**Note:** If the ECS instances have public IP addresses before they enter the No Fees for Stopped Instances \(VPC-Connected\) state, the instances are reassigned public IP addresses when they are restarted. The IP addresses may be different from the previous ones.

        -   When a scale-out event is triggered, the ECS instances in the stopped instance pool preferentially enter the Running state. If these instances are still insufficient, Auto Scaling creates more ECS instances. The ECS instances in the stopped instance pool may or may not enter the Running state. If the ECS instances in the stopped instance pool cannot enter the running state due to insufficient resources, Auto Scaling releases these instances and creates a specific number of ECS instances.
**Warning:** Make sure that you have sufficient balance in your account. If you have overdue payments in your account, pay-as-you-go and preemptible instances are stopped or released in some cases. For information about status changes of ECS instances in a scaling group due to overdue payments, see [Overdue payments](/intl.en-US/Pricing/Overdue payments.md). |
    |**VPC**|VPC|Select an existing VPC.|
    |**Select VSwitch**|VPC|You must select a vSwitch after you select a VPC. Each vSwitch can belong only to one zone. To deploy ECS instances across multiple zones, you must specify multiple vSwitches that belong to different zones. We recommend that you select multiple zones to mitigate the risk of insufficient resources and increase the success rate of creating ECS instances.|
    |**Add Existing Instance**|VPC and classic network|If **Instance Configuration Source** is set to **Launch Templates** or **Select Existing Instance**, you can add existing ECS instances to a scaling group when you create the scaling group. If you specify the expected number of instances and then add existing instances, the expected number of instances automatically increases. For example, when you create a scaling group, you set the expected number of instances in the scaling group to one and then add two existing instances. After the scaling group is created, two existing instances are added to the scaling group, and the expected number of instances becomes three.

You can select **Enable the scaling group to manage the instance lifecycle**.

    -   If the scaling group is enabled to manage the lifecycle of instances, the instances are released when they are manually removed from the scaling group or automatically removed because they are considered to be unhealthy.
    -   If the scaling group is not enabled to manage the lifecycle of instances, the instances are not released when they are removed from the scaling group.
**Note:** Subscription instances can be added to a scaling group, but their lifecycle cannot be managed by the scaling group. |
    |**Associate SLB Instance**|VPC and classic network|After you associate SLB instances with the scaling group, ECS instances that are added to the scaling group are automatically added as SLB backend servers. You can specify a server group to which to add the ECS instances. ECS instances can be added to the following types of server groups:    -   Default server group: The group of ECS instances that are used to receive requests. If the listener is not configured with a vServer group or a primary/secondary server group, requests are forwarded to the ECS instances in the default server group.
    -   vServer group: If you want to distribute different requests to different backend servers or configure domain name- or URL-based routing methods, you can use vServer groups.
**Note:** If you specify the default server group and multiple vServer groups at the same time, ECS instances are added to all the specified server groups.

You can associate only a limited number of SLB instances and vServer groups with a scaling group. For more information, see [Limits](/intl.en-US/Product Introduction/Limits.md). |
    |**Associate RDS Instance**|VPC and classic network|After you associate ApsaraDB RDS instances with the scaling group, the internal IP addresses of ECS instances that are added to the scaling group are automatically added to the whitelists of the ApsaraDB RDS instances to allow internal communication. You can associate a limited number of ApsaraDB RDS instances with a scaling group. For more information, see [Limits](/intl.en-US/Product Introduction/Limits.md). |

6.  In the **Create Scaling Group** dialog box, click **OK**.

    The created scaling group is displayed in the scaling group list. ECS instances can be added to the scaling group only when the scaling group is in the **Enabled** state. For more information, see [Enable a scaling group](/intl.en-US/Scaling Group/Scaling group/Enable a scaling group.md).

    **Note:** If **Instance Configuration Source** is set to **Create from Scratch**, you must create a scaling configuration or specify a launch template before you can enable a scaling group. For more information, see [Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md).


**References**  


[CreateScalingGroup](/intl.en-US/API Reference/Scaling group/CreateScalingGroup.md)

