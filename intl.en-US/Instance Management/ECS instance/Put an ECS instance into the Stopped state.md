---
keyword: [stopped, No Fees for Stopped Instances \(VPC-Connected\), shutdown and reclaim]
---

# Put an ECS instance into the Stopped state

If the instance reclaim mode of a scaling group is set to Shutdown and Reclaim Mode, you can manually put ECS instances in the scaling group into the Stopped state. During scale-out events, Auto Scaling preferentially starts ECS instances that are in the Stopped state.

-   The network type of the scaling group is VPC.
-   The instance reclaim mode of the scaling group is set to Shutdown and Reclaim Mode.
-   The ECS instance that you want to stop is automatically created.

After an ECS instance in a scaling group is stopped, the instance stops providing services and some resources of the instance are not charged. Therefore, you do not need to manually enable the No Fees for Stopped Instances \(VPC-Connected\) feature in the ECS console. After an ECS instance is put into the Stopped state, the vCPUs, memory, and public IP address of the instance are released and not charged. However, other resources such as cloud disks and elastic IP addresses \(EIPs\) are still charged.

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Find the target scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   Click **Manage** in the **Actions** column.
5.  In the left-side navigation pane, click **ECS Instances**.

6.  Click the **Auto Created** tab.

7.  Find the ECS instance that you want to stop and click **Switch to Stopped** in the **Actions** column.

8.  Click **OK**.


