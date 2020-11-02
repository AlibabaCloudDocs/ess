# DescribeScalingActivities

调用DescribeScalingActivities查询伸缩活动。

## 接口说明

查询时可以指定伸缩组ID来查询该伸缩组下的所有伸缩活动。

查询时可以通过伸缩活动的状态来过滤查询结果。

可以查询30日内的伸缩活动。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DescribeScalingActivities&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeScalingActivities|系统规定参数。取值：DescribeScalingActivities |
|RegionId|String|是|cn-hangzhou|伸缩活动所属伸缩组的地域ID。 |
|PageNumber|Integer|否|1|伸缩活动列表的页码，起始值：1。

 默认值：1 |
|PageSize|Integer|否|10|分页查询时设置的每页行数，最大值：50。

 默认值：10 |
|ScalingGroupId|String|否|asg-bp18p2yfxow2dloq\*\*\*\*|伸缩组的ID。 |
|StatusCode|String|否|Successful|伸缩活动的状态。取值范围：

 -   Successful：执行成功的伸缩活动。
-   Warning：部分执行成功的伸缩活动。
-   Failed：执行失败的伸缩活动。
-   InProgress：正在执行的伸缩活动。
-   Rejected：执行伸缩活动请求被拒绝。 |
|ScalingActivityId.1|String|否|asa-bp161xudmuxdzofe\*\*\*\*|ScalingActivityId.N为待查询伸缩活动的ID，N的取值范围：1～20。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|当前页码。 |
|PageSize|Integer|10|每页行数。 |
|RequestId|String|CC107349-57B7-4405-B1BF-9BF5AF7F2A46|请求ID。 |
|ScalingActivities|Array of ScalingActivity| |伸缩活动信息组成的集合。 |
|ScalingActivity| | | |
|AttachedCapacity|String|0|执行完伸缩活动后，伸缩组中用户手动添加的实例的总数。 |
|AutoCreatedCapacity|String|2|执行完伸缩活动后，伸缩组中由伸缩组负责自动创建的实例的总数。 |
|Cause|String|A user requests to execute scaling rule \\"asr-bp12tcnol686y1ik\*\*\*\*\\", changing the Total Capacity from \\"1\\" to \\"2\\".|触发伸缩活动的原因。 |
|Description|String|Add \\"1\\" ECS instance|伸缩活动的描述信息。 |
|EndTime|String|2020-09-10T09:54Z|伸缩活动的结束时间。 |
|Progress|Integer|100|伸缩活动的运行进度。 |
|ScalingActivityId|String|asa-bp161xudmuxdzofe\*\*\*\*|伸缩活动的ID。 |
|ScalingGroupId|String|asg-bp18p2yfxow2dloq\*\*\*\*|伸缩组的ID。 |
|ScalingInstanceNumber|Integer|1|如果伸缩活动类型为扩容，该参数表示本次伸缩活动中被创建或从停机回收状态启动的实例的个数。

 如果伸缩活动类型为缩容，该参数表示本次伸缩活动中被删除或进入停机回收状态的实例的个数。 |
|StartTime|String|2020-09-10T09:54Z|伸缩活动的开始时间。 |
|StatusCode|String|Successful|伸缩活动的状态，取值范围：

 -   Successful：执行成功的伸缩活动。
-   Warning：部分执行成功的伸缩活动。
-   Failed：执行失败的伸缩活动。
-   InProgress：正在执行的伸缩活动。
-   Rejected：执行伸缩活动请求被拒绝。 |
|StatusMessage|String|\\"1\\" ECS instances are added|伸缩活动的状态信息。 |
|TotalCapacity|String|2|执行完伸缩活动后，伸缩组中实例的总数。 |
|TotalCount|Integer|1|伸缩活动总数。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=DescribeScalingActivities
&RegionId=cn-qingdao
&ScalingGroupId=asg-bp18p2yfxow2dloq****
&StatusCode=Successful
&ScalingActivityId.1=asa-bp161xudmuxdzofe****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeScalingActivitiesResponse>
    <TotalCount>1</TotalCount>
    <PageSize>10</PageSize>
    <RequestId>CC107349-57B7-4405-B1BF-9BF5AF7F2A46</RequestId>
    <PageNumber>1</PageNumber>
    <ScalingActivities>
        <ScalingActivity>
            <ScalingInstanceNumber>1</ScalingInstanceNumber>
            <Progress>100</Progress>
            <Description>Add "1" ECS instance</Description>
            <EndTime>2020-09-10T09:54Z</EndTime>
            <AttachedCapacity>0</AttachedCapacity>
            <ScalingActivityId>asa-bp161xudmuxdzofe****</ScalingActivityId>
            <ScalingGroupId>asg-bp18p2yfxow2dloq****</ScalingGroupId>
            <StartTime>2020-09-10T09:54Z</StartTime>
            <StatusCode>Successful</StatusCode>
            <AutoCreatedCapacity>2</AutoCreatedCapacity>
            <StatusMessage>"1" ECS instances are added</StatusMessage>
            <Cause>A user requests to execute scaling rule "asr-bp12tcnol686y1ik****", changing the Total Capacity from "1" to "2".</Cause>
            <TotalCapacity>2</TotalCapacity>
        </ScalingActivity>
    </ScalingActivities>
</DescribeScalingActivitiesResponse>
```

`JSON` 格式

```
{
	"TotalCount": 1,
	"PageSize": 10,
	"RequestId": "CC107349-57B7-4405-B1BF-9BF5AF7F2A46",
	"PageNumber": 1,
	"ScalingActivities": {
		"ScalingActivity": [
			{
				"ScalingInstanceNumber": 1,
				"Progress": 100,
				"Description": "Add \"1\" ECS instance",
				"EndTime": "2020-09-10T09:54Z",
				"AttachedCapacity": 0,
				"ScalingActivityId": "asa-bp161xudmuxdzofe****",
				"ScalingGroupId": "asg-bp18p2yfxow2dloq****",
				"StartTime": "2020-09-10T09:54Z",
				"StatusCode": "Successful",
				"AutoCreatedCapacity": 2,
				"StatusMessage": "\"1\" ECS instances are added",
				"Cause": "A user requests to execute scaling rule \"asr-bp12tcnol686y1ik****\", changing the Total Capacity from \"1\" to \"2\".",
				"TotalCapacity": 2
			}
		]
	}
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ess)查看更多错误码。

