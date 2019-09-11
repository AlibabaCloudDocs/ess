# DescribeScalingActivities {#doc_api_Ess_DescribeScalingActivities .reference}

You can call this operation to query scaling activities.

## Description {#description .section}

You can specify a scaling group ID to query all scaling activities in this scaling group.

You can filter query results based on the status of scaling activities.

Only scaling activities during the last 30 days can be returned.

## Debugging {#api_explorer .section}

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeScalingActivities&type=RPC&version=2014-08-28)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|RegionId|String|Yes|cn-qingdao| The region ID of the scaling group to which a scaling activity belongs.

 |
|Action|String|No|DescribeScalingActivities| The operation that you want to perform. Set the value to DescribeScalingActivities.

 |
|PageNumber|Integer|No|1| The page number of the scaling activity list to return. Pages start from page 1.

 Default value: 1.

 |
|PageSize|Integer|No|50| The number of entries to return on each page. Maximum value: 50.

 Default value: 10.

 |
|ScalingActivityId.1|String|No|ebta5WbUzC8gcwUWvfch\*\*\*\*| The ID of scaling activity N to be queried. Valid values of N: 1 to 20.

 |
|ScalingGroupId|String|No|AG6CQdPU8OKdwLjgZcJ\*\*\*\*| The ID of the scaling group.

 |
|StatusCode|String|No|Successful| The status of the scaling activity. Valid values:

 -   Successful: The scaling activity was successfully executed.
-   Warning: The scaling activity was partially executed.
-   Failed: The scaling activity failed.
-   InProgress: The scaling activity is currently being executed.
-   Rejected: The scaling activity request was rejected.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1| The current page number.

 |
|PageSize|Integer|50| The number of entries returned on each page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|ScalingActivities| | | The set of scaling activities.

 |
|AttachedCapacity|String|1| The total number of instances that you added manually to the scaling group after the scaling activity was completed.

 |
|AutoCreatedCapacity|String|1| The total number of the instances that were added automatically by the scaling group after the scaling activity was completed.

 |
|Cause|String|A scheduled task execute scaling rule \\"sr\*\*\*\*\\",changing the Total Capacity from \\"0\\" to \\"1\\".| The cause that triggered the scaling activity.

 |
|Description|String|Add \\"1\\" ECS instance| The description of the scaling activity.

 |
|EndTime|String|2014-08-17T12:39Z| The time when the scaling activity ended.

 |
|Progress|Integer|100| The execution progress of the scaling activity.

 |
|ScalingActivityId|String|ebta5WbUzC8gcwUWvfch\*\*\*\*| The ID of the scaling activity.

 |
|ScalingGroupId|String|AG6CQdPU8OKdwLjgZcJ\*\*\*\*| The ID of the scaling group.

 |
|ScalingInstanceNumber|Integer|1| The number of instances that were created or restarted from the shutdown and reclaim mode during the scale-out event.

 The number of instances that were deleted or switched to the shutdown and reclaim mode during the scale-in event.

 |
|StartTime|String|2014-08-17T12:39Z| The time when the scaling activity started.

 |
|StatusCode|String|2014-08-17T12:39Z| The status of the scaling activity. Valid values:

 -   Successful: The scaling activity was successfully executed.
-   Warning: The scaling activity was partially executed.
-   Failed: The scaling activity failed.
-   InProgress: The scaling activity is currently being executed.
-   Rejected: The scaling activity request was rejected.

 |
|StatusMessage|String|"1" ECS instances is added.| The details about the scaling activity in a state.

 |
|TotalCapacity|String|2| The total number of instances in the scaling group after the scaling activity was completed.

 |
|TotalCount|Integer|1| The total number of scaling activities.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DescribeScalingActivities
&RegionId=cn-qingdao
&PageSize=50
&<Common request parameters>

```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
<DescribeScalingActivitiesResponse>
      <RequestId>8FAAE99E-EB43-4838-85AD-93F62454904C</RequestId>
      <TotalCount>1</TotalCount>
      <PageNumber>1</PageNumber>
      <PageSize>10</PageSize>
      <ScalingActivities>
            <ScalingActivity>
                  <Cause>A scheduled task execute scaling rule "sr****",changing the Total Capacity from "0" to "1". </Cause>
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

`JSON` format

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
				"Cause":" A scheduled task execute scaling rule \"sr****\",changing the Total Capacity from \"0\" to \"1\".",
				"ScalingActivityId":"bBxOR5dhKFoccGkbTrcy****"
			}
		]
	}
}
```

## Error codes {#section_ztj_8yc_77i .section}

