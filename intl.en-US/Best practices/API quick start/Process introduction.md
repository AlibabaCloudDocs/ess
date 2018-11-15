# Process introduction {#concept_25869_zh .concept}

This topic explains how to use APIs to create and configure overall scaling solutions, including scheduled, dynamic, customized, and fixed quantity scaling.

Follow the steps shown in the following figure. The first three steps are used to create a simple scaling solution:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40610/154227373132063_en-US.png)

1.  Create a scaling group. Configure the minimum \(Min Size\) and maximum \(Max Size\) number of ECS instances for scaling, and select a Server Load Balancer instance and an RDS instance.
2.  Create scaling configuration. Specify the specifications of ECS instances used for Auto Scaling, such as Image ID and Instance Type.
3.  Enable the scaling group according to the scaling configuration created in Step 2.
4.  Create a scaling rule. For example, **adding N \(number\) ECS instances**.
5.  Create a scheduled task. For example, triggering the scaling rule at 13:00.
6.  Create an alarm task \(CloudMonitor API PutAlarmRule\). For example, adding 1 ECS instance when the CPU usage is equal to or greater than 80%.

