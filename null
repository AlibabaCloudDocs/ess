# CreateAlarm

You can call this operation to create an event-triggered task.

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

The values of user\_id and scaling\_group are set by the system, whereas the values of device and state must be manually set. For more information, see the Dimension.N.DimensionKey and Dimension.N.DimensionValue parameters in the "Request parameters" section of this topic.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=CreateAlarm&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateAlarm|The operation that you want to perform. Set the value to CreateAlarm. |
|MetricName|String|Yes|CpuUtilization|The name of the metric. Valid values:

-   CpuUtilization: the CPU utilization in percentage.
-   ClassicInternetRx: the inbound traffic over the public network to the classic network. Unit: KB/min.
-   ClassicInternetTx: the outbound traffic over the public network from the classic network. Unit: KB/min.
-   VpcInternetRx: the inbound traffic over the public network to the VPC. Unit: KB/min.
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
|RegionId|String|Yes|cn-qingdao|The region ID of the event-triggered task. |
|ScalingGroupId|String|Yes|asg-bp18p2yfxow2dloq\*\*\*\*|The ID of the scaling group to be monitored by the event-triggered task. |
|Threshold|Float|Yes|80|The threshold of the metric. The alert condition of the event-triggered task specifies the relationship between the statistical value and the threshold of the metric. When the alert condition is met for the specified number of times, Auto Scaling triggers an alert and executes the scaling rules specified in the event-triggered task. |
|Name|String|No|TestAlarmTask|The name of the event-triggered task. |
|Description|String|No|Test alarm task.|The description of the event-triggered task. |
|AlarmAction.N|RepeatList|No|ari:acs:ess:cn-hangzhou:1406926\*\*\*\*:scalingrule/asr-bp163l21e07uhn\*\*\*\*|The unique identifier of scaling rule N to be associated with the event-triggered task. |
|MetricType|String|No|system|The type of the metric. Valid values:

-   system: the built-in metric of Cloud Monitor.
-   custom: the custom metric that is used to report relevant data of ECS instances to Cloud Monitor. |
|Period|Integer|No|300|The period for collecting the statistical value of the metric. Unit: seconds. Valid values:

-   60
-   120
-   300
-   900

Default value: 300. |
|Statistics|String|No|Average|The type of the statistical value that is collected for the metric. Valid values:

-   Average: the average value.
-   Minimum: the minimum value.
-   Maximum:the maximum value.

Default value: Average. |
|ComparisonOperator|String|No|\>=|The operator for comparison between the collected metric value and the threshold. This parameter is used to specify the relationship between the metric value and the threshold that meets the alert condition. Valid values:

-   \>=: The metric value is greater than or equal to the threshold.
-   <=: The metric value is less than or equal to the threshold.
-   \>: The metric value is greater than the threshold.
-   <: The metric value is less than the threshold.

Default value: \>=. |
|EvaluationCount|Integer|No|3|The number of times that the alert condition must be met to trigger an alert and execute scaling rules. For example, if this parameter is set to 3, an alert is triggered when the average CPU utilization is greater than or equal to 80% for three times.

Default value: 3. |
|Dimension.N.DimensionKey|String|No|device|The key of dimension N to be associated with a metric. Valid values:

-   user\_id: the ID of your account.
-   scaling\_group: the scaling group to be monitored.
-   device: the type of the NIC.
-   state: specifies whether to count the total number of TCP connections or the number of TCP connections that have been established and are available. |
|Dimension.N.DimensionValue|String|No|eth0|The value of dimension N to be associated with the metric. The value of this parameter depends on the Dimension.N.DimensionKey parameter.

When the value of Dimension.N.DimensionKey is user\_id, the value of this parameter is set by the system.

When the value of Dimension.N.DimensionKey is scaling\_group, this value is set by the system.

When the value of Dimension.N.DimensionKey is device, the valid values of this parameter are:

-   eth0: the internal network NIC for classic network-type ECS instances, and the only NIC for VPC-type ECS instances.
-   eth1: the public network NIC for classic network-type ECS instances.

When the value of Dimension.N.DimensionKey is state, the valid values of this parameter are:

-   TCP\_TOTAL: specifies to count the total number of TCP connections.
-   ESTABLISHED: specifies to count the number of TCP connections that have been established and are available. |
|GroupId|Integer|No|4055401|The ID of the application group to which the custom metric belongs. This parameter takes effect only when the MetricType parameter is set to custom. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AlarmTaskId|String|asg-bp1hvbnmkl10vll5\*\*\*\*\_f95ce797-dc2e-4bad-9618-14fee7d1\*\*\*\*|The ID of the event-triggered task. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=CreateAlarm
&RegionId=cn-qingdao
&ScalingGroupId=asg-bp18p2yfxow2dloq****
&MetricName=CpuUtilization
&Threshold=80
&AlarmAction.1=ari:acs:ess:cn-hangzhou:1406926****:scalingrule/asr-bp163l21e07uhn****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateAlarmResponse>
    <AlarmTaskId>asg-bp1hvbnmkl10vll5****_f95ce797-dc2e-4bad-9618-14fee7d1****</AlarmTaskId>
    <RequestId>ADD82C07-7A7C-4DD4-907F-1D114742****</RequestId>
</CreateAlarmResponse>
```

`JSON` format

```
{
    "AlarmTaskId":"asg-bp1hvbnmkl10vll5****_f95ce797-dc2e-4bad-9618-14fee7d1****",
    "RequestId":"ADD82C07-7A7C-4DD4-907F-1D114742****"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|404

|InvalidParameter

|The specified value of parameter "%s" is not valid.

|The error message returned because the specified "%s" parameter is invalid. |

