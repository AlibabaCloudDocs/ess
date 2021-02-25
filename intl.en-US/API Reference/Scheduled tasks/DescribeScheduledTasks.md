# DescribeScheduledTasks

You can call this operation to query scheduled tasks.

## Description

You can query scheduled tasks based on the scaling rules that are executed by scheduled tasks, the IDs and names of scheduled tasks.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeScheduledTasks&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeScheduledTasks|The operation that you want to perform. Set the value to DescribeScheduledTasks. |
|RegionId|String|Yes|cn-qingdao|The region ID of the scaling group to which a scheduled task belongs. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default: 1. |
|PageSize|Integer|No|50|The number of entries to return on each page. Maximum value: 50.

Default value: 10. |
|ScheduledAction.N|String|No|ari:acs:ess:cn-hangzhou:1406926474\*\*\*\*:scalingrule/asr-bp1id5rhu8edp7kd\*\*\*\*|The operation to be performed when scheduled task N is triggered. Valid values of N: 1 to 20. |
|ScheduledTaskId.N|String|No|edRtShc57WGXdt8TlPbr\*\*\*\*|The ID of scheduled task N to be queried. Valid values of N: 1 to 20. |
|ScheduledTaskName.N|String|No|scheduled\*\*\*\*|The name of scheduled task N to be queried. Valid values of N: 1 to 20. |
|ScalingGroupId|String|No|asg-bp1bo5tca4m56nap\*\*\*\*|The ID of the scaling group in which the scheduled task is to be executed. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|50|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|ScheduledTasks|Array of ScheduledTask| |Details about scheduled tasks. |
|ScheduledTask| | | |
|Description|String|Test scheduled task.|The description of the scheduled task. |
|DesiredCapacity|Integer|10|The expected number of instances in the scaling group when the scaling method of the scheduled task is to specify the number of instances in the scaling group. |
|LaunchExpirationTime|Integer|600|The time period during which the failed scheduled task is retried. Unit: seconds. Valid values: 0 to 21600. |
|LaunchTime|String|2014-08-18T10:52Z|The point in time at which the scheduled task was triggered. |
|MaxValue|Integer|10|The maximum number of instances in the scaling group when the scaling method of the scheduled task is to specify the number of instances in the scaling group. |
|MinValue|Integer|0|The minimum number of instances in the scaling group when the scaling method of the scheduled task is to specify the number of instances in a scaling group. |
|RecurrenceEndTime|String|2014-08-20T16:55Z|The end time of the repeated scheduled task. |
|RecurrenceType|String|Daily|The interval at which the scheduled task was repeated. |
|RecurrenceValue|String|1|The number of recurrences of the scheduled task. |
|ScalingGroupId|String|asg-bp1bo5tca4m56nap\*\*\*\*|The ID of the scaling group where the number of instances is modified when the scheduled task is triggered. You can modify the number of instances by specifying the following parameters: MinValue, MaxValue, and DesiredCapacity.

Note: You cannot specify `ScheduledAction` and `ScalingGroupId` at the same time. |
|ScheduledAction|String|ari:acs:ess:cn-hangzhou:1406926474\*\*\*\*:scalingrule/asr-bp1id5rhu8edp7kd\*\*\*\*|The scaling rule that was executed when the scheduled task was triggered.

Note: You cannot specify `ScheduledAction` and `ScalingGroupId` at the same time. |
|ScheduledTaskId|String|edRtShc57WGXdt8TlPbr\*\*\*\*|The ID of the scheduled task. |
|ScheduledTaskName|String|scheduled\*\*\*\*|The name of the scheduled task. |
|TaskEnabled|Boolean|true|Indicates whether the scheduled task is enabled. |
|TotalCount|Integer|1|The total number of scheduled tasks. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DescribeScheduledTasks
&RegionId=cn-qingdao
&ScheduledTaskId.1=edRtShc57WGXdt8TlPbr****
&PageSize=50
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeScheduledTasksResponse>
      <ScheduledTasks>
            <ScheduledTask>
                  <LaunchExpirationTime>600</LaunchExpirationTime>
                  <RecurrenceType>Daily</RecurrenceType>
                  <RecurrenceEndTime>2020-03-02T00:00Z</RecurrenceEndTime>
                  <ScalingGroupId>asg-bp1bo5tca4m56nap****</ScalingGroupId>
                  <TaskEnabled>false</TaskEnabled>
                  <ScheduledTaskName>scheduled****</ScheduledTaskName>
                  <MaxValue>1</MaxValue>
                  <LaunchTime>2020-03-01T00:00Z</LaunchTime>
                  <ScheduledTaskId>cV0bJbAXpipdbFI1NbM****</ScheduledTaskId>
                  <RecurrenceValue>31</RecurrenceValue>
            </ScheduledTask>
            <ScheduledTask>
                  <LaunchExpirationTime>600</LaunchExpirationTime>
                  <MinValue>1</MinValue>
                  <RecurrenceType>Daily</RecurrenceType>
                  <RecurrenceEndTime>2020-02-27T00:00Z</RecurrenceEndTime>
                  <ScalingGroupId>asg-bp1bo5tca4m56nap****</ScalingGroupId>
                  <TaskEnabled>true</TaskEnabled>
                  <ScheduledTaskName>scheduled****</ScheduledTaskName>
                  <LaunchTime>2020-02-26T00:00Z</LaunchTime>
                  <ScheduledTaskId>cD3G3pesE65NcSTmkld1****</ScheduledTaskId>
                  <RecurrenceValue>31</RecurrenceValue>
            </ScheduledTask>
      </ScheduledTasks>
      <PageNumber>1</PageNumber>
      <TotalCount>34</TotalCount>
      <PageSize>10</PageSize>
      <RequestId>4CF33369-7318-4BD5-BE1C-A776BA2C6627</RequestId>
</DescribeScheduledTasksResponse>
```

`JSON` format

```
{
    "ScheduledTasks": {
        "ScheduledTask": [
            {
                "LaunchExpirationTime": 600,
                "RecurrenceType": "Daily",
                "RecurrenceEndTime": "2020-03-02T00:00Z",
                "ScalingGroupId": "asg-bp1bo5tca4m56nap****",
                "TaskEnabled": false,
                "ScheduledTaskName": "scheduled****",
                "MaxValue": 1,
                "LaunchTime": "2020-03-01T00:00Z",
                "ScheduledTaskId": "cV0bJbAXpipdbFI1NbM****",
                "RecurrenceValue": "31"
            },
            {
                "LaunchExpirationTime": 600,
                "MinValue": 1,
                "RecurrenceType": "Daily",
                "RecurrenceEndTime": "2020-02-27T00:00Z",
                "ScalingGroupId": "asg-bp1bo5tca4m56nap****",
                "TaskEnabled": true,
                "ScheduledTaskName": "scheduled****",
                "LaunchTime": "2020-02-26T00:00Z",
                "ScheduledTaskId": "cD3G3pesE65NcSTmkld1****",
                "RecurrenceValue": "31"
            }
        ]
    },
    "PageNumber": 1,
    "TotalCount": 34,
    "PageSize": 10,
    "RequestId": "4CF33369-7318-4BD5-BE1C-A776BA2C6627"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

