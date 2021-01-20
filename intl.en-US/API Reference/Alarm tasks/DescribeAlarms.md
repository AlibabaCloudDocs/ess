# DescribeAlarms

You can call this operation to query one or more event-triggered tasks.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeAlarms&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAlarms|The operation that you want to perform. Set the value to DescribeAlarms. |
|RegionId|String|Yes|cn-qingdao|The region ID of the event-triggered task. |
|ScalingGroupId|String|No|asg-bp18p2yfxow2dloq\*\*\*\*|The ID of the scaling group to be monitored by the event-triggered task. |
|AlarmTaskId|String|No|asg-bp1hvbnmkl10vll5\*\*\*\*\_f95ce797-dc2e-4bad-9618-14fee7d1\*\*\*\*|The ID of the event-triggered task. |
|State|String|No|OK|The status of the event-triggered task. Valid values:

-   ALARM: One or more alerts are triggered because the specified alert condition is met.
-   OK: No alert is triggered because the specified alert condition is not met.
-   INSUFFICIENT\_DATA: Auto Scaling cannot determine whether the specified alert condition is met because data is insufficient. |
|IsEnable|Boolean|No|true|Specifies whether the event-triggered task is enabled. Valid values:

-   true: The event-triggered task is enabled.
-   false: The event-triggered task is disabled. |
|MetricType|String|No|system|The type of the metric. Valid values:

-   system: the built-in metric of Cloud Monitor.
-   custom: the custom metric that is used to report relevant data of ECS instances to Cloud Monitor. |
|PageSize|Integer|No|10|The number of entries to return on each page. Maximum value: 50.

Default: 10. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default value: 1. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AlarmList|Array of Alarm| |The list of event-triggered tasks. |
|Alarm| | | |
|AlarmActions|List|ari:acs:ess:cn-hangzhou:1406926474\*\*\*\*:scalingrule/asr-bp163l21e07uh\*\*\*\*|The list of unique identifiers of the scaling rules that are associated with the event-triggered tasks. |
|AlarmTaskId|String|asg-bp1hvbnmkl10vll5\*\*\*\*\_f95ce797-dc2e-4bad-9618-14fee7d1\*\*\*\*|The ID of the event-triggered task. |
|ComparisonOperator|String|\>=|The operator for comparison between the collected metric value and the threshold. This parameter is used to specify the relationship between the metric value and the threshold that meets the alert condition. Valid values:

-   \>=: The metric value is greater than or equal to the threshold.
-   <=: The metric value is less than or equal to the threshold.
-   \>: The metric value is greater than the threshold.
-   <: The metric value is less than the threshold. |
|Description|String|Test alarm task.|The description of the event-triggered task. |
|Dimensions|Array of Dimension| |The dimensions that are associated with the metric. |
|Dimension| | | |
|DimensionKey|String|device|The key of the dimension that is associated with the metric. Valid values:

-   user\_id: the ID of your account.
-   scaling\_group: the scaling group that is monitored.
-   device: the type of the network interface controller \(NIC\).
-   state: indicates whether the total number of TCP connections or the number of TCP connections that have been established and are available is counted. |
|DimensionValue|String|eth0|The value of the dimension that is associated with the metric. The value of this parameter depends on the DimensionKey parameter.

When the value of DimensionKey is user\_id, the value of this parameter is set by the system.

When the value of DimensionKey is scaling\_group, the value of this parameter is set by the system.

When the value of DimensionKey is device, the valid values of this parameter are:

-   eth0: the internal network NIC for classic network-type ECS instances, and the only NIC for VPC-type ECS instances.
-   eth1: the public network NIC for classic network-type ECS instances.

When the value of DimensionKey is state, the valid values of this parameter are:

-   TCP\_TOTAL: indicates that the total number of TCP connections is counted.
-   ESTABLISHED: indicates that the number of TCP connections that have been established and are available is counted. |
|Effective|String|Test|**Note:** This parameter is in invitational preview and not available. |
|Enable|Boolean|true|Indicates whether the event-triggered task is enabled. Valid values:

