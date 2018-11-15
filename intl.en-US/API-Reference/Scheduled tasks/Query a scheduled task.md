# Query a scheduled task {#concept_25959_zh .concept}

Queries information of a scheduled task.

You can use the ScheduledAction to query the relevant scheduled task.

## Request parameters {#section_ojj_t3l_sfb .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|Operation interface name, required parameter. Value: DescribeScheduledTasks.|
|RegionId|String|Yes|Region of the scheduled task.|
|ScheduledTaskId.N|String|No|ID of the scheduled task. You can enter at most 20 IDs. Invalid scheduled task IDs are not displayed in the query results, and no error is reported.|
|ScheduledTaskName.N|String|No|Display name of the schedules task. You can enter at most 20 display names. Names of invalid scheduled tasks will be neglected in the query results, and no error is reported.|
|ScheduledAction.N|String|No|Operations performed when the scheduled task is triggered. You can enter at most 20 operations. Invalid operations are not displayed in the query results, and no error is reported.|
|PageNumber|Integer|No|Page number of the scheduled task list, starting from 1. The default value is 1.|
|PageSize|Integer|No|When querying by page, this parameter indicates the number of lines per page. Maximum value: 50; default value: 10.|

## Response parameters {#section_xff_v3l_sfb .section}

|Name|Type|Description|
|:---|:---|:----------|
|TotalCount|Integer|Total number of scheduled tasks|
|PageNumber|Integer|Current page number|
|PageSize|Integer|Number of lines per page|
|ScheduledTasks|ScheduledTaskSetType|A set of scheduled task information|

ScheduledTaskSetType is a set of ScheduledTaskItemTypes.

|Name|Type|Description|
|:---|:---|:----------|
|ScheduledTask|ScheduledTaskItemType|Information of the scheduled task|

The attributes of the ScheduledTaskItemType are listed as follows.

|Name|Type|Description|
|:---|:---|:----------|
|ScheduledTaskId|String|ID of the scheduled task|
|ScheduledTaskName|String|Name of the scheduled task|
|Description|String|Description of the scheduled task|
|ScheduledAction|String|Operations performed when the scheduled task is triggered|
|LaunchTime|String|Time point at which the scheduled task is triggered|
|LaunchExpirationTime|Integer|Retry interval for the failed scheduled task|
|RecurrenceType|String|Type of the scheduled task to be repeated|
|RecurrenceValue|String|Value of the scheduled task to be repeated|
|RecurrenceEndTime|String|End time of the scheduled task to be repeated|
|TaskEnabled|Bool|Whether to enable the scheduled task|

## Error code {#section_jqh_1jl_sfb .section}

For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

## Request example {#section_w21_cjl_sfb .section}

```
http://ess.aliyuncs.com/?Action=DescribeScheduledTasks
&RegionId=cn-qingdao
&ScheduledTaskId. 1=edRtShc57WGXdt8TlPbrjsnV
&PageSize=50
Public Request Parameters
```

## Response example { .section}

XML format:

```
<DescribeScheduledTasksResponse>
<RequestId>B9B498DA-E836-45FF-83C7-1930492FDD5A</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>50</PageSize>
    <ScheduledTasks>
        <ScheduledTask>
            <Description/>
            <LaunchExpirationTime>600</LaunchExpirationTime>
            <LaunchTime>2014-08-18T10:52Z</LaunchTime>
            <RecurrenceEndTime>2014-08-20T16:55Z</RecurrenceEndTime>
            <RecurrenceType>Daily</RecurrenceType>
            <RecurrenceValue>1</RecurrenceValue>            
<ScheduledAction>
ari:acs:ess:cn-qingdao:1344371:scalingrule/cCBpdYdQuBe2cUxOdu6piOk
</ScheduledAction>
            <ScheduledTaskId>edRtShc57WGXdt8TlPbrjsnV</ScheduledTaskId>
            <ScheduledTaskName>edRtShc57WGXdt8TlPbrjsnV</ScheduledTaskName>
            <TaskEnabled>true</TaskEnabled>
        </ScheduledTask>
    </ScheduledTasks>
</DescribeScheduledTasksResponse>
```

JSON format:

```
{
  "RequestId": "43434132-91C4-4264-8343-681130760A5C",
"TotalCount": 1,
"PageSize": 1,
  "PageNumber": 1,
  "ScheduledTasks": {
    "ScheduledTask": [
      {
        "TaskEnabled": true,
        "ScheduledTaskId": "b27CLSc8T478c2iqHr6fqbF",
        "Description": "ditingshigechunqingchunan",
        "ScheduledTaskName": "9906a33f-14eb-42b8-8bdb-ee8cdf912706",
        "LaunchExpirationTime": 120,
        "RecurrenceType": "Daily",
        "RecurrenceEndTime": "2014-08-13T19:19Z",
        "LaunchTime": "2014-08-12T17:55Z",
        "RecurrenceValue": "1",
        "ScheduledAction": "ari:acs:ess:cn-qingdao:1344371:scalingrule/qGx9feK1giadmp3XKer94cD"
      }
    ]
  }
}
```

