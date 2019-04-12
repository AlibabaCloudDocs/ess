# ModifyScheduledTasksk {#concept_25958_zh .concept}

Modifies the attributes of a scheduled task.

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|Operation interface name, required parameter. Value: ModifyScheduledTask.|
|ScheduledTaskId|String|Yes|ID of the scheduled task.|
|ScheduledTaskName|String|No|Display name of the scheduled task, which must be 2-40 characters \(English or Chinese\) long. It must begin with a number, an upper/lower-case letter or a Chinese character and may contain numbers, “\_”, “-“ or “.”. The account name is unique in the same region. If this parameter is not specified, the default value ScheduledScalingTaskId is used.

 |
|Description|String|No|Description of the scheduled task, which is 2-200 characters \(English or Chinese\) long.|
|ScheduledAction|String|No|Operations performed when the scheduled task is triggered. Fill in the unique identifier of the scaling rule.|
|LaunchTime|String|No|Time point at which the scheduled task is triggered. The date format follows the ISO8601 standard and uses UTC time. It is in the format of YYYY-MM-DDThh:mmZ.

 If RecurrenceType is specified, the time point specified by this attribute is the default time point at which the circle is executed.

 If RecurrenceType is not specified, the task is executed once on the designated date and time.

 A time point 90 days after creation or modification cannot be entered.

 |
|LaunchExpirationTime|Integer|No|Time period within which the failed scheduled task is retried. The default value is 600s.

 Value range: \[0, 21600\]

 |
|RecurrenceType|String|No|Type of the scheduled task to be repeated. Optional values: -   Daily: Recurrence interval by day for a scheduled task.
-   Weekly: Recurrence interval by week for a scheduled task.
-   Monthly: Recurrence interval by month for a scheduled task.
-   Cron: Execute a scheduled task according to the specified Cron expression.

 After modification, RecurrenceType, RecurrenceValue and RecurrenceEndTime must be set simultaneously.

 |
|RecurrenceValue|String|No|Value of the scheduled task to be repeated. -   Daily: Only one value in the range \[1,31\] can be filled.
-   Weekly: Multiple values can be filled. The values of Sunday to Saturday are 0 to 6 in sequence. Multiple values shall be separated by commas \(,\).
-   Monthly: In the format of A-B. The value range of A and B is 1 to 31, and the B value must be greater than the A value.
-   Cron: An expression comprises of minute, hour, day, month and week. And the expression supports comma \(,\), hyphen \(-\), asterisk \(\*\) and slash \(/\).

 After modification, RecurrenceType, RecurrenceValue and RecurrenceEndTime must be set simultaneously.

 |
|RecurrenceEndTime|String|No|End time of the scheduled task to be repeated. The date format follows the ISO8601 standard and uses UTC time. It is in the format of YYYY-MM-DDThh:mmZ. A time point 90 days after creation or modification cannot be entered.

 After modification, RecurrenceType, RecurrenceValue and RecurrenceEndTime must be set simultaneously.

 |
|TaskEnabled|Bool|No|Whether to enable the scheduled task. -   When the parameter is set to true, the task is enabled.
-   When the parameter is set to false, the task is disabled.

 The default value is true.

 |

## Response parameters { .section}

Public parameters.

## Request example { .section}

```
http://ess.aliyuncs.com/?Action=ModifyScheduledTask
&ScheduledTaskId=edRtShc57WGXdt8TlPbrjsnV
&LaunchTime=2014-08-18T10:52Z
&RecurrenceEndTime=2014-08-20T16:55Z
&<Public Request Parameters>
```

## Response example { .section}

XML format:

```
<ModifyScheduledTaskResponse>
    <RequestId>F9372E8D-C163-471F-BEB4-3A02B3CE176E</RequestId>
</ModifyScheduledTaskResponse>
```

JSON format:

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## Error code { .section}

For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|Error code|Error message|HTTP status code|Description|
|:---------|:------------|:---------------|:----------|
|InvalidScheduledTaskId.NotFound|The specified scheduled task does not exist.|404|The specified scheduled task does not exist.|
|InvalidScheduledTaskName.Duplicate|The specified value of parameter `ScheduledTaskName` is duplicated.|400|The specified value of parameter <parameter name\> is duplicated.|
|ScheduledAction.RegionMismatch|The specified scheduled task and the specified scheduled action are not in the same Region.|400|The specified scheduled task and the specified scheduled action are not in the same Region.|

