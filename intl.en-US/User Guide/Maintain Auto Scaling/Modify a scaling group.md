# Modify a scaling group {#concept_qkz_nkx_rfb .concept}

This topic describes how to modify a scaling group.

You can modify the attributes of a scaling group based on your actual needs after it is created.

**Note:** If you specify the **Maximum Instances** or **Minimum Instances** parameter and the number of instances exceeds or drops below the limit, Auto Scaling automatically adds or removes instances to make sure that the number of instances is valid.

## Procedure {#section_psv_wkx_rfb .section}

Follow these steps to modify the attributes of a scale group:

1.  On the Scaling Groups page, click **Edit** in the **Actions** column.
2.  In the Edit Scaling Group dialog box that appears, modify the attributes as needed.
    1.  Enter a name in the **Scaling Group Name** field.
    2.  Enter a number in the **Maximum Instances** field.

        **Note:** If the specified number exceeds the upper limit, Auto Scaling automatically removes instances to make the number of instances equal to the upper limit.

    3.  Enter a number in the **Minimum Instances** field.

        **Note:** If the specified number drops below the lower limit, Auto Scaling automatically adds instances to make the number of instances equal to the lower limit.

    4.  Enter a number in the **Default Cooldown Time \(Seconds\)** field.

        **Note:** This parameter specifies the default scaling activity cooldown time. For more information, see [Cool-down time](reseller.en-US/User Guide/Usage notes/Cool-down time.md#).

    5.  Configure a **Removal Policy**.

        **Note:** This parameter specifies the policy to remove instances when the number of instances in a scaling group exceeds the upper limit. For more information, see [Removal policies](reseller.en-US/User Guide/Realize Auto Scaling/Removal policies.md#).

    6.  Select an **Instance Configuration Source**.
    7.  \(Optional\) Once selected, you cannot modify the **Network Type** of the scaling group. If the **Network Type** of the scaling group that you need to modify is **VPC**, then you can change the **VSwitch**. However, you cannot change the **Multi-Zone Scaling Policy** or the **Reclaim Mode**.

        ![Modify a scaling group - Change the VSwitch](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40591/154989905021739_en-US.png)

    8.  \(Optional\) Select **SLB Instances**.

        **Note:** A scaling group can be associated with up to five SLB instances at the same time. You can also select the [default server group](../../../../../reseller.en-US/User Guide/后端服务器/Backend server overview.md#section_fzb_g5n_n2b) or [VServer group\(s\)](../../../../../reseller.en-US/User Guide/后端服务器/Backend server overview.md#section_xqs_h2v_vdb) of a SLB instance for the scaling group. You can select up to five VServer groups for a scaling group at the same time. For more information, see [Use Server Load Balancer \(SLB\) in Auto Scaling](reseller.en-US/User Guide/Use Server Load Balancer (SLB) in Auto Scaling.md#).

        ![Modify a scaling group - Modify an SLB instance](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40591/154989905021740_en-US.png)

    9.  \(Optional\) Select **RDS Instances**. Currently, only RDS databases are supported.

        **Note:** You can only add RDS instances that are in the same region where the scaling group is created. After ECS instances are added to the scaling group, Auto Scaling automatically adds the internal IP addresses of the ECS instances to the RDS whitelist to allow internal communication between the ECS and the RDS instances.


