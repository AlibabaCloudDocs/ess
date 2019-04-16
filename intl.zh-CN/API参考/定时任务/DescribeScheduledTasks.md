# DescribeScheduledTasks {#concept_25959_zh .concept}

查询定时任务的信息。

## 描述 {#section_m5v_bdv_lgb .section}

查询时可以指定定时触发的操作（ScheduledAction）来查询关联的定时任务。

## 请求参数 {#section_ojj_t3l_sfb .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：DescribeScheduledTasks。|
|RegionId|String|是|定时任务所属的region。|
|ScheduledTaskId.N|String|否|定时任务的ID，最多可以输入20个。查询结果会忽略失效的定时任务ID，并且不报错。|
|ScheduledTaskName.N|String|否|定时任务的显示名称，最多可以输入20个。查询结果会忽略失效的定时任务名称，并且不报错。|
|ScheduledAction.N|String|否|定时任务触发时需要执行的操作，最多可以输入20个。查询结果会忽略失效的操作，并且不报错。|
|PageNumber|Integer|否|定时任务列表的页码，起始值为1，默认值为1。|
|PageSize|Integer|否|分页查询时设置的每页行数，最大值50行，默认值为10。|

## 返回参数 {#section_xff_v3l_sfb .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|定时任务总数。|
|PageNumber|Integer|当前页码。|
|PageSize|Integer|每页行数。|
|ScheduledTasks|ScheduledTaskSetType|定时任务信息组成的集合。|

ScheduledTaskSetType是由ScheduledTaskItemType类型组成的集合。

|名称|类型|描述|
|:-|:-|:-|
|ScheduledTask|ScheduledTaskItemType|定时任务信息。|

ScheduledTaskItemType类型的属性如下表所示。

|名称|类型|描述|
|:-|:-|:-|
|ScheduledTaskId|String|定时任务ID。|
|ScheduledTaskName|String|定时任务名称。|
|Description|String|定时任务的描述信息。|
|ScheduledAction|String|定时任务触发时需要执行的操作。|
|LaunchTime|String|定时任务触发的时间点。|
|LaunchExpirationTime|Integer|定时任务触发操作失败后，在此时间内重试。|
|RecurrenceType|String|重复执行定时任务的类型。|
|RecurrenceValue|String|重复执行定时任务的数值。|
|RecurrenceEndTime|String|重复执行定时任务的结束时间。|
|TaskEnabled|Bool|是否启动定时任务。|

## 示例 {#section_w21_cjl_sfb .section}

请求示例

```
http://ess.aliyuncs.com/?Action=DescribeScheduledTasks
&RegionId=cn-qingdao
&ScheduledTaskId.1=edRtShc57WGXdt8TlPbrjsnV
&PageSize=50
&<公共请求参数>
```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码 {#section_jqh_1jl_sfb .section}

对于所有接口的通用性错误，请参考 [客户端错误](intl.zh-CN/API参考/错误代码/客户端错误.md#) 或 [服务器端错误](intl.zh-CN/API参考/错误代码/服务器端错误.md#)。

