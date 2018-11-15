# Workflow {#concept_25879_zh .concept}

This topic introduces the workflow of Auto Scaling.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40565/154227253121283_en-US.png)

After a scaling group, scaling configuration, scaling rule, and scaling trigger task are created, the system executes the process as follows \(in this example, we add ECS instances\):

1.  The scheduled task triggers the request for executing a scaling rule at the specified time.
    -   The CloudMonitor task monitors the performance of ECS instances in the scaling group in real time and triggers the request for executing a scaling rule based on the configured alarm rules. For example, when the average CPU usage of all ECS instances in the scaling group exceeds 60%.
    -   The task triggers a scaling activity according to the trigger condition.
    -   The custom task triggers the request for executing a scaling rule based on the monitoring system and alarm rules. For example, the number of online users or the job queue.
    -   Health check tasks regularly check the health status of the scaling group and its ECS instances. If an ECS instance is found to be unhealthy \(not in the **Running** status\), the health check task triggers a request to **remove the ECS instance from the group**.
2.  The system triggers a scaling activity through the ExecuteScalingRule interface and specifies the scaling rule to be executed by its unique Alibaba Cloud resource identifier \(ARI\) in this interface.

    If a custom task needs to be executed, you must have the ExecuteScalingRule interface called in your program.

3.  The system obtains information about the scaling rule, scaling group, and scaling configuration based on the scaling rule ARI entered in Step 2 and creates a scaling activity.
    1.  The system uses the scaling rule ARI to query the scaling rule and scaling group, computes the number of ECS instances to be added, and configures the Server Load Balancer and RDS instances.
    2.  According to the scaling group, the system queries the scaling configuration to determine the correct parameters \(CPU, memory, bandwidth\) to use when creating new ECS instances.
    3.  The system creates scaling activity based on the number of ECS instances to be added, the ECS instance configuration, and the Server Load Balancer and RDS instance configurations.
4.  During the scaling activity, the system creates ECS instances and configures Server Load Balancer and RDS instances.
    1.  The system creates the specified number of ECS instances based on the instance configuration.
    2.  The system adds the intranet IP addresses of the created ECS instances to the whitelist of the specified RDS instance and adds the created ECS instances to the specified Server Load Balancer instance.
5.  After the scaling activity is completed, the system starts the cool-down function for the scaling group. The cool-down time must elapse before the scaling group can execute any new scaling activity.

