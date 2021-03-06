# DescribeLifecycleActions

You can call this operation to query the lifecycle actions that correspond to a scaling activity.

## Description

If a scaling activity whose type is consistent with that of lifecycle hooks occurs, each lifecycle hook triggers a lifecycle action. The following section describes the statuses of lifecycle actions:

-   Pending: The lifecycle action is pending. ECS instances are put into the wait state.
-   Timeout: The lifecycle action times out. The lifecycle hook times out and puts ECS instances out of the wait state.
-   Completed: The lifecycle action is processed. You manually put ECS instances out of the wait state in advance.

If you do not specify the subsequent actions when you create a lifecycle hook, such as triggering the execution of a specific Operation Orchestration Service \(OOS\) template after ECS instances are put out of the wait state, you can call this operation to obtain the token of the corresponding lifecycle action for the current scaling activity. This helps you customize the subsequent actions.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeLifecycleActions&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeLifecycleActions|The operation that you want to perform. Set the value to DescribeLifecycleActions. |
|ScalingActivityId|String|Yes|asa-bp17mug9t0pegagw\*\*\*\*|The ID of the scaling activity. |
|LifecycleActionStatus|String|No|Pending|The status of the lifecycle action. Valid values:

-   Pending: The lifecycle action is pending. ECS instances are put into the wait state.
-   Timeout: The lifecycle action times out. The lifecycle hook times out and puts ECS instances out of the wait state.
-   Completed: The lifecycle action is processed. You manually put ECS instances out of the wait state in advance. |
|NextToken|String|No|AAAAAcSz4VTb1Nq\*\*\*\*|The query token. It is used to specify the position from which to start the query. For example, after 10 lifecycle actions were queried, the query starts from the eleventh lifecycle action. Set this parameter to the NextToken value that is returned in the previous API call. If this parameter is not specified, the query starts from the beginning. |
|MaxResults|Integer|No|1|The maximum number of entries to return on each page. Valid values: 1 to 50.

Default value: 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|LifecycleActions|Array of LifecycleAction| |The lifecycle actions that correspond to each lifecycle hook. |
|LifecycleAction| | | |
|InstanceIds|List|\["i-bp11m3fzlqrgk5vh\*\*\*\*","i-bp11m3fzlqrgk5vh\*\*\*\*"\]|The IDs of the ECS instances that are put into the wait state by the lifecycle hook. |
|LifecycleActionResult|String|CONTINUE|The next action to take after the lifecycle action triggered by the lifecycle hook ends. Valid values:

