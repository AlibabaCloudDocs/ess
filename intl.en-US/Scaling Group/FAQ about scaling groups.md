# FAQ about scaling groups

This topic provides answers to commonly asked questions about scaling groups.

-   FAQ about scaling group configurations
    -   [Must Auto Scaling be used with Alibaba Cloud services such as SLB, Cloud Monitor, and RDS?](#section_s08_me8_us6)
    -   [How many ECS instances can I add to a scaling group?](#section_012_swz_wv6)
    -   [Can I add existing ECS instances to a scaling group?](#section_5pc_nm8_9h7)
    -   [Can I add existing subscription ECS instances to a scaling group?](#section_dxu_nq9_etn)
    -   [Can I add an ECS instance to multiple scaling groups?](#section_v7t_w23_hr0)
    -   [Can I control how Auto Scaling removes ECS instances from a scaling group?](#section_w54_0xc_xg1)
    -   [After I disable a scaling group, does Auto Scaling release ECS instances that are automatically added to the scaling group?](#section_z1p_h7c_abl)
-   FAQ about scaling configurations
    -   [Can I specify multiple ECS instance types for a scaling configuration?](#section_nok_06f_7lk)
    -   [Can I configure 8-core or 16-core ECS instances for a scaling group?](#section_yac_v6f_yyk)
    -   [How do I set the capacity of data disks for ECS instances that are automatically created by Auto Scaling?](#section_ipn_53q_9d6)
    -   [If Auto Scaling uses images from Alibaba Cloud Marketplace to create ECS instances, how do I make sure that the ECS instances can be created?](#section_0af_02b_s62)
    -   [Can I buy multiple images from Alibaba Cloud Marketplace at a time?](#section_0bk_5ek_5hj)
    -   [If Alibaba Cloud Marketplace no longer provides an image that is used to create ECS instances in Auto Scaling, how do I make sure that ECS instances can be created with the image?](#section_uaf_q73_ltq)
    -   [Why is an error of unsupported Alibaba Cloud Marketplace images returned when Auto Scaling creates an ECS instance?](#section_6tm_x8s_o62)
    -   [Can images of different regions use the same product code?](#section_h4w_acv_igz)
    -   [I purchased 100 images with the same product code. Can I use them in any region?](#section_83p_ke7_gfu)
-   FAQ about scaling activities
    -   [What information do I need to provide when I submit a ticket about Auto Scaling?](#section_xrn_c52_zke)
    -   [Why is a resource error returned when Auto Scaling creates an ECS instance?](#section_c99_9lu_isv)
    -   [How do I avoid scale-out failures due to insufficient inventory of an instance type?](#section_brg_xys_xgb)
    -   [Why is an ECS instance for which I enabled release protection automatically released from a scaling group?](#section_ty9_oli_yc4)
    -   [How do I prevent Auto Scaling from automatically releasing an ECS instance that I manually added to a scaling group?](#section_7ji_np8_vy4)
    -   [When Auto Scaling automatically adds or removes ECS instances to or from a scaling group, does Auto Scaling automatically add or remove the IP addresses of the ECS instances to or from the whitelists of the RDS instances or ApsaraDB for Memcache instances associated with the scaling group?](#section_p3y_qln_5h0)
    -   [How do I prevent Auto Scaling from automatically removing an ECS instance that I manually added to a scaling group?](#section_wwv_wqt_7er)
    -   [Can Auto Scaling automatically adjust the CPU, memory, and bandwidth of ECS instances?](#section_k5y_xa2_ykd)
    -   [After ECS instances are removed from scaling groups and released, is the data of the ECS instances retained?](#section_t03_8tt_d7y)
    -   [How do I delete ECS instances that are automatically created by Auto Scaling in a scaling group?](#section_0dg_bhr_74x)
    -   [When Auto Scaling automatically creates multiple ECS instances, will Auto Scaling attempt to recreate instances that fail to be created?](#section_4hk_err_pwe)
-   FAQ about ECS instances in scaling groups
    -   [For an ECS instance that is automatically created by Auto Scaling, how do I obtain its password and log on to it?](#section_3db_mu8_l7z)
    -   [Why am I unable to use the password set in the custom image to log on to an ECS instance that is automatically created by Auto Scaling?](#section_leh_e9v_f9z)
    -   [How do I synchronize data to ECS instances in a scaling group?](#section_pwt_1d0_d2i)
    -   [Why is IP Address 127.0.0.1 deleted from the /etc/hosts file of ECS instances that are automatically created by Auto Scaling?](#section_gkh_sb6_dxh)
-   FAQ about SLB instances associated with scaling groups
    -   [What does an SLB instance do after it is associated with a scaling group?](#section_z3p_c1m_gwo)
    -   [How do SLB instances work with scaling groups?](#section_w8e_ln5_36d)
    -   [After an ECS instance is added to a scaling group, does Auto Scaling automatically add the ECS instance to an SLB instance as a backend server?](#section_032_8qb_jdq)
    -   [Can Auto Scaling add an automatically created ECS instance to multiple SLB instances as a backend server?](#section_ix6_1fd_tfx)
    -   [After an ECS instance is added to an SLB instance as a backend server, can I change the weight of the ECS instance?](#section_kng_0nf_mh2)
    -   [After I associate a public SLB instance with a scaling group, do I need to set the public bandwidth for ECS instances when I create a scaling configuration for the scaling group?](#section_stl_1q2_qt9)
    -   [Why is a health check error about the SLB instance returned when I create a scaling group?](#section_v4m_d6k_9zp)
    -   [How does an SLB instance determine whether a newly created ECS instance can process requests?](#section_zx2_7xq_n1e)
    -   [Why does the timeout period of a Layer-7 HTTP listener of an SLB instance exceed 60 seconds?](#section_vj3_piv_qog)
-   FAQ about RDS instances associated with scaling groups
    -   [What does an RDS instance do after it is associated with a scaling group?](#section_zjm_20i_w3g)
    -   [How do RDS instances work with scaling groups?](#section_w0t_tvt_ooi)

## Must Auto Scaling be used with Alibaba Cloud services such as SLB, Cloud Monitor, and RDS?

No, Auto Scaling is an open and flexible service and can be used alone without the need to combine Server Load Balancer \(SLB\), ApsaraDB RDS \(RDS\), or Cloud Monitor. We recommend that you use Auto Scaling with these Alibaba Cloud services to improve performance. You can deploy Auto Scaling with SLB or RDS and use Cloud Monitor to trigger scaling activities in Auto Scaling. For information about these Alibaba Cloud services, see the following topics:

-   SLB: [What is SLB?](/intl.en-US/Product Introduction/What is SLB?.md)
-   RDS: [What is ApsaraDB for RDS?](/intl.en-US/Product Introduction/What is ApsaraDB for RDS?.md)
-   Cloud Monitor: [Event-triggered task overview](/intl.en-US/Automatic Scaling/Alarm tasks/Event-triggered task overview.md)

## How many ECS instances can I add to a scaling group?

For information about the limits related to Auto Scaling, see [Limits](/intl.en-US/Product Introduction/Limits.md).

## Can I add existing ECS instances to a scaling group?

Yes, you can add existing ECS instances to a scaling group. Make sure that the ECS instances meet the following conditions:

-   The ECS instances and the scaling group must be in the same region. For more information, see [Regions and zones](https://www.alibabacloud.com/help/doc-detail/40654.htm).
-   The ECS instances are in the **Running** state. For more information, see [ECS instance lifecycle](/intl.en-US/Instance/ECS instance lifecycle.md).
-   The ECS instances are not added to other scaling groups.

## Can I add existing subscription ECS instances to a scaling group?

Yes, you can add existing subscription or pay-as-you-go instances to a scaling group. You can add existing ECS instances to a scaling group, including subscription and pay-as-you-go instances. Additionally, Auto Scaling can automatically create pay-as-you-go and preemptible instances.

## Can I add an ECS instance to multiple scaling groups?

No, you can add an ECS instance only to a single scaling group.

## Can I control how Auto Scaling removes ECS instances from a scaling group?

Yes, you can control how Auto Scaling removes ECS instances from a scaling group. You can set a removal policy for a scaling group to preferentially remove the ECS instances created based on the Earliest Instance Created Using Scaling Configuration, Earliest Created Instance, or Most Recent Created Instance option. For more information, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md).

## After I disable a scaling group, does Auto Scaling release ECS instances that are automatically added to the scaling group?

No, Auto Scaling does not automatically release ECS instances after you disable a scaling group by using the Auto Scaling console or calling an API operation. For more information, see [Change the status of a scaling group](/intl.en-US/Scaling Group/Scaling group/Disable a scaling group.md).

## Can I specify multiple ECS instance types for a scaling configuration?

Yes, you can specify multiple ECS instance types for a scaling configuration. This increases the success rate of creating ECS instances. However, make sure that the number of ECS instance types specified for a scaling configuration does not exceed the upper limit. For more information, see [Limits](/intl.en-US/Product Introduction/Limits.md).

## Can I configure 8-core or 16-core ECS instances for a scaling group?

Yes, you can configure 8-core or 16-core ECS instances for a scaling group. If the current available instance types cannot meet your requirements,[submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to request the use of more ECS instance types.

## How do I set the capacity of data disks for ECS instances that are automatically created by Auto Scaling?

You can specify the capacity of data disks in the Storage section when you create a scaling configuration. For more information, see [Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md).

## If Auto Scaling uses images from Alibaba Cloud Marketplace to create ECS instances, how do I make sure that the ECS instances can be created?

If you want Auto Scaling to create N instances that use the same Alibaba Cloud Marketplace image, you must purchase the image N times from Alibaba Cloud Marketplace in advance.

## Can I buy multiple images from Alibaba Cloud Marketplace at a time?

No, you can buy only a single image from Alibaba Cloud Marketplace at a time.

## If Alibaba Cloud Marketplace no longer provides an image that is used to create ECS instances in Auto Scaling, how do I make sure that ECS instances can be created with the image?

We recommend that you use other images available in Alibaba Cloud Marketplace.

## Why is an error of unsupported Alibaba Cloud Marketplace images returned when Auto Scaling creates an ECS instance?

If you specify an Alibaba Cloud Marketplace image that you have not purchased in the scaling configuration, the following error is returned when an ECS instance is created based on the scaling configuration:

```
Fail to create Instance into scaling group("The specified image is from the image market. You have not bought it or your quota has been exceeded.").
```

Auto Scaling cannot create ECS instances by using Alibaba Cloud Marketplace images that you have not purchased. To use Alibaba Cloud Marketplace images to create ECS instances in Auto Scaling, you must purchase the images from[Alibaba Cloud Marketplace](https://marketplace.alibabacloud.com/) in advance.

## Can images of different regions use the same product code?

Yes, images of different regions can use the same product code as long as the images are supported in the regions.

## I purchased 100 images with the same product code. Can I use them in any region?

No, you cannot use an image in all regions. Alibaba Cloud Marketplace images are region-specific. If you want to use an image in a specific region, purchase the image for that region.

## What information do I need to provide when I submit a ticket about Auto Scaling?

When you [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex), provide the ID of the scaling activity or relevant logs to facilitate troubleshooting. The ID of a scaling activity is specified by the ScalingActivityId parameter.

For information about how to query scaling activities, see [View the details of a scaling activity](/intl.en-US/Monitoring/Scaling events/View the details of a scaling activity.md).

## Why is a resource error returned when Auto Scaling creates an ECS instance?

If the following errors are returned, ECS resources may be insufficient. We recommend that you change the zone for the scaling group and try again.

```
Fail to create Instance into scaling group("The resource is out of usage".).
```

```
Fail to create Instance into scaling group(The specified region is in resource control, please try later.").
```

## How do I avoid scale-out failures due to insufficient inventory of an instance type?

When you create a scaling group, specify multiple zones by selecting VSwitches in different zones. When you create a scaling configuration for the scaling group, select multiple ECS instance types. Then, if an instance type is unavailable in one zone, Auto Scaling automatically selects another instance type with sufficient inventory in that zone. If all instance types are unavailable in that zone, Auto Scaling switches to another zone. For more information, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md) and [Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md).

## Why is an ECS instance for which I enabled release protection automatically released from a scaling group?

Auto Scaling can automatically release an ECS instance created during a scale-out event even if you enabled release protection by using the ECS console or calling the [ModifyInstanceAttribute](/intl.en-US/API Reference/Instances/ModifyInstanceAttribute.md) operation.

To prevent an ECS instance from being automatically released, you must put the ECS instance into the protected state. For more information, see [Put an ECS instance into the Protected state](/intl.en-US/Instance Management/ECS instance/Put an ECS instance into the Protected state.md).

## How do I prevent Auto Scaling from automatically releasing an ECS instance that I manually added to a scaling group?

To prevent an ECS instance from being automatically released, you must put the ECS instance into the protected state. For more information, see [Put an ECS instance into the Protected state](/intl.en-US/Instance Management/ECS instance/Put an ECS instance into the Protected state.md).

## When Auto Scaling automatically adds or removes ECS instances to or from a scaling group, does Auto Scaling automatically add or remove the IP addresses of the ECS instances to or from the whitelists of the RDS instances or ApsaraDB for Memcache instances associated with the scaling group?

Auto Scaling can automatically add or remove the IP addresses of ECS instances to or from the whitelists of RDS instances, but not the ApsaraDB for Memcache instances.

## How do I prevent Auto Scaling from automatically removing an ECS instance that I manually added to a scaling group?

Assume that you want to prevent Auto Scaling from automatically removing the 100 ECS instances that you manually added to a scaling group. Perform the following operations to configure the scaling group:

-   Set the minimum number of ECS instances in the scaling group to a value greater than or equal to 100.
-   Set the removal policy to **Earliest Instance Created Using Scaling Configuration** for the first step.

Manually added ECS instances are not created based on scaling configurations. Therefore, the preceding settings ensure that Auto Scaling preferentially selects, removes, and releases automatically created ECS instances. Auto Scaling selects and removes manually added ECS instances only after all automatically created ECS instances are removed. When Auto Scaling removes a manually created ECS instance, Auto Scaling does not release the ECS instance.

**Note:** To prevent Auto Scaling from automatically removing a manually added ECS instance, do not stop the ECS instance. If the ECS instance is stopped, Auto Scaling considers that the ECS instance is unhealthy and automatically removes it.

## Can Auto Scaling automatically adjust the CPU, memory, and bandwidth of ECS instances?

No, Auto Scaling cannot automatically adjust the CPU, memory, or bandwidth of ECS instances. Auto Scaling can automatically add or remove ECS instances based on scaling rules in response to business changes. However, Auto Scaling cannot automatically change the configurations of a single ECS instance.

## After ECS instances are removed from scaling groups and released, is the data of the ECS instances retained?

No, Auto Scaling does not retain any data of ECS instances after the instances are removed and released. Therefore, do not store application status information or important data, such as sessions, databases, and logs, on ECS instances that belong to a scaling group. If the status information of your applications must be stored, we recommend that you store the status information on an independent state server or in a database or service. For example, you can store the status information on an independent ECS instance, in RDS, or in Log Service.

## How do I delete ECS instances that are automatically created by Auto Scaling in a scaling group?

Log on to the Auto Scaling console, find the ECS instances that you want to delete, and then delete them. For more information, see [Manually remove an ECS instance from a scaling group](/intl.en-US/Instance Management/ECS instance/Manually remove an ECS instance from a scaling group.md).

## When Auto Scaling automatically creates multiple ECS instances, will Auto Scaling attempt to recreate instances that fail to be created?

No, Auto Scaling will not attempt to recreate instances that fail to be created. Auto Scaling does not guarantee that all ECS instances are created in a scaling activity. If some instances fail to be created during a scaling activity, Auto Scaling considers that the scaling activity is complete without attempting to recreate the failed instances. You can view the status of a scaling activity in the Auto Scaling console. For more information, see [View the details of a scaling activity](/intl.en-US/Monitoring/Scaling events/View the details of a scaling activity.md).

Assume that Auto Scaling attempts to automatically create 20 ECS instances. 19 instances are created, and one instance fails to be created. Then, Auto Scaling adds the 19 created instances to the scaling group but does not attempt to recreate the failed one. The scaling activity is complete but is in the **Warning** state.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8460881061/p64066.png)

## For an ECS instance that is automatically created by Auto Scaling, how do I obtain its password and log on to it?

If the ECS instance is a Linux instance and a Secure Shell \(SSH\) key pair is set in the scaling configuration for creating the ECS instance, you can use the SSH key pair to log on to the ECS instance. Auto Scaling does not allow you to set a unified password for automatically created ECS instances. For Linux ECS instances, we recommend that you set an SSH key pair in the scaling configuration.

If you do not set an SSH key pair in the scaling configuration, you must reset the password for the ECS instance in the ECS console. The new password takes effect after the ECS instance is restarted. Then, you can use the new password to log on to the ECS instance.

## Why am I unable to use the password set in the custom image to log on to an ECS instance that is automatically created by Auto Scaling?

For security reasons, Auto Scaling does not use the password set in the custom image as the logon password of automatically created ECS instances. We recommend that you set an SSH key pair in the scaling configuration for creating an ECS instance. Then, you can use the SSH key pair to log on to the ECS instance.

If you do not set an SSH key pair in the scaling configuration, you must reset the password for the ECS instance in the ECS console. The new password takes effect after the ECS instance is restarted. Then, you can use the new password to log on to the ECS instance.

## How do I synchronize data to ECS instances in a scaling group?

You can configure a custom image in the scaling configuration for creating ECS instances. In this way, you can pass custom data to the created ECS instances. To synchronize data to or from a running ECS instance, we recommend that you install rsync on the ECS instance and use rsync to transfer data.

## Why is IP Address 127.0.0.1 deleted from the /etc/hosts file of ECS instances that are automatically created by Auto Scaling?

If you use a custom image where the /etc/hosts file is modified to create ECS instances, the file is restored to default settings when Auto Scaling automatically creates ECS instances from the custom image. Therefore, your modifications to the /etc/hosts file are lost. To retain the modifications to the /etc/hosts file, add a script to the rc.local file to check whether the corresponding information exists in the /etc/hosts file and add the information if the information does not exist.

## What does an SLB instance do after it is associated with a scaling group?

The SLB instance forwards traffic to ECS instances in the scaling group based on the routing method. By associating an SLB instance with a scaling group, you can improve the performance and availability of your applications. For more information about SLB, see [What is SLB?](/intl.en-US/Product Introduction/What is SLB?.md).

## How do SLB instances work with scaling groups?

You can specify an SLB instance for one or more scaling groups. Then, Auto Scaling automatically adds ECS instances in the scaling groups to the SLB instance as backend servers. By default, the weight of an ECS instance added to an SLB instance as a backend server is 50. For more information about SLB backend servers, see [Add ECS instances to the default server group](/intl.en-US/User Guide/Backend servers/Default server groups/Add ECS instances to the default server group.md).

## After an ECS instance is added to a scaling group, does Auto Scaling automatically add the ECS instance to an SLB instance as a backend server?

Yes, Auto Scaling automatically adds the ECS instance as a backend server to the SLB instance associated with the scaling group. You must associate the SLB instance with the scaling group in advance.

## Can Auto Scaling add an automatically created ECS instance to multiple SLB instances as a backend server?

Yes, Auto Scaling can add an automatically created ECS instance to multiple SLB instances associated with the scaling group. Only a limited number of SLB instances can be associated with a scaling group. For more information, see [Limits](/intl.en-US/Product Introduction/Limits.md).

If you want to associate more SLB instances with a scaling group,[submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).

## After an ECS instance is added to an SLB instance as a backend server, can I change the weight of the ECS instance?

Yes, you can change the weight of an ECS instance after it is added to an SLB instance as a backend server. For more information, see [Change the weight of a backend server](/intl.en-US/User Guide/Backend servers/Default server groups/Change the weight of a backend server.md).

An SLB instance balances loads among its backend servers based on the ratio of their weights, instead of the weight values. Assume that you have two ECS instances and their weights are both 50. If you change both the weights to 100, the SLB instance balances loads among the two ECS instances in the same way. This is because the weight ratio remains unchanged and is still 1:1. Typically, ECS instances in a scaling group provide the same service and are of the same instance type. Therefore, their weights are the same. By default, the weight of an ECS instance added to an SLB instance as a backend server is 50.

## After I associate a public SLB instance with a scaling group, do I need to set the public bandwidth for ECS instances when I create a scaling configuration for the scaling group?

No, public bandwidth is an optional setting for ECS instances. However, we recommend that you set the public bandwidth to at least 1 Mbit/s when you create a scaling configuration. This facilitates the management of ECS instances.

## Why is a health check error about the SLB instance returned when I create a scaling group?

The following error is returned if health check is disabled for the SLB instance:

```
The current health check type of load balancer "xxxx" does not support this action.
```

Make sure that health check is enabled for SLB instances that are associated with scaling groups. For more information, see [Configure health check](/intl.en-US/User Guide/Health check/Configure health check.md).

## How does an SLB instance determine whether a newly created ECS instance can process requests?

After a newly created ECS instance is added to a scaling group, the SLB instance associated with the scaling group checks whether the corresponding ports on the ECS instance can respond to requests. The SLB instance forwards requests to the new ECS instance only when the ports on the ECS instance can respond to requests.

## Why does the timeout period of a Layer-7 HTTP listener of an SLB instance exceed 60 seconds?

Problem: The timeout period of an HTTP listener is about 60 seconds on an SLB instance. However, the timeout period exceeds 60 seconds for all HTTP requests, or the SLB instance directly returns a 504 error code for an HTTP request.

Cause: You can set the timeout period of an HTTP listener to make sure that an HTTP request is responded within the specified period. However, the total timeout period depends on the number of ECS instances configured for the SLB instance.

If an HTTP request times out on the first ECS instance, the SLB instance forwards the HTTP request to the second ECS instance. The same rule applies to the remaining ECS instances until all ECS instances are polled or until the request is processed by an ECS instance. Assume that three ECS instances are added as backend servers to an SLB instance. The total HTTP timeout period reaches about 180 seconds.

Other services may also affect the HTTP timeout period of an SLB instance. We recommend that you do not rely on the HTTP timeout period configured on the SLB instance to monitor the processing of HTTP requests. Instead, we recommend that you configure the timeout period in applications deployed on ECS instances.

## What does an RDS instance do after it is associated with a scaling group?

RDS is a stable, reliable, and scalable online database service. By associating an RDS instance with a scaling group, you can back up data of the scaling group to the RDS instance based on custom backup policies. This improves the security and reliability of the data and allows you to restore the data when it is deleted by mistake. For more information about RDS, see [What is ApsaraDB for RDS?](/intl.en-US/Product Introduction/What is ApsaraDB for RDS?.md).

## How do RDS instances work with scaling groups?

After an RDS instance is associated with a scaling group, Auto Scaling automatically adds the internal IP addresses of newly created ECS instances in the scaling group to the whitelist of the RDS instance. This allows the ECS instances to access the RDS instance over the internal network. You can associate multiple RDS instances with a scaling group. For more information about whitelists of RDS instances, see [Control access to an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Control access to an ApsaraDB RDS for MySQL instance.md).

