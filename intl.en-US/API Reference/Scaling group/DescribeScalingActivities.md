# DescribeScalingActivities

You can call this operation to query scaling activities.

## Description

You can specify a scaling group ID to query all scaling activities in the scaling group.

You can filter query results based on the status of scaling activities.

You can query scaling activities that are executed in the last 30 days.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeScalingActivities&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeScalingActivities|The operation that you want to perform. Set the value to DescribeScalingActivities. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the scaling group to which the scaling activity belongs. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default: 1 |
|PageSize|Integer|No|10|The number of entries to return on each page. Maximum value: 50.

Default value: 10 |
|ScalingGroupId|String|No|asg-bp18p2yfxow2dloq\*\*\*\*|The ID of the scaling group. |
|StatusCode|String|No|Successful|The status of the scaling activity. Valid values:

-   Successful: The scaling activity is successful.
-   Warning: The scaling activity is partially successful.
-   Failed: The scaling activity fails.
-   InProgress: The scaling activity is in progress.
-   Rejected: The scaling activity request is rejected. |
|ScalingActivityId.N|RepeatList|No|asa-bp161xudmuxdzofe\*\*\*\*|The ID of scaling activity N to be queried. Valid values of N: 1 to 20. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|CC107349-57B7-4405-B1BF-9BF5AF7F2A46|The ID of the request. |
|ScalingActivities|Array of ScalingActivity| |Details about the scaling activities. |
|ScalingActivity| | | |
|AttachedCapacity|String|0|The total number of instances that were manually added to the scaling group after the scaling activity was complete. |
|AutoCreatedCapacity|String|2|The total number of instances that were automatically created by Auto Scaling after the scaling activity was complete. |
|Cause|String|A user requests to execute scaling rule \\"asr-bp12tcnol686y1ik\*\*\*\*\\", changing the Total Capacity from \\"1\\" to \\"2\\".|The cause that triggered the scaling activity. |
|Description|String|Add \\"1\\" ECS instance|The description of the scaling activity. |
|EndTime|String|2020-09-10T09:54Z|The time when the scaling activity ended. |
|Progress|Integer|100|The execution progress of the scaling activity. |
|ScalingActivityId|String|asa-bp161xudmuxdzofe\*\*\*\*|The ID of the scaling activity. |
|ScalingGroupId|String|asg-bp18p2yfxow2dloq\*\*\*\*|The ID of the scaling group. |
|ScalingInstanceNumber|Integer|1|The number of instances that were created or restarted from the Stopped state during the scale-out event.

The number of instances that were deleted or put into the Stopped state during the scale-in event. |
|StartTime|String|2020-09-10T09:54Z|The time when the scaling activity started. |
|StatusCode|String|Successful|The status of the scaling activity. Valid values:

-   Successful: The scaling activity was successful.
-   Warning: The scaling activity was partially successful.
-   Failed: The scaling activity failed.
-   InProgress: The scaling activity was in progress.
-   Rejected: The scaling activity request was rejected. |
|StatusMessage|String|\\"1\\" ECS instances are added|The status about the scaling activity. |
|TotalCapacity|String|2|The total number of instances in the scaling group after the scaling activity was complete. |
|TotalCount|Integer|1|The total number of scaling activities. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DescribeScalingActivities
&RegionId=cn-qingdao
&ScalingGroupId=asg-bp18p2yfxow2dloq****
&StatusCode=Successful
&ScalingActivityId.1=asa-bp161xudmuxdzofe****
&<Common request parameters>
```

Sample success responses

`XML` format

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
            <Cause>A user requests to execute scaling rule "asr-bp12tcnol686y1ik****", changing the Total Capacity from "1" to "2". </Cause>
            <TotalCapacity>2</TotalCapacity>
        </ScalingActivity>
    </ScalingActivities>
</DescribeScalingActivitiesResponse>
```

`JSON` format

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

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

