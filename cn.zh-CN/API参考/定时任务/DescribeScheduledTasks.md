# DescribeScheduledTasks {#doc_api_Ess_DescribeScheduledTasks .reference}

调用DescribeScheduledTasks查询定时任务的信息。

## 接口说明 {#description .section}

您可以通过定时触发的操作（ScheduledAction）查询关联的定时任务。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DescribeScheduledTasks&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-qingdao|定时任务所属伸缩组的地域ID。

 |
|Action|String|否|DescribeScheduledTasks|系统规定参数，取值：DescribeScheduledTasks。

 |
|PageNumber|Integer|否|1|定时任务列表的页码，起始值：1。

 默认值：1。

 |
|PageSize|Integer|否|50|分页查询时设置的每页行数，最大值：50。

 默认值：10。

 |
|ScheduledAction.1|String|否|ari:acs:ess:cn-qingdao:1344371:scalingrule/cCBpdYdQuBe2cUxOdu6piOk|ScheduledAction.N为对应定时任务在触发时需要执行的操作，N的取值范围：1～20。

 |
|ScheduledTaskId.1|String|否|edRtShc57WGXdt8TlPbr\*\*\*\*|ScheduledTaskId.N为待查询定时任务的ID，N的取值范围：1～20。

 |
|ScheduledTaskName.1|String|否|edRtShc57WGXdt8TlPbr\*\*\*\*|ScheduledTaskName.N为待查询定时任务的名称，N的取值范围：1～20。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|当前页码。

 |
|PageSize|Integer|50|每页行数。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |
|ScheduledTasks| | |定时任务信息组成的集合。

 |
|Description|String|fortest|定时任务的描述信息。

 |
|LaunchExpirationTime|Integer|600|定时任务触发操作失败后，在此时间内重试。单位为秒，取值范围：0~21600。

 |
|LaunchTime|String|2014-08-18T10:52Z|定时任务触发的时间点。

 |
|MaxValue|Integer|5|预测型伸缩规则产生的定时任务中的MinValue，执行该定时任务时会修改伸缩组的MinValue。

 |
|MinValue|Integer|1|预测型伸缩规则产生的定时任务中的MaxValue，执行该定时任务时会修改伸缩组的MaxValue。

 |
|RecurrenceEndTime|String|2014-08-20T16:55Z|重复执行定时任务的结束时间。

 |
|RecurrenceType|String|Daily|重复执行定时任务的类型。

 |
|RecurrenceValue|String|1|重复执行定时任务的数值。

 |
|ScheduledAction|String|ari:acs:ess:cn-qingdao:1344371:scalingrule/cCBpdYdQuBe2cUxOdu6\*\*\*\*|定时任务触发时需要执行的操作。

 |
|ScheduledTaskId|String|edRtShc57WGXdt8TlPbr\*\*\*\*|定时任务的ID。

 |
|ScheduledTaskName|String|edRtShc57WGXdt8TlPbr\*\*\*\*|定时任务的名称。

 |
|TaskEnabled|Boolean|true|是否启动定时任务。

 |
|TotalCount|Integer|1|定时任务总数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DescribeScheduledTasks
&RegionId=cn-qingdao
&ScheduledTaskId.1=edRtShc57WGXdt8TlPbr****
&PageSize=50
&<公共请求参数>

```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

