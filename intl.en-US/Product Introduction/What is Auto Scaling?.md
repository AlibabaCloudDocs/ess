---
keyword: [elastic scaling, Auto Scaling, ESS, scale-out, scale-in]
---

# What is Auto Scaling?

Auto Scaling is a management service that automatically adjusts the number of elastic computing resources based on your business demands and policies. When business loads increase, Auto Scaling automatically adds ECS instances to ensure sufficient computing capabilities. When business loads decrease, Auto Scaling automatically removes ECS instances to save costs. It is suitable for applications with fluctuating business loads, as well as applications with stable business loads.

## Example of elastic scaling

You must specify the conditions that are used to trigger elastic scaling. The following figure shows that the monitoring metric is the average vCPU utilization of ECS instances in a scaling group, the threshold value to trigger scale-out events is 80%, and the threshold value to trigger scale-in events is 30%.

![What is ESS? - Diagram of ESS](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0627659951/p21244.png)

## Scale-out

When business loads surge above normal loads, Auto Scaling automatically increases underlying resources. This helps maintain access speed and ensures that resources are not overloaded.

You can configure Cloud Monitor to monitor your ECS instance usage in real time. For example, when Cloud Monitor detects that the vCPU utilization of ECS instances in a scaling group exceeds 80%, Auto Scaling automatically scales out ECS resources based on the scaling rules that you configured. During the scale-out event, Auto Scaling automatically creates ECS instances and adds these ECS instances to the backend server groups of the associated SLB instances and the whitelists of the associated ApsaraDB for RDS instances.

During scale-out events, ECS instances are automatically created based on the instance configuration information of the scaling group. The instance configuration information includes the instance type, operating system, and user data. For more information, see [Overview of instance configuration sources](/intl.en-US/Scaling Group/Instance Configuration Source/Overview of instance configuration sources.md). You can log on to the ECS console to start or stop ECS instances. You can also connect to an ECS instance to modify its system configurations.

![What is ESS? - Diagram of a scale-out event](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0627659951/p21245.png)

## Scale-in

When business loads decrease, ESS automatically releases underlying resources to prevent resource wastage and reduce costs.

You can configure Cloud Monitor to monitor your ECS instance usage in real time. For example, when Cloud Monitor detects that the vCPU utilization of ECS instances in a scaling group is less than 30%, ESS automatically scales in ECS resources based on the scaling rules that you configured. During the scale-in event, ESS automatically releases ECS instances and removes these ECS instances from the backend server groups of the associated SLB instances and the whitelists of the associated ApsaraDB for RDS instances.

![What is ESS? - Diagram of a scale-in event](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0627659951/p21246.png)

## Elastic recovery

ESS provides the health check feature and automatically monitors the health status of ECS instances in a scaling group, so that the number of healthy ECS instances in the scaling group does not fall below the minimum value that is specified for the scaling group.

When ESS detects that an ECS instance is unhealthy, ESS automatically releases the unhealthy ECS instance, creates a new ECS instance, and then adds the new instance to the backend server groups of the associated SLB instances and the whitelists of the associated ApsaraDB for RDS instances.

![What is ESS? - Diagram of elastic recovery](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0627659951/p21247.png)

## References

-   [What is ECS?](/intl.en-US/Product Introduction/What is ECS?.md)
-   [What is ApsaraDB for RDS?](/intl.en-US/Product Introduction/What is ApsaraDB for RDS?.md)
-   [What is SLB?](/intl.en-US/Product Introduction/What is SLB?.md)
-   [What is Cloud Monitor?](/intl.en-US/Product Introduction/What is CloudMonitor?.md)

