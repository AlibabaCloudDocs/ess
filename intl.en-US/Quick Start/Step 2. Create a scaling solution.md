# Step 2. Create a scaling solution {#concept_vhg_w5m_qfb .concept}

It takes two main steps as follows to create a simple scaling solution.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40548/154227136032077_en-US.png)

Creating a scaling group is the first step to use Auto Scaling. A scaling group is a set of ECS instances with the same scenarios. You can define the maximum and minimum numbers of ECS instances in the group, its associated Server Load Balancer and RDS instances, and other attributes. After you create a scaling group, its scope attributes cannot be changed. For more information, see [regions and zones](../../../../reseller.en-US/General Reference/Regions and zones.md#). Here is an example of how to create a scaling group and complete the scaling configurations in a region such as China East 2 \(Shanghai \).

## Create a scaling group {#section_gvl_cvm_qfb .section}

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  Select a **Region**, such as China East 2.
3.  Click **Create Scaling Group**.
4.  On the Create Scaling Group page:
    1.  Enter the **Scaling Group Name**, such as ScalingGroupTest.
    2.  Set the **Maximum Number of Instances Allowed for Scaling**, such as 4.
    3.  Set the **Minimum Number of Instances Allowed for Scaling**, such as 1.
    4.  Set the **Default Cool-down Time \(Seconds\)**, such as 600.
    5.  Set the **Removal Policy**. For example, filter the **Earliest Instances** first, and filter **Instances Corresponded to the Earliest Scaling Configurations** from the result.
    6.  Set **Network Type**, such as **VPC**. For more information, see [create a VPC](https://www.alibabacloud.com/help/faq-detail/53604.htm)[create a VPC](https://partners-intl.aliyun.com/help/faq-detail/53604.htm).
    7.  Configure a Server Load Balancer instance Health check must be enabled for all listening ports of the specified Server Load Balancer instance, otherwise, the instance cannot be added to the scaling group.
    8.  Configure an RDS instance
    9.  Click **Submit** to complete the creation.
5.  After the scaling group is created successfully, you can [Create Scaling Configuration](#) directly, or click **Later**.

## Create scaling configurations {#section_hjn_fwm_qfb .section}

**Prerequisite**

You have created an ECS security group. For more information, see [create a security group](../../../../reseller.en-US/User Guide/Security groups/Create a security group.md#).

**Procedure**

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  In the left-side navigation pane, click **Scaling Groups**.
3.  Select a **region**, such as China East 2.
4.  Find the target scaling group, and click **Add Scaling Configuration**.
5.  On the Basic Configurations page:
    1.  Enter the **Scaling Configuration Name**, such as ScalingGroupTest. 1.
    2.  Select a **Billing Method**, such as **Pay-As-You-Go**. For more information, see [Pay-As-You-Go](../../../../reseller.en-US/Pricing/Pay-As-You-Go.md#) and [preemptible instance](../../../../reseller.en-US/Product Introduction/Instances/Preemptible instance.md#).
    3.  Select an **instance** type, such as ecs.xn4.small and ecs.g5.2xlarge. For more information, see [instance type families](../../../../reseller.en-US/Product Introduction/Instance type families.md#).

        **Note:** We recommend that you configure multiple instance types to avoid ECS creation failure due to insufficient resource of certain instance type.

    4.  Select an **image**, such as CentOS 7.4 64. If you want to realize functions like Web server automatic startup, automatic code and script downloading, and so on, select **Custom Image**.
    5.  Select the **storage** type, such as 40 GB Ultra Disk.
    6.  Select the **public network bandwidth**, such as 1 Mbit/s by traffic.
    7.  Select a security group.
    8.  Click **Next**.
6.  On the System Configurations page:
    1.  \(Optional\) Select a tag. For more information, see [add a tag to resources](../../../../reseller.en-US/User Guide/Tags/Add a tag to resources.md#).
    2.  Set logon credentials, such as SSH key pair. For more information, see [create an SSH key pair](../../../../reseller.en-US/User Guide/Key pairs/Create an SSH key pair.md#).
    3.  Set the **Instance Name**, such as ScalingGroupTest.
    4.  Click **Next**.
7.  Confirm the scaling configuration information, including the scaling group set in the previous two steps and the scaling configuration information, and the estimated cost of the scaling configuration. Check the protocol, and click **Confirm**.

    **Note:** The cost only includes the cost of the ECS service. Auto Scaling is for free. For more information, see [billing](../../../../reseller.en-US/Pricing/Billing.md#).

8.  In the dialog box, click **Back** or **Enable Configuration**, such as **Enable Configuration**.

    **Note:** After you enable the scaling configuration, the minimum number of ECS instances you set in the scaling configuration are automatically created and added to the specified Server Load Balancer instance, and the private IPs of the instances are added to the specified RDS instance whitelist.


## What to do next {#section_nbz_zxm_qfb .section}

You can enable your first scaling group in the corresponding region, such as China East 2.