-   CONTINUE: Auto Scaling continues to respond to a scale-out event and adds ECS instances to the scaling group, or continues to respond to a scale-in event and removes ECS instances from the scaling group.
-   ABANDON: Auto Scaling terminates a scale-out event and releases the created ECS instances or continues to respond to a scale-in event and removes ECS instances from the scaling group. |
|LifecycleActionStatus|String|Pending|The status of the lifecycle action. |
|LifecycleActionToken|String|9C2E9DA7-F794-449A-ACF6-CEE24444F7BB|The token of the lifecycle action. |
|LifecycleHookId|String|ash-bp18uoft0deax0f7\*\*\*\*|The ID of the lifecycle hook. |
|MaxResults|Integer|3|The maximum number of entries returned per page. |
|NextToken|String|AAAAAcSz4VTb1Nq\*\*\*\*|The query token returned in this call. |
|RequestId|String|42A742EB-FCF3-459E-9C62-E107048C17E3|The ID of the request. |
|TotalCount|Integer|3|The total number of queried lifecycle actions. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DescribeLifecycleActions
&ScalingActivityId=asa-bp17mug9t0pegagw****
&MaxResults=3
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeLifecycleActionsResponse>
      <TotalCount>3</TotalCount>
      <RequestId>678A42DB-A9CE-44C7-95B0-9E4150E6308F</RequestId>
      <NextToken>AAAAAcSz4VTb****</NextToken>
      <MaxResults>3</MaxResults>
      <LifecycleActions>
            <LifecycleAction>
                  <LifecycleActionStatus>Pending</LifecycleActionStatus>
                  <LifecycleActionResult>CONTINUE</LifecycleActionResult>
                  <InstanceIds>
                        <InstanceId>i-bp11m3fzlqrgk5vh****</InstanceId>
                        <InstanceId>i-bp11m3fzlqrgk5vh****</InstanceId>
                  </InstanceIds>
                  <LifecycleActionToken>9C2E9DA7-F794-449A-ACF6-CEE24444F7BB</LifecycleActionToken>
                  <LifecycleHookId>ash-bp16ed9xxytrxdlt****</LifecycleHookId>
            </LifecycleAction>
            <LifecycleAction>
                  <LifecycleActionStatus>Pending</LifecycleActionStatus>
                  <LifecycleActionResult>CONTINUE</LifecycleActionResult>
                  <InstanceIds>
                        <InstanceId>i-bp11m3fzlqrgk5vh****</InstanceId>
                        <InstanceId>i-bp11m3fzlqrgk5vh****</InstanceId>
                  </InstanceIds>
                  <LifecycleActionToken>35D11A1F-A2CF-4B6E-B164-B19CC94D1A33</LifecycleActionToken>
                  <LifecycleHookId>ash-bp18uoft0deax0f7****</LifecycleHookId>
            </LifecycleAction>
            <LifecycleAction>
                  <LifecycleActionStatus>Pending</LifecycleActionStatus>
                  <LifecycleActionResult>CONTINUE</LifecycleActionResult>
                  <InstanceIds>
                        <InstanceId>i-bp11m3fzlqrgk5vh****</InstanceId>
                        <InstanceId>i-bp11m3fzlqrgk5vh****</InstanceId>
                  </InstanceIds>
                  <LifecycleActionToken>25547B8D-05D8-44D7-84D4-3E594556CAD3</LifecycleActionToken>
                  <LifecycleHookId>ash-bp18uoft0deayjo2****</LifecycleHookId>
            </LifecycleAction>
      </LifecycleActions>
</DescribeLifecycleActionsResponse>
```

`JSON` format

```
{
    "TotalCount": 3,
    "RequestId": "678A42DB-A9CE-44C7-95B0-9E4150E6308F",
    "NextToken": "AAAAAcSz4VTb****",
    "MaxResults": 3,
    "LifecycleActions": {
        "LifecycleAction": [
            {
                "LifecycleActionStatus": "Pending",
                "LifecycleActionResult": "CONTINUE",
                "InstanceIds": {
                    "InstanceId": [
                        "i-bp11m3fzlqrgk5vh****",
                        "i-bp11m3fzlqrgk5vh****"
                    ]
                },
                "LifecycleActionToken": "9C2E9DA7-F794-449A-ACF6-CEE24444F7BB",
                "LifecycleHookId": "ash-bp16ed9xxytrxdlt****"
            },
            {
                "LifecycleActionStatus": "Pending",
                "LifecycleActionResult": "CONTINUE",
                "InstanceIds": {
                    "InstanceId": [
                        "i-bp11m3fzlqrgk5vh****",
                        "i-bp11m3fzlqrgk5vh****"
                    ]
                },
                "LifecycleActionToken": "35D11A1F-A2CF-4B6E-B164-B19CC94D1A33",
                "LifecycleHookId": "ash-bp18uoft0deax0f7****"
            },
            {
                "LifecycleActionStatus": "Pending",
                "LifecycleActionResult": "CONTINUE",
                "InstanceIds": {
                    "InstanceId": [
                        "i-bp11m3fzlqrgk5vh****",
                        "i-bp11m3fzlqrgk5vh****"
                    ]
                },
                "LifecycleActionToken": "25547B8D-05D8-44D7-84D4-3E594556CAD3",
                "LifecycleHookId": "ash-bp18uoft0deayjo2****"
            }
        ]
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|400

|InvalidParameter

|The specified value of parameter "ScalingActivityId" is not valid.

|The error message returned because a specified parameter is invalid. |
|400

|InvalidParameter

|The specified value of parameter "MaxResults" is not valid.

|The error message returned because a specified parameter is invalid. |
|400

|InvalidParameter

|The specified value of parameter "LifecycleActionStatus" is not valid.

|The error message returned because a specified parameter is invalid. |

