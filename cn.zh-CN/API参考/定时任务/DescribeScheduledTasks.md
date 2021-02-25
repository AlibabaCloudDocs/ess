# DescribeScheduledTasks

调用DescribeScheduledTasks查询定时任务的信息。

## 接口说明

您可以通过定时任务的ID、定时任务的名称、定时任务执行的伸缩规则等查询定时任务。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DescribeScheduledTasks&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeScheduledTasks|系统规定参数。取值：DescribeScheduledTasks |
|RegionId|String|是|cn-qingdao|定时任务所属伸缩组的地域ID。 |
|PageNumber|Integer|否|1|定时任务列表的页码，起始值：1。

 默认值：1 |
|PageSize|Integer|否|50|分页查询时设置的每页行数，最大值：50。

 默认值：10 |
|ScheduledAction.N|RepeatList|否|ari:acs:ess:cn-hangzhou:1406926474\*\*\*\*:scalingrule/asr-bp1id5rhu8edp7kd\*\*\*\*|ScheduledAction.N为对应定时任务在触发时需要执行的操作，N的取值范围：1～20。 |
|ScheduledTaskId.N|RepeatList|否|edRtShc57WGXdt8TlPbr\*\*\*\*|ScheduledTaskId.N为待查询定时任务的ID，N的取值范围：1～20。 |
|ScheduledTaskName.N|RepeatList|否|scheduled\*\*\*\*|ScheduledTaskName.N为待查询定时任务的名称，N的取值范围：1～20。 |
|ScalingGroupId|String|否|asg-bp1bo5tca4m56nap\*\*\*\*|执行定时任务的伸缩组的ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|当前页码。 |
|PageSize|Integer|50|每页行数。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|ScheduledTasks|Array of ScheduledTask| |定时任务信息组成的集合。 |
|ScheduledTask| | | |
|Description|String|Test scheduled task.|定时任务的描述信息。 |
|DesiredCapacity|Integer|10|定时任务的伸缩方式为设置伸缩组内实例数量时，指定伸缩组内实例的期望实例数。 |
|LaunchExpirationTime|Integer|600|定时任务触发操作失败后，在此时间内重试。单位为秒，取值范围：0~21600。 |
|LaunchTime|String|2014-08-18T10:52Z|定时任务触发的时间点。 |
|MaxValue|Integer|10|定时任务的伸缩方式为设置伸缩组内实例数量时，指定伸缩组内实例的最大数量。 |
|MinValue|Integer|0|定时任务的伸缩方式为设置伸缩组内实例数量时，指定伸缩组内实例的最小数量。 |
|RecurrenceEndTime|String|2014-08-20T16:55Z|重复执行定时任务的结束时间。 |
|RecurrenceType|String|Daily|重复执行定时任务的类型。 |
|RecurrenceValue|String|1|重复执行定时任务的数值。 |
|ScalingGroupId|String|asg-bp1bo5tca4m56nap\*\*\*\*|定时任务触发时修改该伸缩组的实例数量，具体修改方式通过MinValue、MaxValue和DesiredCapacity指定。

 注意：`ScheduledAction`和`ScalingGroupId`不会同时存在。 |
|ScheduledAction|String|ari:acs:ess:cn-hangzhou:1406926474\*\*\*\*:scalingrule/asr-bp1id5rhu8edp7kd\*\*\*\*|定时任务触发时执行的伸缩规则。

 注意：`ScheduledAction`和`ScalingGroupId`不会同时存在。 |
|ScheduledTaskId|String|edRtShc57WGXdt8TlPbr\*\*\*\*|定时任务的ID。 |
|ScheduledTaskName|String|scheduled\*\*\*\*|定时任务的名称。 |
|TaskEnabled|Boolean|true|是否启动定时任务。 |
|TotalCount|Integer|1|定时任务总数。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=DescribeScheduledTasks
&RegionId=cn-qingdao
&ScheduledTaskId.1=edRtShc57WGXdt8TlPbr****
&PageSize=50
&<公共请求参数>
```

正常返回示例

`XML`格式

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

`JSON`格式

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

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

