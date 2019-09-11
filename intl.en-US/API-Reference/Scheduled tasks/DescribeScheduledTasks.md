# DescribeScheduledTasks {#doc_api_Ess_DescribeScheduledTasks .reference}

You can call this operation to query scheduled tasks.

## Description {#description .section}

You can query relevant scheduled tasks by specifying the ScheduledAction parameter.

## Debugging {#api_explorer .section}

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeScheduledTasks&type=RPC&version=2014-08-28)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|RegionId|String|Yes|cn-qingdao|The region ID of the scaling group to which a scheduled task belongs.

 |
|Action|String|No|DescribeScheduledTasks|The operation that you want to perform. Set the value to DescribeScheduledTasks.

 |
|PageNumber|Integer|No|1|The page number of the scheduled task list to return. Pages start from page 1.

 Default value: 1.

 |
|PageSize|Integer|No|50|The number of entries to return on each page. Maximum value: 50.

 Default value: 10.

 |
|ScheduledAction.1|String|No|ari:acs:ess:cn-qingdao:1344371:scalingrule/cCBpdYdQuBe2cUxOdu6piOk|The operation to be performed when scheduled task N is triggered. Valid values of N: 1 to 20.

 |
|ScheduledTaskId.1|String|No|edRtShc57WGXdt8TlPbr\*\*\*\*|The ID of scheduled task N to be queried. Valid values of N: 1 to 20.

 |
|ScheduledTaskName.1|String|No|edRtShc57WGXdt8TlPbr\*\*\*\*|The name of scheduled task N to be queried. Valid values of N: 1 to 20.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The current page number.

 |
|PageSize|Integer|50|The number of entries returned on each page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request.

 |
|ScheduledTasks| | |The set of scheduled tasks.

 |
|Description|String|fortest|The description of the scheduled task.

 |
|LaunchExpirationTime|Integer|600|The time period during which the failed scheduled task is retried. Unit: seconds. Valid values: 0 to 21600.

 |
|LaunchTime|String|2014-08-18T10:52Z|The time when the scheduled task was triggered.

 |
|MaxValue|Integer|5|The MaxValue specified in the scheduled task that was created by the predictive scaling rule. The MaxValue of the scaling group is modified when the scheduled task is executed.

 |
|MinValue|Integer|1|The MinValue specified in the scheduled task that was created by the predictive scaling rule. The MinValue of the scaling group is modified when the scheduled task is executed.

 |
|RecurrenceEndTime|String|2014-08-20T16:55Z|The end time after which the scheduled task is no longer repeated.

 |
|RecurrenceType|String|Daily|Indicates the interval that a scheduled task is repeated at.

 |
|RecurrenceValue|String|1|Indicates how often the scheduled task recurs.

 |
|ScheduledAction|String|ari:acs:ess:cn-qingdao:1344371:scalingrule/cCBpdYdQuBe2cUxOdu6\*\*\*\*|The operation performed when a scheduled task is triggered.

 |
|ScheduledTaskId|String|edRtShc57WGXdt8TlPbr\*\*\*\*|The ID of the scheduled task.

 |
|ScheduledTaskName|String|edRtShc57WGXdt8TlPbr\*\*\*\*|The name of the scheduled task.

 |
|TaskEnabled|Boolean|true|Indicates whether the scheduled task is enabled.

 |
|TotalCount|Integer|1|The total number of scheduled tasks.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DescribeScheduledTasks
&RegionId=cn-qingdao
&ScheduledTaskId.1=edRtShc57WGXdt8TlPbr****
&PageSize=50
&<Common request parameters>

```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
<DescribeScheduledTasksResponse>
    <RequestId>43434132-91C4-4264-8343-681130760A5C</RequestId>
    <TotalCount>1</TotalCount>
    <PageSize>50</PageSize>
    <PageNumber>1</PageNumber>
    <ScheduledTasks>
        <ScheduledTask>
            <TaskEnabled>true</TaskEnabled>
            <ScheduledTaskId>b27CLSc8T478c2iqHr6****</ScheduledTaskId>
            <Description>Scheduled task test</Description>
            <ScheduledTaskName>edRtShc57WGXdt8TlPbr****</ScheduledTaskName>
            <LaunchExpirationTime>120</LaunchExpirationTime>
            <RecurrenceType>Daily</RecurrenceType>
            <RecurrenceEndTime>2014-08-13T19:19Z</RecurrenceEndTime>
            <LaunchTime>2014-08-12T17:55Z</LaunchTime>
            <RecurrenceValue>1</RecurrenceValue>
            <ScheduledAction>ari:acs:ess:cn-qingdao:1344371:scalingrule/qGx9feK1giadmp3XKer****</ScheduledAction>
        </ScheduledTask>
    </ScheduledTasks>
</DescribeScheduledTasksResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"ScheduledTasks":{
		"ScheduledTask":[
			{
				"LaunchExpirationTime":120,
				"Description":"Scheduled task test",
				"RecurrenceEndTime":"2014-08-13T19:19Z",
				"RecurrenceType":"Daily",
				"TaskEnabled":true,
				"ScheduledAction":"ari:acs:ess:cn-qingdao:1344371:scalingrule/qGx9feK1giadmp3XKer****",
				"ScheduledTaskName":"edRtShc57WGXdt8TlPbr****",
				"LaunchTime":"2014-08-12T17:55Z",
				"ScheduledTaskId":"b27CLSc8T478c2iqHr6****",
				"RecurrenceValue":"1"
			}
		]
	},
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":50,
	"RequestId":"43434132-91C4-4264-8343-681130760A5C"
}
```

## Error codes { .section}

