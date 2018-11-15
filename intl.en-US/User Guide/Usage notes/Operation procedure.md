# Operation procedure {#concept_25878_zh .concept}

This topic introduces the steps to create a complete Auto Scaling solution.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40564/154227249721282_en-US.png)

1.  Create a scaling group \(CreateScalingGroup\). Configure the minimum and maximum number of ECS instances in the scaling group, and select the associated Server Load Balancer and RDS instances.
2.  Create scaling configuration \(CreateScalingConfiguration\). Configure the ECS instances attributes for Auto Scaling, such as Image ID and Instance Type.
3.  Enable the scaling group with the scaling configuration created in Step 2 \(EnableScalingGroup\).
4.  Create a scaling rule \(CreateScalingRule\). For example, add N ECS instances.
5.  Create a scheduled task \(CreateScheduledTask\). For example, to trigger the scaling rule created in Step 4 at 12:00 AM.
6.  Create an alarm task \(CloudMonitor API PutAlarmRule\). For example, to add 1 ECS instance when the average \(it can also be max or min\) CPU usage is greater than or equal to 80%.

