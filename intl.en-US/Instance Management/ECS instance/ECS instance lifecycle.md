# ECS instance lifecycle

This topic describes how to manage the lifecycle of ECS instances in a scaling group and lists all the possible service states of the instances. When Auto Scaling manages the lifecycle of ECS instances, it checks whether ECS instances are healthy, and removes or even releases unhealthy instances.

## Methods for managing the lifecycle of ECS instances

ECS instances in a scaling group are categorized into automatically created and manually added instances based on how the instances are added to the scaling group. The following table describes the methods for managing the lifecycle of automatically created and manually added instances in a scaling group.

|Type|Description|Management method|
|----|-----------|-----------------|
|Automatically created ECS instances|Instances that are automatically created based on the instance configuration source of a scaling group|Auto Scaling manages the whole lifecycle of an ECS instance. During a scale-out event, Auto Scaling automatically creates ECS instances. During a scale-in event, Auto Scaling stops and releases ECS instances.|
|Manually added ECS instances|Instances that are manually created and then added to a scaling group|The management method depends on whether the scaling group is enabled to manage the lifecycle of the ECS instances: -   If the scaling group is enabled to manage the lifecycle of the ECS instances, the ECS instances are stopped and released during a scale-in event.
-   If the scaling group is not enabled to manage the lifecycle of the ECS instances, the ECS instances are removed from the scaling group, but are not released during a scale-in event.

**Note:** Subscription instances can be manually added to a scaling group, but their lifecycle cannot be managed by the scaling group. |

**Note:** The lifecycle of an ECS instance starts when the instance is created and ends when it is released. The instance lifecycle is different from the process during which an ECS instance is added to and removed from a scaling group. For more information, see [ECS instance lifecycle](/intl.en-US/Instance/ECS instance lifecycle.md).

## Instance service states

The following table lists all the service states through which an ECS instance in a scaling group may transition from when the instance is added to the scaling group to when the instance is removed from the scaling group.

|Service state|Corresponding operation|Description|
|-------------|-----------------------|-----------|
|Pending \(Pending\)|-   [Execute a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Execute a scaling rule.md).

A scaling rule can be executed manually or by using event-triggered or scheduled tasks.

-   [Manually add an ECS instance to a scaling group](/intl.en-US/Instance Management/ECS instance/Manually add an ECS instance to a scaling group.md).

|The ECS instance is being added to a scaling group. During this process, the ECS instance is added to the backend server groups of the associated Server Load Balancer \(SLB\) instances and the whitelists of the associated ApsaraDB RDS instances.|
|Adding:Wait \(Pending:Wait\)|[Create a lifecycle hook](/intl.en-US/Scaling Group/Lifecycle hooks/Create a lifecycle hook.md).|If a lifecycle hook that applies to scale-out events is created for a scaling group, the ECS instance is put into the wait state when it is being added to the scaling group. The instance remains in the wait state until the lifecycle hook times out.You can perform customized operations on the instance during the timeout period, such as binding a secondary elastic network interface \(ENI\) and adding the instance to the whitelist of an ApsaraDB RDS instance. |
|In Service \(InService\)|None|The ECS instance is added to a scaling group and can provide services normally.|
|Standby \(Standby\)|[Put an ECS instance into the Standby state](/intl.en-US/Instance Management/ECS instance/Put an ECS instance into the Standby state.md).|The ECS instance stops providing services and its weight as a backend server of an SLB instance is set to zero. The SLB instance stops forwarding traffic to the ECS instance and Auto Scaling does not manage the lifecycle of the instance. You must manually manage the lifecycle of the instance.You can troubleshoot and update the image of the ECS instance that is in the Standby state, and then put the instance into service again. |
|Protected \(Protected\)|[Put an ECS instance into the Protected state](/intl.en-US/Instance Management/ECS instance/Put an ECS instance into the Protected state.md).|The ECS instance can provide services normally. However, Auto Scaling does not manage the lifecycle of the instance. You must manually manage the lifecycle of the instance.|
|Stopped \(Stopped\)|[Put an ECS instance into the Stopped state](/intl.en-US/Instance Management/ECS instance/Put an ECS instance into the Stopped state.md).|The ECS instance is stopped and put out of service. When the instance is stopped, its vCPUs, memory, and public IP address are reclaimed. You are no longer charged for these resources. However, you are still charged for other resources such as disks and elastic IP addresses \(EIPs\). During scale-out events, Auto Scaling preferentially starts ECS instances that are in the Stopped state in a scaling group.**Note:** If you want to stop an ECS instance in a scaling group, make sure that the instance reclaim mode is set to Shutdown and Reclaim Mode when you create the scaling group. |
|Removing \(Removing\)|-   [Execute a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Execute a scaling rule.md).

A scaling rule can be executed manually or by using event-triggered or scheduled tasks.

-   [Manually remove an ECS instance from a scaling group](/intl.en-US/Instance Management/ECS instance/Manually remove an ECS instance from a scaling group.md).

|The ECS instance is being removed from a scaling group. During this process, the instance is removed from the backend server groups of the associated SLB instances and from the whitelists of the associated ApsaraDB RDS instances.|
|Removing:Wait \(Removing:Wait\)|[Create a lifecycle hook](/intl.en-US/Scaling Group/Lifecycle hooks/Create a lifecycle hook.md).|If a lifecycle hook that applies to scale-in events is created for a scaling group, the ECS instance is put into the wait state when it is being removed from the scaling group. The instance remains in the wait state until the lifecycle hook times out.You can perform customized operations on the instance during the timeout period, such as copying logs and clearing data. |

The following figure shows the transitions between service states of an ECS instance in a scaling group.

![Transitions between service states](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0719521061/p134065.png)

## Instance health check

You can enable or disable the health check feature when or after you create a scaling group. For more information, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md) and [Modify a scaling group](/intl.en-US/Scaling Group/Scaling group/Modify a scaling group.md).

After the health check feature is enabled, Auto Scaling manages the lifecycle of ECS instances in the scaling group and checks the status of these instances on a regular basis. If Auto Scaling detects that an ECS instance is not in the Running state, the instance is considered unhealthy.

**Note:** The running states of an ECS instance are not its service states in a scaling group. The running states refer to all possible states of an ECS instance from when the instance is created to when the instance is released.

The following section describes how unhealthy ECS instances are removed from a scaling group:

-   If the instances are automatically created by Auto Scaling, or are manually added to the scaling group and their lifecycle is managed by the scaling group, Auto Scaling removes and releases these instances.
-   If the instances are manually added to the scaling group and their lifecycle is not managed by the scaling group, Auto Scaling removes these instances from the scaling group but does not release them.

The removal of unhealthy ECS instances is not subject to the minimum number of instances in a scaling group. Therefore, the number of instances in the scaling group may be less than the minimum number of instances after instances are removed. Auto Scaling will automatically create a corresponding number of ECS instances to maintain the minimum number.

**Warning:** Make sure that you have sufficient balance in your account. If you have overdue payments in your account, pay-as-you-go and preemptible instances will be stopped or even released. For information about status changes of ECS instances due to overdue payments, see [Overdue payments](/intl.en-US/Pricing/Overdue payments.md).

