# Create an alarm task {#concept_och_fzd_sfb .concept}

This topic describes how to create an alarm task.

There are currently two types of alarm tasks: System Metric Alarm Task and Custom Metric Alarm Task.

## Create a System Metric Alarm Task {#section_agz_kzd_sfb .section}

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  Select **Auto-Trigger Tasks** \> **Alarm Tasks**, and then click **Create Alarm Task**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40603/154227491232052_en-US.png)

3.  In the dialog box, enter the custom information, for example:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40603/154227491232053_en-US.png)

    The information of the alarm task in the preceding figure is defined as follows:

    -   test\_cpu\_alarm is the task name, and cpu utilization is the task description.
    -   classic is a monitoring resource, that is, the scaling group monitored by the alarm task.
    -   `System Monitoring` is the monitoring type.
    -   CPU \(CPU utilization\) is the metric.
    -   The data is collected and checked every minute to determine whether the alarm is triggered.
    -   An average value greater than or equal to 50% is the statistical method, which is repeated three times. It means that when average value of the CPU utilization in one minute exceeds the threshold of 50%, and the statistical methods are satisfied three times consecutively, the alarm is triggered.
    -   Scaling rule add1 is an alarm trigger rule, indicating that when an alarm is triggered, the alarm rule add1 is performed, that is, one instance is added.

## Create a Custom Metric Alarm Task {#section_m2w_112_sfb .section}

The process of creating a Custom Metric Alarm Task is similar to creating a System Metric Alarm Task. The only difference is that, the metrics of the System Metric Alarm Task are collected by the CloudMonitor for the users, and the Custom Metric Alarm Task requires the users to report the metrics to the CloudMonitor themselves.

When you create a Custom Metric Alarm Task, the custom metrics that have been reported must exist, that is, the Time Sequence. You can then set alarm rules for this Time Sequence.

Before the Custom Metric Alarm Task is created in the preceding figure, a custom monitoring data stream \(Time Sequence\) has been pushed to the CloudMonitor. The application group which the Time Sequence belongs to is 54504, the metric name is testMetric, and the dimension information is age=10.

