# Use custom scaling configurations to create scaling groups {#concept_25882_zh .concept}

You must create a scaling group before using Auto Scaling to reallocate resources.

A scaling group is a collection of ECS instances that are applied to the same scenario. You can set scaling group parameters, such as the maximum and minimum number of instances and cooldown time. You can also associate the ECS instances with SLB instances and RDS instances for easy management.

**Note:** There is a limit to the number of scaling groups that you can create under one account. For more information, see [Quantity restrictions](reseller.en-US/User Guide/Usage notes/Quantity restrictions.md#).

For information about using launch templates to create scaling groups, see [Use launch templates to create scaling groups](reseller.en-US/User Guide/Use launch templates to create scaling groups.md#).

## Procedure { .section}

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  On the Scaling Groups page, click **Create Scaling Group**.
3.  Configure the scaling group.
    1.  Enter a name in the **Scaling Group Name** field.
    2.  Enter a number in the **Maximum Instances** field.

        **Note:** When the number of ECS instances exceeds the upper limit, Auto Scaling automatically removes instances to make the number of instances in the scaling group match the upper limit.

    3.  Enter a number in the **Minimum Instances** field.

        **Note:** When the number of ECS instances drops below the lower limit, Auto Scaling automatically adds instances to make the number of instances in the scaling group match the lower limit.

    4.  Enter a number in the **Default Cooldown Time \(Seconds\)** field.

        **Note:** This parameter specifies the cooldown time of a scaling activity. For more information, see [Cool-down time](reseller.en-US/User Guide/Usage notes/Cool-down time.md#).

    5.  Specify the **Removal Policy**.

        **Note:** This parameter specifies the policy for removing ECS instances when the number of instances in the scaling group exceeds the upper limit. For more information, see [Removal policies](reseller.en-US/User Guide/Realize Auto Scaling/Removal policies.md#).

    6.  Select an **Instance Configuration Source**. This example uses **Custom Scaling Configuration**.
    7.  Select a **Network Type**. You must set the following parameters if you select **VPC**:

        1.  Specify a **VPC ID** and a **VSwitch**.
        2.  Specify the **Multi-Zone Scaling Policy**. For more information, see [Multi-zone scaling policy](#).
        3.  Specify the **Reclaim Mode**. For more information, see [Reclaim mode](#).
        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40577/154996088221653_en-US.png)

    8.  \(Optional\) Click **SLB Instances** to associate the scaling group with SLB instances.

        **Note:** A scaling group can be associated with up to five SLB instances at the same time. You can also select the [default server group](../../../../../reseller.en-US/User Guide/后端服务器/Backend server overview.md#section_fzb_g5n_n2b) or [VServer group\(s\)](../../../../../reseller.en-US/User Guide/后端服务器/Backend server overview.md#section_xqs_h2v_vdb) of a SLB instance for the scaling group. You can select up to five VServer groups for a scaling group at the same time. For more information, see [Use Server Load Balancer \(SLB\) in Auto Scaling](reseller.en-US/User Guide/Use Server Load Balancer (SLB) in Auto Scaling.md#).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40577/154996088221654_en-US.png)

    9.  \(Optional\) Add **RDS Instances**. Currently, only RDS databases are supported.

        **Note:** You can only add RDS instances in the region where the scaling group is created. Auto Scaling automatically adds the internal IP addresses of the newly created ECS instances to the whitelist of the RDS instances to allow communication between the ECS and RDS instances.

4.  Click **OK**.
5.  Click **Create Now** to create an ECS instance template that is used to create new ECS instances.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40577/154996088221655_en-US.png)

    **Note:** For more information about scaling configurations, see [Create a scaling configuration](reseller.en-US/User Guide/Scaling configurations/Create a scaling configuration.md#).

6.  In the Apply Scaling Configuration dialog box that appears, click **Confirm**.

## Multi-zone scaling policy {#hxfive .section}

|Policy name|Description|
|:----------|:----------|
|Priority|Scales out ECS instances based on the specified VSwitch. This policy allows Auto Scaling to use a secondary VSwitch to create ECS instances when the primary VSwitch cannot create ECS instance in its region.|
|Distribution balancing|Evenly distributes ECS instances in the specified zones when multiple VSwitches are specified. You can reallocate ECS instances to make them evenly distributed when the ECS instances are unevenly distributed in the zone due to certain issues such as insufficient ECS resources.**Note:** This policy only takes effect when you have specified multiple VSwitches.

|
|Cost optimization|This policy has the following benefits when the network type of the scaling group is VPC:-   Ensures business stability when preemptible instances are selected for the scaling configuration.
-   Reduces costs when multiple instance types are selected for the scaling configuration. Creates an instance based on vCPU billing rates. Instances with the lowest vCPU rate are given priority.
-   Creates the specified type of preemptible instance when multiple preemptible instance types are specified for the scaling configuration.
-   Automatically creates Pay-As-You-Go instances when all types of preemptible instances are unavailable.

|

## Reclaim mode {#section_rmq_bpw_rfb .section}

|Name|Description|
|----|-----------|
|Release Mode|Automatically releases ECS instances based on your scheduled tasks or event-triggered tasks during a scale in event.Creates new ECS instances and adds them to the scaling group based on your scheduled tasks or event-triggered tasks during a scale out event.

|
|Shutdown and Reclaim Mode|Increases scaling efficiency:-   Automatically created ECS instances will be stopped during a scale in event. CPUs and memory of stopped instances will not be billed. However, cloud disks including system disks and data disks, EIP addresses, and bandwidth will still be billed. Public IP addresses will be reclaimed and then reassigned when the ECS instances are restarted. EIP addresses will be reserved. All stopped ECS instances are added to an instance pool.
-   ECS instances in the stopped instance pool will be restarted first when a scale out event starts. If the number of these instances is insufficient, Auto Scaling creates new instances.

**Note:** 

-   This mode is supported only by scaling groups that consist of VPC-connected ECS instances.
-   This mode is not supported by instances with local disks, such as d1, d1ne, ga1, gn5, i1, and i2 instances.
-   We cannot guarantee that all stopped instances in the stopped instance pool can be successfully restarted when Auto Scaling scales out instances. The stopped ECS instances will be released if they cannot be restarted. Auto Scaling creates new ECS instances to ensure that the scaling activity is successful.
-   You cannot modify a scaling group when it is set to the shutdown and reclaim mode.

|

