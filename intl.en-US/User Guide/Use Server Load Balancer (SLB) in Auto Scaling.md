# Use Server Load Balancer \(SLB\) in Auto Scaling {#concept_wsy_kts_ggb .concept}

You can associate a scaling group with SLB instances to distribute traffic to multiple ECS instances in a scaling group, improving the performance of the scaling group.

## Overview {#section_fzl_yts_ggb .section}

SLB allows multiple ECS instances in a region to use the same SLB instance IP address to share the service load. These ECS instances act as a high-performance and highly available application service pool. This means that SLB allocates and controls traffic by using SLB instances, listeners, and backend servers. For more information, see [What is Server Load Balancer](../../../../../reseller.en-US/Product Introduction/What is Server Load Balancer?.md#).

## Prerequisites {#section_f2z_hkz_ggb .section}

Make sure that the following requirements are met before you attach SLB instances to a scaling group:

-   You have one or more SLB instances in the **Running** status. If you do not have a running SLB instance, [create an SLB instance](../../../../../reseller.en-US/User Guide/Server Load Balancer instance/Create an SLB instance.md#) first.
-   The SLB instance and the scaling group must be in the same region.
-   The SLB instance and the scaling group must be in the same VPC network if their network type is VPC.
-   If the network type of the SLB instance is classic, the network type of the scaling group is VPC, and the backend server group of the SLB instance contains VPC-connected ECS instances, then the ECS instances and the scaling group must be in the same VPC network.
-   You must configure at least one listener for the SLB instance. For more information about listeners, see [Listener overview](../../../../../reseller.en-US/User Guide/Listeners/Listener overview.md#).
-   You must enable health check for the SLB instance. For more information, see [Configure health check](../../../../../reseller.en-US/User Guide/Health check/Configure health check.md#).

## Manage SLB instances in the Auto Scaling console {#section_f1g_vvs_ggb .section}

**Note:** This section describes how to manage SLB instances in the Auto Scaling console. For more information, see [Use custom scaling configuration to create a scaling group](reseller.en-US/User Guide/Use custom scaling configurations to create scaling groups.md#).

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  On the Scaling Groups page, use one of the following methods to add SLB instances:
    -   Click **Create Scaling Group** in the upper-right corner when you create a scaling group.
    -   Click **Edit** in the **Actions** column when you modify a scaling group.
3.  Select a **Network Type**.

    **Note:** Once selected, you cannot change the network type.

4.  Associate the scaling group with an SLB instance.

    **Note:** You can associate a scaling group with up to five SLB instances at the same time. Your SLB instances may not be displayed if they do not meet the requirements described in [prerequisites](#section_f2z_hkz_ggb). Click **Manage SLB instances** to view and update the SLB instances in the SLB console.

5.  Select a server group for the ECS instances in the scaling group.

    **Note:** You can also select the [default server group](../../../../../reseller.en-US/User Guide/后端服务器/Backend server overview.md#section_fzb_g5n_n2b) or [VServer group\(s\)](../../../../../reseller.en-US/User Guide/后端服务器/Backend server overview.md#section_xqs_h2v_vdb) for each SLB instance in the scaling group. You can select up to five VServer groups for a scaling group at the same time.

    ![Associate the scaling group with an SLB instance](images/35588_en-US.png)

6.  Configure the remaining settings as needed.

## Call API operations to manage SLB instances {#section_z15_4b3_3gb .section}

When you call [CreateScalingGroup](../../../../../reseller.en-US/API-Reference/Scaling group/Create a scaling group.md#) to create a scaling group, you can use LoadBalancerIds to associate the scaling group with SLB instances and use VServerGroup to set the attributes of the VServer group.

To modify a scaling group, you can call AttachLoadBalancers or DetachLoadBalancers to associate or disassociate the scaling group from SLB instances, and call AttachVServerGroups or DetachVServerGroups to add or remove VServer groups.

## Load balancing effect {#section_k5w_hws_ggb .section}

After the scaling group is associated with SLB instances, all ECS instances will be added to the backend server group of the SLB instances. The SLB instances distribute traffic to ECS instances based on traffic distribution and health check policies. This improves resource availability.

**Note:** The weight of these ECS instances is 50 by default, you can adjust the weight on the corresponding SLB instances.

