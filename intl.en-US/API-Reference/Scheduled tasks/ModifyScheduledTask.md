# ModifyScheduledTask {#doc_api_Ess_ModifyScheduledTask .reference}

You can call this operation to modify the attributes of a scheduled task.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=ModifyScheduledTask) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|ScheduledTaskId|String|Yes|edRtShc57WGXdt8TlPbr\*\*\*\*| The ID of the scheduled task for which you want to modify attributes.

 |
|Action|String|No|ModifyScheduledTask| The operation that you want to perform. Set the value to ModifyScheduledTask.

 |
|Description|String|No|fortest| The description of the scheduled task. The description must be 2 to 200 characters in length.

 |
|LaunchExpirationTime|Integer|No|600| The period of time for which the scheduled task is retried if it fails. Default value: 600. Unit: seconds.

 Valid values: 0 to 21600.

 |
|LaunchTime|String|No|2014-08-18T10:52Z| The time at which the scheduled task is triggered. The time follows the ISO 8601 standard and uses UTC time. The format is YYYY-MM-DDThh:mmZ.

 If the RecurrenceType parameter is specified, the task is executed each day at the time specified by LaunchTime.

 If the RecurrenceType parameter is not specified, the task is only executed once at the time specified by LaunchTime. You cannot enter a point in time later than 90 days from the date of scheduled task creation or modification.

 |
|RecurrenceEndTime|String|No|2014-08-20T16:55Z| The end time after which the scheduled task is no longer repeated. The time follows the ISO 8601 standard and uses UTC time. The format is YYYY-MM-DDThh:mmZ.

 You cannot enter a point in time later than 90 days from the date of scheduled task creation or modification.

 If you set RecurrenceEndTime, you must also set both RecurrenceType and RecurrenceValue.

 |
|RecurrenceType|String|No|Daily| Indicates the interval for which the scheduled task is repeated. Valid values:

 -   Daily: The scheduled task is executed recurrently after the specified number of days.
-   Weekly: The scheduled task is executed on each specified day of a week.
-   Monthly: The scheduled task is executed on each specified day of a month.
-   Cron: The scheduled task is executed recurrently based on the specified Cron expression.

 If you set RecurrenceType, you must also set both RecurrenceValue and RecurrenceEndTime.

 |
|RecurrenceValue|String|No|2| Indicates how often the scheduled task recurs.

 -   Daily: indicates the interval of days at which the scheduled task is repeated. You can enter a single value ranging from 1 to 31.
-   Weekly: indicates which days of the week that the scheduled task is repeated on. The values 0 to 6 correspond to the days of the week in sequence from Sunday to Saturday. Multiple values must be separated by commas \(,\).
-   Monthly: indicates which days of the month that the scheduled task is repeated on. You can enter two values ranging from 1 to 31. The format is A-B. B must be greater than or equal to A.
-   Cron: indicates a user-defined Cron expression that determines when the scheduled task is repeated. A Cron expression is written in UTC time and consists of five fields: minute, hour, day of month \(date\), month, and day of week. The expression can contain wildcard characters including commas \(,\), question marks \(?\), hyphens \(-\), asterisks \(\*\), number signs \(\#\), and forward slashes \(/\).

 If you set RecurrenceValue, you must also set both RecurrenceType and RecurrenceEndTime.

 |
|ScheduledAction|String|No|ari:acs:ess:cn-qingdao:1344371:scalingRule/cCBpdYdQuBe2cUxOdu6piOk| The operations performed when the scheduled task is triggered. When you set this parameter, you must also enter the unique identifier of the scaling rule.

 |
|ScheduledTaskName|String|No|test| The display name of the scheduled task. The name must be 2 to 64 characters in length and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a letter or digit. The name of the scheduled task must be unique to an Alibaba Cloud account in a region. The default name is the ID of the scheduled scaling task.

 |
|TaskEnabled|Boolean|No|true| Indicates whether to enable the scheduled task.

 -   When the parameter is set to true, the task is enabled.
-   When the parameter is set to false, the task is disabled.

 Default value: true.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=ModifyScheduledTask
&ScheduledTaskId=edRtShc57WGXdt8TlPbr****
&LaunchTime=2014-08-18T10:52Z
&RecurrenceEndTime=2014-08-20T16:55Z 
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyScheduledTaskResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</ModifyScheduledTaskResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes {#section_f6v_cqj_610 .section}

[View error codes](https://error-center.aliyun.com/status/product/Ess)

| HTTP status code

 | Error code

 | Error message

 | Description

 |
|--------------------|--------------|-----------------|---------------|
| 404

 | InvalidScheduledTaskId.NotFound

 | The specified scheduled task does not exist.

 | The error message returned when the specified scheduled task does not exist in the current account.

 |
| 400

 | InvalidScheduledTaskName.Duplicate

 | The specified value of parameter

 `ScheduledTaskName` is duplicated.

 | The error message returned when the specified name of the scheduled task already exists.

 |
| 400

 | ScheduledAction.RegionMismatch

 | The specified scheduled task and the specified scheduled action are not in the same Region.

 | The error message returned when the specified value of the ScheduledAction parameter and the specified scheduled task are not in the same region.

 |

