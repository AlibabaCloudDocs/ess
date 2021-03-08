# Use SLB in Auto Scaling

You can associate Server Load Balancer \(SLB\) instances with a scaling group. The SLB instances distribute traffic to multiple ECS instances in the scaling group. This improves the performance of the scaling group.

-   You have at least one SLB instance in the **Active** state. For more information, see [Create an SLB instance](/intl.en-US/Classic Load Balancer/User Guide/Instance/Create an SLB instance.md).
-   The SLB instance and the scaling group are in the same region.
-   The SLB instance and the scaling group are in the same VPC if their network type is VPC.
-   If the network type of the SLB instance is classic network, the network type of the scaling group is VPC, and the backend server group of the SLB instance contains VPC-type ECS instances, the ECS instances and the scaling group must be in the same VPC.
-   At least one listener is configured on the SLB instance. For more information, see [Listener overview](/intl.en-US/Classic Load Balancer/User Guide/Listeners/Listener overview.md).
-   Health check is enabled on the SLB instance. For more information, see [Configure health check](/intl.en-US/Classic Load Balancer/User Guide/Health check/Configure health checks.md).

SLB allows multiple ECS instances in a region to share the service load by using the IP address of an SLB instance. These ECS instances act as a high-performance and high-availability application service pool. SLB distributes and controls traffic by using SLB instances, listeners, and backend servers. For more information, see [What is CLB?](/intl.en-US/Classic Load Balancer/Product Introduction/What is CLB?.md)

After an SLB instance is associated with a scaling group, all ECS instances including those automatically and manually created in the scaling group are added to the backend server group of the SLB instance. The SLB instance distributes traffic to the ECS instances based on traffic distribution policies and health check policies. This improves resource availability.

**Note:** Each ECS instance in the backend server group of an SLB instance has a default load balancing weight of 50. You can adjust the weight of an ECS instance. For more information, see [Change the weight of a backend server](/intl.en-US/Classic Load Balancer/User Guide/Backend servers/Default server groups/Change the weight of a backend server.md).

## Procedure

The following section describes the procedure to associate an SLB instance with a scaling group in the Auto Scaling console. For more information about other configurations of a scaling group, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md).

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Go to the page for associating SLB instances with a scaling group.

    -   To create a scaling group to associate with SLB instances, click **Create**.
    -   To modify a scaling group that is not associated with SLB instances, find the scaling group and click **Edit** in the **Actions** column.
5.  Optional. Configure the **Network Type** parameter.

    The network type of a scaling group cannot be changed after the scaling group is created.

6.  Configure the **Associate SLB Instance** parameter.

    1.  Select the SLB instances to be associated with the scaling group.

        You can only associate a limited number of SLB instances with a scaling group. For more information, see [Limits](/intl.en-US/Product Introduction/Limits.md). If your SLB instance does not appear in the drop-down list, check whether your SLB instance meets the prerequisites.

    2.  Select backend server groups for the SLB instance.

        You can select the default server group and vServer groups. For more information, see [Backend server overview](/intl.en-US/Classic Load Balancer/User Guide/Backend servers/Backend server overview.md).

        -   The default server group contains the ECS instances that receive requests forwarded by a listener. If no vServer group or primary and secondary server group is specified for the listener, the listener forwards all requests to the ECS instances in the default server group.
        -   You can select vServer groups if you want to forward requests to different backend servers, or forward requests based on domain names or URLs.
7.  Configure the remaining settings.


**References**  


[CreateScalingGroup](/intl.en-US/API Reference/Scaling group/CreateScalingGroup.md)

[AttachLoadBalancers](/intl.en-US/API Reference/Scaling group/AttachLoadBalancers.md)

[DetachLoadBalancers](/intl.en-US/API Reference/Scaling group/DetachLoadBalancers.md)

[AttachVServerGroups](/intl.en-US/API Reference/Scaling group/AttachVServerGroups.md)

[DetachVServerGroups](/intl.en-US/API Reference/Scaling group/DetachVServerGroups.md)

