# Use SLB in Auto Scaling

You can attach Server Load Balancer \(SLB\) instances to a scaling group. The SLB instances distribute traffic to multiple Elastic Compute Service \(ECS\) instances in the scaling group, improving the performance of the scaling group.

-   You have at least one SLB instance in the **Running** state. For more information, see [Create an SLB instance](/intl.en-US/Classic Load Balancer/User Guide/Instance/Create an SLB instance.md).
-   The SLB instance and the scaling group are in the same region.
-   The SLB instance and the scaling group are in the same Virtual Private Cloud \(VPC\) network if their network type is VPC.
-   If the network type of the SLB instance is classic network, the network type of the scaling group is VPC, and the back-end server group of the SLB instance contains VPC-connected ECS instances, then the ECS instances and the scaling group must be in the same VPC network.
-   At least one listener is configured on the SLB instance. For more information, see [Listener overview](/intl.en-US/Classic Load Balancer/User Guide/Listeners/Listener overview.md).
-   Health check is enabled on the SLB instance. For more information, see [Configure health check](/intl.en-US/Classic Load Balancer/User Guide/Health check/Configure health checks.md).

SLB allows multiple ECS instances in a region to share the service load through the IP address of an SLB instance. These ECS instances act as a high-performance and highly available application service pool. Simply put, SLB distributes and controls traffic by using SLB instances, listeners, and back-end ECS servers. For more information, see [What is CLB?](/intl.en-US/Classic Load Balancer/Product Introduction/What is CLB?.md).

After an SLB instance is attached to a scaling group, all ECS instances including those automatically and manually created in the scaling group are added to the back-end server group of the SLB instance. The SLB instance distributes traffic to the ECS instances based on traffic distribution policies and health check policies. This improves resource availability.

**Note:** ECS instances in the back-end server group of an SLB instance have a default load balancing weight of 50. You can adjust the weight of a back-end ECS instance on the SLB instance. For more information, see [Change the weight of a backend server](/intl.en-US/Classic Load Balancer/User Guide/Backend servers/Default server groups/Change the weight of a backend server.md).

## Procedure

This section focuses on operations for attaching an SLB instance to a scaling group in the Auto Scaling console. For more information about other configurations of a scaling group, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md).

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Use either of the following methods to go to the page for attaching an SLB instance to a scaling group:

    -   To create a scaling group, click **Create Scaling Group**.
    -   To modify a scaling group, find the target scaling group and click **Edit** in the **Actions** column.
5.  Set the network type.

    The network type cannot be changed for a scaling group after it is created.

6.  Select the SLB instance to be attached to the scaling group.

    You can only attach a limited number of SLB instances to a scaling group. For more information, see [Limits](/intl.en-US/Product Introduction/Limits.md). If your SLB instance does not appear in the drop-down list, check whether your SLB instance meets the prerequisites.

7.  Select back-end server groups for the SLB instance.

    You can select the default server group and VServer groups. For more information, see [Backend server overview](/intl.en-US/Classic Load Balancer/User Guide/Backend servers/Backend server overview.md).

    -   The default server group contains the ECS instances that receive requests forwarded by a listener. If no VServer group or primary/secondary server group has been specified for the listener, the listener forwards all requests to the ECS instances in the default server group.
    -   You can select VServer groups if you want to forward different requests to different back-end servers, or forward requests based on domain names or URLs. You can only attach a limited number of SLB instances to a scaling group. For more information, see [Limits](/intl.en-US/Product Introduction/Limits.md).
    ![Select server groups](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8959739851/p35588.png)

8.  Configure the remaining settings as needed.


**Related topics**  


[CreateScalingGroup](/intl.en-US/API Reference/Scaling group/CreateScalingGroup.md)

[AttachLoadBalancers](/intl.en-US/API Reference/Scaling group/AttachLoadBalancers.md)

[DetachLoadBalancers](/intl.en-US/API Reference/Scaling group/DetachLoadBalancers.md)

[AttachVServerGroups](/intl.en-US/API Reference/Scaling group/AttachVServerGroups.md)

[DetachVServerGroups](/intl.en-US/API Reference/Scaling group/DetachVServerGroups.md)

