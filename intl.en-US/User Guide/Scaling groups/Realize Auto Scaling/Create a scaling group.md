# Create a scaling group {#concept_25882_zh .concept}

A scaling group is a collection of ECS instances with similar configuration deployed in an application scenario.

It defines the maximum and minimum number of ECS instances in the group, associated Server Load Balancer and RDS instances, and other attributes.

**Note:** The number of the scaling groups that can be created with an account is limited. For more information, see [quantity restrictions](reseller.en-US/User Guide/Usage notes/Quantity restrictions.md#).

## Procedure { .section}

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  On the Scaling Groupspage, click **Create Scaling Group**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40577/154227280032034_en-US.png)

3.  Set the scaling group parameters, and click **Submit**.

    **Note:** For scaling group attributes, see [create a scaling group](#).

4.  Click **Create Scaling Configuration**.

    **Note:** For more information about scaling configuration, see [create a scaling configuration](reseller.en-US/User Guide/Scaling configurations/Create a scaling configuration.md#).

5.  In the Enable Scaling Group dialog box, click **OK**.

## Scaling group attributes {#section_vxs_l4w_rfb .section}

The following table lists the specific scaling group attribute meanings and examples.

|Parameter|Description|Example|Required|
|:--------|:----------|:------|:-------|
|Scaling group name|The name consists of 2-40 characters. It must begin with a lower-case letter, number, or a Chinese character, and can contain ".", "\_" or "-".|sg-yk201808201449|Yes|
|Maximum number of instances for scaling|Maximum number of ECS instances in the scaling group When the upper limit is exceeded, Auto Scaling removes the ECS instances automatically based on the [removal policy](reseller.en-US/User Guide/Scaling groups/Realize Auto Scaling/Removal policies.md#) to make the current number of ECS instances equal to the upper limit.|10|Yes|
|Minimum number of instances for scaling|Minimum number of ECS instances in the scaling group When the lower limit is exceeded, Auto Scaling adds the ECS instances automatically to make the current number of ECS instances equal to the lower limit.|1|Yes|
|Default cool-down time \(second\)|The default cool-down time after a scaling activity occurs in the scaling group For more information, see [cool-down time](reseller.en-US/User Guide/Usage notes/Cool-down time.md#).|600|Yes|
|Removal policy|The policy to remove the ECS instances when the number of ECS instances in the scaling group exceeds the upper limit For more information, see [removal policy](reseller.en-US/User Guide/Scaling groups/Realize Auto Scaling/Removal policies.md#).|The instance corresponded to the oldest scaling configuration|Yes|
|Network type|The type of network to which the scaling group belongs You can select Classic Network or VPC. If you select VPC, you must configure multiple VSwitches. Select multi-zone scaling policies and recycling modes as needed. For specific parameters, see [multi-zone scaling policies](#) and [recycling modes](#).|VPC|Yes|
|Server Load Balancer|If a Server Load Balancer instance is added when you create a scaling group, the scaling group automatically adds the ECS instances in the group to the Server Load Balancer instance. The Server Load Balancer instance in a scaling group extends the service capability of the application and enhances the availability of the application.|slb-yk201807061512|No|
|Database|If an RDS instance is added when you create a scaling group, the scaling group automatically adds the intranet IP of the ECS instance that joined the scaling group to the whitelist of the specified RDS, allowing intranet communication between the ECS instances.|5.7 Basic Edition|No|

**Note:** The scaling group, Server Load Balancer instance, and RDS instance must be in the same region.

## Multi-zone scaling policy {#hxfive .section}

|Policy name|Description|
|:----------|:----------|
|Priority policy|Perform scaling according to the VSwitch you define. When ECS instances cannot be created in the zone to which the VSwitch with higher priority belongs, the system automatically uses the VSwitch with the next priority to create the ECS instance.|
|Even distribution policy|Evenly allocates ECS instances to multiple zones \(that is, multiple VSwitches specified\) specified by the scaling group. If the distribution becomes disequilibrium, you can re-allocate the instances to zones.**Note:** When you set multiple VSwitches, the policy takes effect.

|
|Cost optimization policy|The network type of the scaling group is VPC:-   When preemptible instance is selected for the scaling configuration, the cost optimization policy can be used to guarantee the stability of the business.
-   When multi-instance specification is selected for the scaling configuration, the cost optimization policy can be used to reduce the cost of ECS instances. The cost optimization policy attempts to create instances according to the vCPU price from low to high.
-   When multiple preemptible instances are set for the scaling configuration, the corresponding preemptible instance is created first.
-   When preemptible instances cannot be created, the system attempts to xreate Pay-As-You-Go instances automatically.

|

## Recycling mode {#section_rmq_bpw_rfb .section}

|Mode name|Description|
|---------|-----------|
|Release mode|During scaling down, proper number of ECS instances are automatically released based on the scheduled or alarm tasks.During scaling up, proper number of ECS instances are created to join the scaling group based on the scheduled or alarm tasks.

|
|Downtime recycling mode|The downtime recycling mode improves the time efficiency of scaling. In this mode:-   During scaling down, automatically created ECS instances are in the Stopped status. In this mode, the CPU and memory of the instance are not charged, and the cloud disk \(including the system disk and data disk\), EIP, and bandwidth are still charged. The public network IP is recycled, and is re-allocated when restarted \(the EIP is remained\). These stopped instances form a downtime instance pool.
-   During scaling up, the instances in the downtime instance pool runs first. If the number of downtime instance pools is insufficient, the instance is restarted.

**Note:** 

-   This mode is only supported in scaling groups of VPC-connected instances.
-   It is not supported by all local disk instances \(including but not limited to d1, d1ne, ga1, gn5, i1, i2\).
-   During scaling up, the instances in the downtime instance pool may fail to start. If the stopped instances fail to start, they are released, and new instances are created to guarantee the result of performing scaling rules.
-   If downtime recycling mode is set, the related scaling group cannot be modified.

|

