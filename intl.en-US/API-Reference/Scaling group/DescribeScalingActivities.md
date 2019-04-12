# DescribeScalingActivities {#concept_25961_zh .concept}

This topic introduces how to query a scaling activity using the API.

## Description {#section_ard_kck_sfb .section}

Queries a scaling activity.

-   You can specify a scaling group ID to query all scaling activities in this scaling group.
-   You can filter the query results based on the scaling activity status.
-   Only scaling activities during the last 30 days can be returned.

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|Operation interface name, required parameter. Value: DescribeScalingActivities|
|RegionId|String|Yes|Region of the scaling activity|
|ScalingGroupId|String|No|Scaling group ID|
|ScalingActivityId.N|String|No|Scaling group ID. You can enter up to 10 IDs. Invalid scaling group IDs are neglected in the query results, and no error is reported.

 |
|StatusCode|String|No|Scaling activity status. Optional values: Successful: -   Successful scaling activities.
-   Warning: Partially successful scaling activities.
-   Failed: Failed scaling activities.
-   InProgress: Scaling activities in progress.
-   Rejected: The scaling activity request is rejected.

 |
|PageNumber|Integer|No|Page number of the scaling activity list starting from 1. The default value is 1.|
|PageSize|Integer|No|When querying by page, this parameter indicates the number of lines per page. Maximum value: 50; default value: 10|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|TotalCount|Integer|Total number of the scaling activities|
|PageNumber|Integer|Current page number|
|PageSize|Integer|Number of lines per page|
|ScalingActivities|ScalingActivitySetType|Set of the scaling activity information|

ScalingActivities is a set consisting of the ScalingActivityItemType.

|Name|Type|Description|
|:---|:---|:----------|
|ScalingActivity|ScalingActivityItemType|Scaling activity information|

Attributes of the ScalingActivityItemType are introduced as follows.

|Name|Type|Description|
|:---|:---|:----------|
|ScalingActivityId|String|Scaling activity ID|
|ScalingGroupId|String|Scaling group ID|
|Description|String|Description on the scaling activity|
|Cause|String|Cause that triggers the scaling activity|
|StartTime|String|Start time of the scaling activity|
|EndTime|String|End time of the scaling activity|
|Progress|Integer|Running speed of the scaling activity|
|StatusCode|String|Current status of the scaling activity|
|StatusMessage|String|Message about the scaling activity status|

## Request example { .section}

```
http://ess.aliyuncs.com/?Action=DescribeScalingActivities
&RegionId=cn-qingdao
&PageSize=50
&<Public Request Parameters>
```

## Response example { .section}

## XML format: { .section}

```
<DescribeScalingActivitiesResponse>
    <RequestId>8FAAE99E-EB43-4838-85AD-93F62454904C</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <ScalingActivities>
        <ScalingActivity>
            <Cause>A scheduled task excuete scaling rule "srtest"，changing the Total Capacity from "0" to "1". </Cause>
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

## JSON format: { .section}

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

## Error code { .section}

For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

