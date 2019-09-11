# DescribeScalingActivities {#doc_api_Ess_DescribeScalingActivities .reference}

调用DescribeScalingActivities查询伸缩活动。

## 接口说明 {#description .section}

查询时可以指定伸缩组ID来查询该伸缩组下的所有伸缩活动。

查询时可以通过伸缩活动的状态来过滤查询结果。

可以查询30日内的伸缩活动。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DescribeScalingActivities&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-qingdao|伸缩活动所属伸缩组的地域ID。

 |
|Action|String|否|DescribeScalingActivities|系统规定参数，取值：DescribeScalingActivities。

 |
|PageNumber|Integer|否|1|伸缩活动列表的页码，起始值：1。

 默认值：1 。

 |
|PageSize|Integer|否|50|分页查询时设置的每页行数，最大值：50。

 默认值：10 。

 |
|ScalingActivityId.1|String|否|ebta5WbUzC8gcwUWvfch\*\*\*\*|ScalingActivityId.N为待查询伸缩活动的ID，N的取值范围：1～20。

 |
|ScalingGroupId|String|否|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组的ID。

 |
|StatusCode|String|否|Successful|伸缩活动的状态，取值范围：

 -   Successful：执行成功的伸缩活动。
-   Warning：部分执行成功的伸缩活动。
-   Failed：执行失败的伸缩活动。
-   InProgress：正在执行的伸缩活动。
-   Rejected：执行伸缩活动请求被拒绝。

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
|ScalingActivities| | |伸缩活动信息组成的集合。

 |
|AttachedCapacity|String|1|执行完伸缩活动后，伸缩组中用户手动添加的实例的总数。

 |
|AutoCreatedCapacity|String|1|执行完伸缩活动后，伸缩组中由伸缩组负责自动创建的实例的总数。

 |
|Cause|String|A scheduled task excuete scaling rule \\"sr\*\*\*\*\\"，changing the Total Capacity from \\"0\\" to \\"1\\".|触发伸缩活动的原因。

 |
|Description|String|Add \\"1\\" ECS instance|伸缩活动的描述信息。

 |
|EndTime|String|2014-08-17T12:39Z|伸缩活动的结束时间。

 |
|Progress|Integer|100|伸缩活动的运行进度。

 |
|ScalingActivityId|String|ebta5WbUzC8gcwUWvfch\*\*\*\*|伸缩活动的ID。

 |
|ScalingGroupId|String|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组的ID。

 |
|ScalingInstanceNumber|Integer|1|如果伸缩活动类型为扩容，该参数表示本次伸缩活动中被创建或从停机回收状态启动的实例的个数。

 如果伸缩活动类型为缩容，该参数表示本次伸缩活动中被删除或进入停机回收状态的实例的个数。

 |
|StartTime|String|2014-08-17T12:39Z|伸缩活动的开始时间。

 |
|StatusCode|String|2014-08-17T12:39Z|伸缩活动的状态，取值范围：

 -   Successful：执行成功的伸缩活动。
-   Warning：部分执行成功的伸缩活动。
-   Failed：执行失败的伸缩活动。
-   InProgress：正在执行的伸缩活动。
-   Rejected：执行伸缩活动请求被拒绝。

 |
|StatusMessage|String|"1" ECS instances is added.|伸缩活动的状态信息。

 |
|TotalCapacity|String|2|执行完伸缩活动后，伸缩组中实例的总数。

 |
|TotalCount|Integer|1|伸缩活动总数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DescribeScalingActivities
&RegionId=cn-qingdao
&PageSize=50
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeScalingActivitiesResponse>
      <RequestId>8FAAE99E-EB43-4838-85AD-93F62454904C</RequestId>
      <TotalCount>1</TotalCount>
      <PageNumber>1</PageNumber>
      <PageSize>10</PageSize>
      <ScalingActivities>
            <ScalingActivity>
                  <Cause>A scheduled task excuete scaling rule "sr****"，changing the Total Capacity from "0" to "1".</Cause>
                  <Description>Add "1" ECS instance</Description>
                  <EndTime>2014-08-17T12:39Z</EndTime>
                  <Progress>100</Progress>
                  <ScalingActivityId>ebta5WbUzC8gcwUWvfch****</ScalingActivityId>
                  <ScalingGroupId>AG6CQdPU8OKdwLjgZcJ****</ScalingGroupId>
                  <StartTime>2014-08-17T12:39Z</StartTime>
                  <StatusCode>Successful</StatusCode>
                  <StatusMessage>"1" ECS instances is added. </StatusMessage>
            </ScalingActivity>
      </ScalingActivities>
</DescribeScalingActivitiesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":2582,
	"PageSize":1,
	"RequestId":"0A016AD6-A91F-4210-9DEE-D5BBD4270F45",
	"ScalingActivities":{
		"ScalingActivity":[
			{
				"StatusCode":"Successful",
				"Description":" Add \"1\" ECS instance ",
				"ScalingGroupId":"c7acXJbAJmpPcGE7G3bw****",
				"StatusMessage":"\"1\" ECS instances is added. ",
				"EndTime":"2014-08-18T20:49Z",
				"StartTime":"2014-08-18T20:49Z",
				"Progress":100,
				"Cause":" A scheduled task excuete scaling rule \"sr****\"，changing the Total Capacity from \"0\" to \"1\".",
				"ScalingActivityId":"bBxOR5dhKFoccGkbTrcy****"
			}
		]
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ess)查看更多错误码。

