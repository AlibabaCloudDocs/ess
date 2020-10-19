# CreateScheduledTask

You can call this operation to create a scheduled task.

## Description

When a scheduled task fails to be triggered because the scaling group is executing a scaling activity or the scaling group is disabled, the scheduled task will be retried for the duration of the launch expiration time. After the duration of the launch expiration time, a scheduled task that has failed to be triggered will be abandoned.

If multiple tasks are scheduled at similar points in time to execute scaling rules in the same group, the earliest task will execute its scaling activity first. Other tasks will make attempts to execute their rules during their launch expiration time, but only one scaling activity can be run in a scaling group at a time. If the previous scaling activity is completed while another scheduled task is making triggering attempts during its launch expiration time, Auto Scaling executes the scaling rule that is triggered by the scheduled task and then triggers the corresponding scaling activity.

A scheduled task supports the following scaling methods:

-   You can set the ScheduledAction parameter to specify the scaling rule to be executed.
-   You can set the ScalingGroupId parameter to specify the number of instances in a scaling group.

**Note:** You cannot set ScheduledAction and ScalingGroupId at the same time.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=CreateScheduledTask&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateScheduledTask|The operation that you want to perform. Set the value to CreateScheduledTask. |
|RegionId|String|Yes|cn-qingdao|The region ID of the scheduled task. |
|ScheduledTaskName|String|No|scheduled\*\*\*\*|The display name of the scheduled task. The name must be 2 to 64 characters in length and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a letter or digit. The name of the scheduled task must be unique within the same region for the same Alibaba Cloud account.

The default value is the value of the ScheduledTaskId parameter. |
|Description|String|No|Test scheduled task.|The description of the scheduled task. The description must be 2 to 200 characters in length. |
|ScheduledAction|String|No|ari:acs:ess:cn-hangzhou:140692647\*\*\*\*:scalingrule/asr-bp12tcnol686y1ik\*\*\*\*|The operation to be executed when the scheduled task is triggered. Specify the unique identifier of the scaling rule. After the ScheduledAction parameter is specified, the scaling method of the scheduled task is to select an existing scaling rule.

**Note:** You cannot set ScheduledAction and ScalingGroupId at the same time. |
|RecurrenceEndTime|String|No|2014-08-17T16:55Z|The end time of the scheduled task to be repeated. Specify the time in the ISO 8601 standard in the YYYY-MM-DDThh:mmZ format.

The time must be in UTC. You cannot enter a time point later than 365 days from the scheduled task creation. |
|LaunchTime|String|No|2014-08-17T16:52Z|The time at which the scheduled task is triggered. Specify the time in the ISO 8601 standard in the YYYY-MM-DDThh:mmZ format. The time must be in UTC. You cannot enter a time point later than 90 days from the scheduled task creation.

If the RecurrenceType parameter is specified, the task is executed each day at the time specified by LaunchTime.

If the RecurrenceType parameter is not specified, the task is executed only once at the time specified by LaunchTime. |
|RecurrenceType|String|No|Daily|The interval that a scheduled task is repeated at. Valid values:

-   Daily: The scheduled task is executed once every specified number of days.
-   Weekly: The scheduled task is executed on each specified day of a week.
-   Monthly: The scheduled task is executed on each specified day of a month.
-   Cron: The scheduled task is executed based on the specified cron expression.

You must specify RecurrenceType and RecurrenceValue at the same time. |
|RecurrenceValue|String|No|1|The recurrence value of the scheduled task to be repeated.

-   Daily: If you set RecurrenceType to Daily, you can specify only one value. Valid values: 1 to 31.
-   Weekly: If you set RecurrenceType to Weekly, you can specify multiple values and separate them with commas \(,\). For example, the values of Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, and Saturday are 0, 1, 2, 3, 4, 5, and 6.
-   Monthly: If you set RecurrenceType to Monthly, you can specify two values in the A-B format. Valid values: 1 to 31. B must be greater than or equal to A.
-   Cron: If you set RecurrenceType to Cron, you can specify a cron expression. A cron expression is written in UTC time and consists of five fields: minute, hour, day of month \(date\), month, and day of week. The expression can contain wildcard characters including commas \(,\), question marks \(?\), hyphens \(-\), asterisks \(\*\), number signs \(\#\), forward slashes \(/\), and the L and W letters.

You must specify RecurrenceType and RecurrenceValue at the same time. |
|TaskEnabled|Boolean|No|true|Specifies whether to start the scheduled task.

-   true: starts the scheduled task.
-   false: stops the scheduled task.

Default value: true. |
|LaunchExpirationTime|Integer|No|600|The time period during which the failed scheduled task is retried. Unit: seconds. Valid values: 0 to 21600.

Default value: 600. |
|MinValue|Integer|No|0|The minimum number of instances in a scaling group when the scaling method of the scheduled task is to specify the number of instances in a scaling group. |
|MaxValue|Integer|No|10|The maximum number of instances in a scaling group when the scaling method of the scheduled task is to specify the number of instances in a scaling group. |
|DesiredCapacity|Integer|No|10|The expected number of instances in a scaling group when the scaling method of the scheduled task is to specify the number of instances in a scaling group.

**Note:** You must specify the DesiredCapacity parameter when you create the scaling group. |
|ScalingGroupId|String|No|asg-bp18p2yfxow2dloq\*\*\*\*|The ID of the scaling group whose number of instances is modified when the scheduled task is triggered. After the ScalingGroupId parameter is specified, the scaling method of the scheduled task is to specify the number of instance in a scaling group. You must specify at least one of the MinValue, MaxValue, and DesiredCapacity parameters.

**Note:** You cannot set ScheduledAction and ScalingGroupId at the same time. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3\*\*\*\*|The ID of the request. |
|ScheduledTaskId|String|edRtShc57WGXdt8TlPbr\*\*\*\*|The globally unique ID of the scheduled task generated by the system. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=CreateScheduledTask
&RegionId=cn-qingdao
&LaunchTime=2014-08-17T16:52Z
&RecurrenceType=Daily
&RecurrenceValue=1
&RecurrenceEndTime=2014-08-17T16:55Z
&ScheduledAction=ari:acs:ess:cn-hangzhou:140692647****:scalingrule/asr-bp12tcnol686y1ik****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateScheduledTaskResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3****</RequestId>
      <ScheduledTaskId>edRtShc57WGXdt8TlPbr****</ScheduledTaskId>
</CreateScheduledTaskResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3****",
    "ScheduledTaskId": "edRtShc57WGXdt8TlPbr****"
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

|InvalidRegionId.NotFound

|The specified region does not exist.

|The error message returned because the specified region does not exist. |
|400

|InvalidScheduledTaskName.Duplicate

|The specified value of parameter ScheduledTaskName is duplicated.

|The error message returned because the name of the scheduled task already exists. |
|400

|QuotaExceeded.ScheduledTask

|Scheduled task quota exceeded.

|The error message returned because the maximum number of scheduled tasks that can be created has been reached. |
|400

|ScheduledAction.RegionMismatch

|The specified scheduled task and the specified scheduled action are not in the same Region.

|The error message returned because the specified scaling rule and the scheduled task are not in the same region. |