-   true: The event-triggered task is enabled.
-   false: The event-triggered task is disabled. |
|EvaluationCount|Integer|3|The number of times that the alert condition must be met to trigger an alert and execute scaling rules. For example, if this parameter is set to 3, an alert is triggered when the average CPU utilization is greater than or equal to 80% for three times. |
|MetricName|String|CpuUtilization|The name of the metric. Valid values:

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
|MetricType|String|system|The type of the metric. Valid values:

-   system: the built-in metric of Cloud Monitor.
-   custom: the custom metric that is used to report relevant data of ECS instances to Cloud Monitor. |
|Name|String|TestAlarmTask|The name of the event-triggered task. |
|Period|Integer|300|The period for collecting the statistical value of the metric. Unit: seconds. Valid values:

-   60
-   120
-   300
-   900 |
|ScalingGroupId|String|asg-bp18p2yfxow2dloq\*\*\*\*|The ID of the scaling group that is monitored by the event-triggered task. |
|State|String|ALARM|The status of the event-triggered task. Valid values:

-   ALARM: One or more alerts are triggered because the specified alert condition is met.
-   OK: No alert is triggered because the specified alert condition is not met.
-   INSUFFICIENT\_DATA: Auto Scaling cannot determine whether the specified alert condition is met because data is insufficient. |
|Statistics|String|Average|The type of the statistical value that is collected for the metric. Valid values:

-   Average: the average value.
-   Minimum: the minimum value.
-   Maximum: the maximum value. |
|Threshold|Float|80|The threshold of the metric. The alert condition of the event-triggered task specifies the relationship between the statistical value and the threshold of the metric. When the alert condition is met for the specified number of times, Auto Scaling triggers an alert and executes the scaling rules specified in the event-triggered task. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|871C7C53-34A4-45AA-8C14-4B72FA6A\*\*\*\*|The ID of the request. |
|TotalCount|Integer|2|The total number of event-triggered tasks. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DescribeAlarms
&RegionId=cn-qingdao
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeAlarmsResponse>
  <PageNumber>1</PageNumber>
  <TotalCount>2</TotalCount>
  <PageSize>10</PageSize>
  <AlarmList>
    <Alarm>
      <Period>300</Period>
      <Statistics>Average</Statistics>
      <MetricType>system</MetricType>
      <EvaluationCount>3</EvaluationCount>
      <Name>asg-bp1hvbnmkl10vll5xtt2_f95ce797-dc2e-4bad-9618-14fee7d1****</Name>
      <AlarmTaskId>asg-bp1hvbnmkl10vll5xtt2_f95ce797-dc2e-4bad-9618-14fee7d1****</AlarmTaskId>
      <MetricName>MemoryUtilization</MetricName>
      <Threshold>55</Threshold>
      <State>INSUFFICIENT_DATA</State>
      <Enable>false</Enable>
      <ScalingGroupId>asg-bp1hvbnmkl10vll5****</ScalingGroupId>
      <Dimensions>
        <Dimension>
          <DimensionValue>asg-bp1hvbnmkl10vll5****</DimensionValue>
          <DimensionKey>scaling_group</DimensionKey>
        </Dimension>
        <Dimension>
          <DimensionValue>140692647406****</DimensionValue>
          <DimensionKey>userId</DimensionKey>
        </Dimension>
      </Dimensions>
      <ComparisonOperator>>=</ComparisonOperator>
    </Alarm>
    <Alarm>
      <Period>60</Period>
      <Description>DO NOT EDIT OR DELETE.For TargetTrackingScalingRule scalingRuleAri:ari:acs:ess:cn-hangzhou:140692647406****:scalingrule/asr-bp13jvr9iummzvgk****, scalingRuleName:****-target-tracking-scaling-rule</Description>
      <Statistics>Average</Statistics>
      <MetricType>system</MetricType>
      <EvaluationCount>15</EvaluationCount>
      <AlarmActions>
        <AlarmAction>ari:acs:ess:cn-hangzhou:140692647406****:scalingrule/asr-bp13jvr9iummzvgk****</AlarmAction>
      </AlarmActions>
      <Name>TargetTracking-asr-bp13jvr9iummzvgk****-AlarmLow-3f4730b9-c275-4527-b057-847fa883****</Name>
      <AlarmTaskId>asg-bp18p2yfxow2dloq****_48efb36a-c0b8-4173-b699-bd37c430****</AlarmTaskId>
      <MetricName>CpuUtilization</MetricName>
      <Threshold>56</Threshold>
      <State>ALARM</State>
      <Enable>true</Enable>
      <ScalingGroupId>asg-bp18p2yfxow2dloq****</ScalingGroupId>
      <Dimensions>
        <Dimension>
          <DimensionValue>asg-bp18p2yfxow2dloq****</DimensionValue>
          <DimensionKey>scaling_group</DimensionKey>
        </Dimension>
        <Dimension>
          <DimensionValue>140692647406****</DimensionValue>
          <DimensionKey>userId</DimensionKey>
        </Dimension>
      </Dimensions>
      <ComparisonOperator><</ComparisonOperator>
    </Alarm>
  </AlarmList>
  <RequestId>871C7C53-34A4-45AA-8C14-4B72FA6A****</RequestId>
