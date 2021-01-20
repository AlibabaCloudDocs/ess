# ModifyAlarm

You can call this operation to modify an event-triggered task.

## Description

Cloud Monitor collects monitoring data based on the metrics specified in event-triggered tasks. You must use dimensions to specify the scope for collecting monitoring data. For example, you can specify the user\_id and scaling\_group dimensions for an event-triggered task to collect monitoring data about Elastic Compute Service \(ECS\) instances in the specified scaling group of the specified user account.

The following table describes the dimensions that can be specified for each metric.

|Metric

|Description

|Dimension |
|--------|-------------|-----------|
|CpuUtilization

|The CPU utilization in percentage.

|user\_id and scaling\_group |
|ClassicInternetRx

|The inbound traffic over the public network to the classic network. Unit: KB/min.

|user\_id and scaling\_group |
|ClassicInternetTx

|The outbound traffic over the public network from the classic network. Unit: KB/min.

|user\_id and scaling\_group |
|VpcInternetRx

|The inbound traffic over the public network to the Virtual Private Cloud \(VPC\). Unit: KB/min.

|user\_id and scaling\_group |
|VpcInternetTx

|The outbound traffic over the public network from the VPC. Unit: KB/min.

|user\_id and scaling\_group |
|IntranetRx

|The inbound traffic over the internal network. Unit: KB/min.

|user\_id and scaling\_group |
|IntranetTx

|The outbound traffic over the internal network. Unit: KB/min.

|user\_id and scaling\_group |
|LoadAverage

|The average system load.

|user\_id and scaling\_group |
|MemoryUtilization

|The memory usage in percentage.

|user\_id and scaling\_group |
|SystemDiskReadBps

|The number of bytes read from the system disk per second.

|user\_id and scaling\_group |
|SystemDiskWriteBps

|The number of bytes written to the system disk per second.

|user\_id and scaling\_group |
|SystemDiskReadOps

|The number of times that the system disk is read per second.

|user\_id and scaling\_group |
|SystemDiskWriteOps

|The number of times that the system disk is written per second.

|user\_id and scaling\_group |
|PackagesNetIn

|The number of packets that are received by the network interface controller \(NIC\) per second.

|user\_id, scaling\_group, and device |
|PackagesNetOut

|The number of packets that are sent by the NIC per second.

|user\_id, scaling\_group, and device |
|TcpConnection

|The number of TCP connections.

|user\_id, scaling\_group, and state |

The values of user\_id and scaling\_group are set by the system, whereas the values of device and state must be manually set. For more information, see the Dimension.N.DimensionKey and Dimension.N.DimensionValue parameters in the Request parameters section of this topic.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=ModifyAlarm&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyAlarm|The operation that you want to perform. Set the value to ModifyAlarm. |
|AlarmTaskId|String|Yes|asg-bp1hvbnmkl10vll5\*\*\*\*\_f95ce797-dc2e-4bad-9618-14fee7d1\*\*\*\*|The ID of the event-triggered task. |
|RegionId|String|Yes|cn-qingdao|The region ID of the event-triggered task. |
|Name|String|No|alarmtask\*\*\*\*|The name of the event-triggered task. |
|Description|String|No|Test alarm task.|The description of the event-triggered task. |
|AlarmAction.N|RepeatList|No|ari:acs:ess:cn-hangzhou:140692647\*\*\*\*:scalingrule/asr-bp163l21e07uhn\*\*\*\*|The unique identifier of scaling rule N to be associated with the event-triggered task. |
|MetricName|String|No|MemoryUtilization|The name of the metric. Valid values:

 -   CpuUtilization: the CPU utilization in percentage.
-   ClassicInternetRx: the inbound traffic over the public network to the classic network. Unit: KB/min.
-   ClassicInternetTx: the outbound traffic over the public network from the classic network. Unit: KB/min.
-   VpcInternetRx: the inbound traffic over the public network to the Virtual Private Cloud \(VPC\). Unit: KB/min.
-   VpcInternetTx: the outbound traffic over the public network from the VPC. Unit: KB/min.
-   IntranetRx: the inbound traffic over the internal network. Unit: KB/min.
-   IntranetTx: the outbound traffic over the internal network. Unit: KB/min.
-   LoadAverage: the average system load.
-   MemoryUtilization: the memory usage in percentage.
-   SystemDiskReadBps: the number of bytes read from the system disk per second.
-   SystemDiskWriteBps: the number of bytes written to the system disk per second.
-   SystemDiskReadOps: the number of times that the system disk is read per second.
-   SystemDiskWriteOps: the number of times that the system disk is written per second.
-   PackagesNetIn: the number of packets that are received by the NIC per second.
-   PackagesNetOut: the number of packets that are sent by the NIC per second.
-   TcpConnection: the number of TCP connections.

 For more information, see the Description section of this topic. |
