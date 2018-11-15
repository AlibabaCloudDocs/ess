# What is Auto Scaling {#concept_25857_zh .concept}

Auto Scaling automatically adjusts the volume of your elastic computing resources to meet your changing business needs. Based on the scaling rules that you set, Auto Scaling automatically adds ECS instances as your business needs grow to ensure that you have sufficient computing capabilities. When your business needs fall, Auto Scaling automatically reduces the number of ECS instances to save on costs.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40535/154227110321244_en-US.png)

## Scaling-out {#section_hmh_c2m_qfb .section}

When you upgrade your business, Auto Scaling automatically upgrades the underlying resources for you to avoid access delays and excessive resource loads.

You can set CloudMonitor to monitor your ECS instance usage in real time. For example, when CloudMonitor detects that ECS instance vCPU usage exceeds 80% in a scaling group, Auto Scaling elastically scales out your ECS resources based on the scaling rules that you set. This is done by automatically creating a suitable number of ECS instances and automatically adding these ECS instances to the Server Load Balancer instance and RDS instance whitelist. For more details, see [create a scaling group](../../../../reseller.en-US/Quick Start/Step 2. Create a scaling solution.md#) in Auto Scaling and [monitor Auto Scaling](../../../../reseller.en-US/User Guide/Cloud service monitoring/Auto Scaling.md#) in CloudMonitor.

**Note:** When Auto Scaling scales out your ECS resources, new ECS instances are automatically created and added to the scaling group by using the active scaling configuration as the template. You can log on to the ECS console to do operations on these ECS instances, such as starting, stopping, and connecting to them.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40535/154227110321245_en-US.png)

## Scaling-in { .section}

When your business needs fall, Auto Scaling automatically releases underlying resources for you to avoid wasting resources.

You can set CloudMonitor to monitor your ECS instance usage in real time. For example, when CloudMonitor detects that ECS instance vCPU usage falls below 30% in a scaling group, Auto Scaling elastically scales in your ECS resources based on the scaling rules that you set. This is done by automatically releasing a suitable number of ECS instances and automatically removing these ECS instances from the Server Load Balancer instance and RDS instance whitelist. For more details, see [removal policy](../../../../reseller.en-US/User Guide/Scaling groups/Realize Auto Scaling/Removal policies.md#) in Auto Scaling and [monitor Auto Scaling](../../../../reseller.en-US/User Guide/Cloud service monitoring/Auto Scaling.md#) in CloudMonitor.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40535/154227110321246_en-US.png)

## Flexible recovery { .section}

Auto Scaling provides a health check function and automatically monitors the health of ECS instances within scaling groups, so the number of healthy ECS instances in a scaling group does not fall below the minimum value that you set.

When Auto Scaling detects that an ECS instance is not healthy, Auto Scaling automatically releases the unhealthy ECS instance, creates a new ECS instance, and adds the new instance to the Server Load Balancer instance and RDS instance whitelist. For more information, see [remove an unhealthy ECS instance](../../../../reseller.en-US/User Guide/Usage notes/Remove an unhealthy ECS instance.md#).

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40535/154227110321247_en-US.png)

## References { .section}

-    [What is ECS](../../../../reseller.en-US/Product Introduction/What is ECS?.md#) 
-    [What is RDS](../../../../reseller.en-US/Product Introduction/What is RDS.md#) 
-    [What is Server Load Balancer](../../../../reseller.en-US/Product Introduction/What is Server Load Balancer?.md#) 
-    [CloudMonitor overview](../../../../reseller.en-US/Product Introduction/Overview.md#) 