</DescribeAlarmsResponse>
```

`JSON` format

```
{
    "PageNumber": 1,
    "TotalCount": 2,
    "PageSize": 10,
    "AlarmList": {
        "Alarm": [
            {
                "Period": 300,
                "Statistics": "Average",
                "MetricType": "system",
                "EvaluationCount": 3,
                "Name": "asg-bp1hvbnmkl10vll5xtt2_f95ce797-dc2e-4bad-9618-14fee7d1****",
                "AlarmTaskId": "asg-bp1hvbnmkl10vll5xtt2_f95ce797-dc2e-4bad-9618-14fee7d1****",
                "MetricName": "MemoryUtilization",
                "Threshold": 55,
                "State": "INSUFFICIENT_DATA",
                "Enable": false,
                "ScalingGroupId": "asg-bp1hvbnmkl10vll5****",
                "Dimensions": {
                    "Dimension": [
                        {
                            "DimensionValue": "asg-bp1hvbnmkl10vll5****",
                            "DimensionKey": "scaling_group"
                        },
                        {
                            "DimensionValue": "140692647406****",
                            "DimensionKey": "userId"
                        }
                    ]
                },
                "ComparisonOperator": ">="
            },
            {
                "Period": 60,
                "Description": "DO NOT EDIT OR DELETE.For TargetTrackingScalingRule scalingRuleAri:ari:acs:ess:cn-hangzhou:140692647406****:scalingrule/asr-bp13jvr9iummzvgk****, scalingRuleName:****-target-tracking-scaling-rule",
                "Statistics": "Average",
                "MetricType": "system",
                "EvaluationCount": 15,
                "AlarmActions": {
                    "AlarmAction": [
                        "ari:acs:ess:cn-hangzhou:140692647406****:scalingrule/asr-bp13jvr9iummzvgk****"
                    ]
                },
                "Name": "TargetTracking-asr-bp13jvr9iummzvgk****-AlarmLow-3f4730b9-c275-4527-b057-847fa883****",
                "AlarmTaskId": "asg-bp18p2yfxow2dloq****_48efb36a-c0b8-4173-b699-bd37c430****",
                "MetricName": "CpuUtilization",
                "Threshold": 56,
                "State": "ALARM",
                "Enable": true,
                "ScalingGroupId": "asg-bp18p2yfxow2dloq****",
                "Dimensions": {
                    "Dimension": [
                        {
                            "DimensionValue": "asg-bp18p2yfxow2dloq****",
                            "DimensionKey": "scaling_group"
                        },
                        {
                            "DimensionValue": "140692647406****",
                            "DimensionKey": "userId"
                        }
                    ]
                },
                "ComparisonOperator": "<"
            }
        ]
    },
    "RequestId": "871C7C53-34A4-45AA-8C14-4B72FA6A****"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