|MetricType|String|No|system|The type of the metric. Valid values:

 -   system: the built-in metric of Cloud Monitor.
-   custom: the custom metric that is used to report relevant data of ECS instances to Cloud Monitor. |
|Period|Integer|No|300|The period for collecting the statistical value of the metric. Unit: seconds. Valid values:

 -   60
-   120
-   300
-   900 |
|Statistics|String|No|Average|The type of the statistical value that is collected for the metric. Valid values:

 -   Average: the average value.
-   Minimum: the minimum value.
-   Maximum: the maximum value. |
|Threshold|Float|No|80|The threshold of the metric. The alert condition of the event-triggered task specifies the relationship between the statistical value and the threshold of the metric. When the alert condition is met for the specified number of times, Auto Scaling triggers an alert and executes the scaling rules specified in the event-triggered task. |
|ComparisonOperator|String|No|\>=|The operator for comparison between the collected metric value and the threshold. This parameter is used to specify the relationship between the metric value and the threshold that meets the alert condition. Valid values:

 -   \>=: The metric value is greater than or equal to the threshold.
-   <=: The metric value is less than or equal to the threshold.
-   \>: The metric value is greater than the threshold.
-   <: The metric value is less than the threshold. |
|EvaluationCount|Integer|No|3|The number of times that the alert condition must be met to trigger an alert and execute scaling rules. For example, if this parameter is set to 3, an alert is triggered when the average CPU utilization is greater than or equal to 80% for three times. |
|GroupId|Integer|No|4055401|The ID of the application group to which the custom metric belongs. This parameter takes effect only when the MetricType parameter is set to custom. |
|Dimension.N.DimensionKey|String|No|device|The key of dimension N to be associated with the metric. Valid values:

 -   user\_id: the ID of your account.
-   scaling\_group: the scaling group to be monitored.
-   device: the type of the network interface controller \(NIC\).
-   state: specifies whether to count the total number of TCP connections or the number of TCP connections that have been established and are available. |
|Dimension.N.DimensionValue|String|No|eth0|The value of dimension N to be associated with the metric. The valid value of this parameter depends on the Dimension.N.DimensionKey parameter.

 When the value of Dimension.N.DimensionKey is user\_id, the value of this parameter is set by the system.

 When the value of Dimension.N.DimensionKey is scaling\_group, the value of this parameter is set by the system.

 When the value of Dimension.N.DimensionKey is device, the valid values of this parameter are:

 -   eth0: the internal network NIC for classic network-type ECS instances, and the only NIC for VPC-type ECS instances.
-   eth1: the public network NIC for classic network-type ECS instances.

 When the value of Dimension.N.DimensionKey is state, the valid values of this parameter are:

 -   TCP\_TOTAL: specifies to count the total number of TCP connections.
-   ESTABLISHED: specifies to count the number of TCP connections that have been established and are available. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AlarmTaskId|String|asg-bp1hvbnmkl10vll5\*\*\*\*\_83948190-acdd-483f-98f7-b77f4778\*\*\*\*|The ID of the event-triggered task. |
|RequestId|String|BACACF83-7070-4953-A8FD-D81F89F1\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=ModifyAlarm
&RegionId=cn-qingdao
&AlarmTaskId=asg-bp1hvbnmkl10vll5****_83948190-acdd-483f-98f7-b77f4778****
&MetricName=MemoryUtilization
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyAlarmResponse>
    <AlarmTaskId>asg-bp1hvbnmkl10vll5****_83948190-acdd-483f-98f7-b77f4778****</AlarmTaskId>
    <RequestId>BACACF83-7070-4953-A8FD-D81F89F1****</RequestId>
</ModifyAlarmResponse>
```

`JSON` format

```
{
	"AlarmTaskId": "asg-bp1hvbnmkl10vll5****_83948190-acdd-483f-98f7-b77f4778****",
	"RequestId": "BACACF83-7070-4953-A8FD-D81F89F1****"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

