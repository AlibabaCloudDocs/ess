# Use lifecycle hooks to ensure service availability

After a scaling group is associated with a Server Load Balancer \(SLB\) instance, all the Elastic Compute Service \(ECS\) instances in the scaling group are automatically added to the backend server group of the SLB instance to process the client requests distributed from the SLB instance. In this topic, we recommend that you use lifecycle hooks. During a scale-in or scale-out event, a lifecycle hook can be used to put ECS instances that are being added to or removed from a scaling group into the wait state for a specified period of time to ensure service availability.

A scaling group is associated with an SLB instance. For more information, see [Use SLB in Auto Scaling](/intl.en-US/Instance Management/SLB instance/Use SLB in Auto Scaling.md).

## Scenario 1: Scale-out events

During a scale-out event, created ECS instances are added to a scaling group if you do not create a lifecycle hook for the scaling group. The created ECS instances are also added to the backend server group of the SLB instance that is associated with the scaling group and start to provide services. Applications on ECS instances require some time to start before they can provide services for clients. If the applications are not started when they receive requests from the clients, the applications cannot provide services.

We recommend that you create lifecycle hooks for scaling groups. Before ECS instances in a scaling group are added to the backend server group of an SLB instance that is associated with the scaling group, a lifecycle hook is used to put the ECS instances into the wait state. After applications on the ECS instances are started and the lifecycle hook times out, the ECS instances are added to the backend server group of the SLB instance to provide services. For more information, see [Create a lifecycle hook](/intl.en-US/Scaling Group/Lifecycle hooks/Create a lifecycle hook.md). Take note of the following configurations:

-   Set **Applicable Scaling Activity Type** to **Scale-out Event**.
-   We recommend that you set **Timeout Period** to a period of time during which the applications on the ECS instances can be started.

    **Note:** If you want to terminate the timeout period in advance, you can call the CompleteLifecycleAction operation. For more information, see [CompleteLifecycleAction](/intl.en-US/API Reference/Lifecycle Hook/CompleteLifecycleAction.md).

-   Set **Execution Policy** to **Continue**.

After the lifecycle hook is created, created ECS instances stay in the **Pending** state until the lifecycle hook times out. While the ECS instances are in the wait state, applications on the ECS instances are started. After the ECS instances are put out of the wait state, they are added to the scaling group and the backend server group of the associated SLB instance. The ECS instances provide services when they are in the **In Service** state.

## Scenario 2: Scale-in events

During a scale-in event, ECS instances are removed from a scaling group if you do not create a lifecycle hook for the scaling group. The ECS instances are also removed from the backend server group of the associated SLB instance and stop providing services. However, applications on the ECS instances may be processing requests from clients. This may cause access exceptions on the clients.

We recommend that you create lifecycle hooks for scaling groups. After ECS instances in a scaling group are removed from the backend server group of an SLB instance that is associated with the scaling group, a lifecycle hook is used to put the ECS instances into the wait state. After the ECS instances process the received requests and the lifecycle hook times out, the ECS instances are removed from the scaling group. For more information, see [Create a lifecycle hook](/intl.en-US/Scaling Group/Lifecycle hooks/Create a lifecycle hook.md). Take note of the following configurations:

-   Set **Applicable Scaling Activity Type** to **Scale-in Event**.
-   We recommend that you set **Timeout Period** to the maximum processing time for all requests.

    **Note:** If you want to terminate the timeout period in advance, you can call the CompleteLifecycleAction operation. For more information, see [CompleteLifecycleAction](/intl.en-US/API Reference/Lifecycle Hook/CompleteLifecycleAction.md).


After the lifecycle hook is created, the ECS instances to be removed are first removed from the backend server group of the associated SLB instance and then enter the **Suspending** state until the lifecycle hook times out. While the ECS instances are in the wait state, the ECS instances process the already received requests and no longer receive new requests. After the ECS instances are put out of the wait state, they are removed from the scaling group.

**References**  


[CreateLifecycleHook](/intl.en-US/API Reference/Lifecycle Hook/CreateLifecycleHook.md)

