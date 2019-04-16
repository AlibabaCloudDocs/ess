# DescribeScalingActivities {#concept_25961_zh .concept}

本文介绍查询伸缩活动API操作。

## 描述 {#section_ard_kck_sfb .section}

查询伸缩活动的信息。

-   查询时可以指定伸缩组 ID 来查询该伸缩组下的所有伸缩活动。
-   查询时可以通过伸缩活动的状态来过滤查询结果。
-   可以查询 30 日内的伸缩活动。

## 请求参数 { .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：DescribeScalingActivities。|
|RegionId|String|是|伸缩活动所在的地域。|
|ScalingGroupId|String|否|伸缩组的 ID。|
|ScalingActivityId.N|String|否|伸缩活动的 ID，最多可以输入 10 个。返回查询结果时忽略失效的伸缩活动 ID，并且不报错。

|
|StatusCode|String|否|伸缩活动的状态。可选值：-   Successful：执行成功的伸缩活动。
-   Warning：部分执行成功的伸缩活动。
-   Failed：执行失败的伸缩活动。
-   InProgress：正在执行的伸缩活动。
-   Rejected：执行伸缩活动请求被拒绝。

|
|PageNumber|Integer|否|伸缩活动列表的页码，起始值为 1，默认值为 1 。|
|PageSize|Integer|否|分页查询时设置的每页行数，最大值 50 行，默认值为 10 。|

## 返回参数 { .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|伸缩活动总数。|
|PageNumber|Integer|当前页码。|
|PageSize|Integer|每页行数。|
|ScalingActivities|ScalingActivitySetType|伸缩活动信息组成的集合。|

ScalingActivities 是由 ScalingActivityItemType 类型组成的集合。

|名称|类型|描述|
|:-|:-|:-|
|ScalingActivity|ScalingActivityItemType|伸缩活动信息。|

ScalingActivityItemType 类型的属性如下表所示。

|名称|类型|描述|
|:-|:-|:-|
|ScalingActivityId|String|伸缩活动的 ID。|
|ScalingGroupId|String|伸缩组的 ID。|
|Description|String|伸缩活动的描述信息。|
|Cause|String|触发伸缩活动的原因。|
|StartTime|String|伸缩活动的开始时间。|
|EndTime|String|伸缩活动的结束时间。|
|Progress|Integer|伸缩活动的运行进度。|
|StatusCode|String|伸缩活动的当前状态。|
|StatusMessage|String|伸缩活动的状态信息。|

## 示例 { .section}

请求示例

```
http://ess.aliyuncs.com/?Action=DescribeScalingActivities
&RegionId=cn-qingdao
&PageSize=50
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeScalingActivitiesResponse>
    <RequestId>8FAAE99E-EB43-4838-85AD-93F62454904C</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <ScalingActivities>
        <ScalingActivity>
            <Cause>A scheduled task excuete scaling rule "srtest"，changing the Total Capacity from "0" to "1".</Cause>
            <Description>Add "1" ECS instance</Description>
            <EndTime>2014-08-17T12:39Z</EndTime>
            <Progress>100</Progress>
            <ScalingActivityId>ebta5WbUzC8gcwUWvfchyT4U</ScalingActivityId>
            <ScalingGroupId>AG6CQdPU8OKdwLjgZcJ2eaQ</ScalingGroupId>
            <StartTime>2014-08-17T12:39Z</StartTime>
            <StatusCode>Successful</StatusCode>
            <StatusMessage>"1" ECS instances is added. </StatusMessage>
        </ScalingActivity>
    </ScalingActivities>
</DescribeScalingActivitiesResponse>
```

`JSON` 格式

```
{
"RequestId":"0A016AD6-A91F-4210-9DEE-D5BBD4270F45",
"TotalCount":2582,
"PageNumber":1,
"PageSize":1,
"ScalingActivities":{
"ScalingActivity":[
{
   "ScalingActivityId":"bBxOR5dhKFoccGkbTrcyHE2g",
   "StartTime":"2014-08-18T20:49Z",
"EndTime":"2014-08-18T20:49Z",
"Cause":" A scheduled task excuete scaling rule \"srtest\"，changing the Total Capacity from \"0\" to \"1\".",
"Description":" Add \"1\" ECS instance ",
"Progress":100,
"ScalingGroupId":"c7acXJbAJmpPcGE7G3bwwbS9",
"StatusCode":"Successful",
"StatusMessage":"\"1\" ECS instances is added. "
}
]
},
}
```

## 错误码 { .section}

关于所有接口的通用性错误，请参考 [客户端错误](intl.zh-CN/API参考/错误代码/客户端错误.md#) 或 [服务器端错误](intl.zh-CN/API参考/错误代码/服务器端错误.md#)。

