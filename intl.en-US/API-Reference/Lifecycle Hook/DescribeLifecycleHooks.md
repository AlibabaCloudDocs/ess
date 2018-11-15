# DescribeLifecycleHooks {#concept_73843_zh .concept}

This interface queries one or multiple lifecycle hooks that meet the specified conditions \(`DescribeLifecycleHooks`\).

You can query lifecycle hooks using the following methods:

-   Specify the parameter `LifecycleHookId.N`. `ScalingGroupId` and `LifecycleHookName` are ignored.
-   Specify the parameter `ScalingGroupId`.
-   Specify the parameters `ScalingGroupId` and `LifecycleHookName`.

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: DescribeLifecycleHooks.|
|LifecycleHookId.N|String|No|The list of lifecycle hook IDs. Replace `N` with the actual number to indicate a specific item lifecycle hook. The value range of N is \[1, 50\].|
|ScalingGroupId|String|No|The ID of the scaling group|
|LifecycleHookName|String|No|The name of the lifecycle hook|
|PageNumber|Integer|No|Page numbers of the instance status list. Initial value: 1; Default value: 1.|
|PageSize|Integer|No|Number of rows per page when performing a query. Maximum: 50. Default: 50.|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|RequestId|String|The request ID|
|PageNumber|Integer|The initial page number for query|
|PageSize|String|The number of items returned per page when performing a query|
|TotalCount|String|Total number of lifecycle hooks|
|LifecycleHooks| [LifecycleHookModelSet](#) |The list of lifecycle hook data|

## LifecycleHookModelSet {#hxone .section}

|Name|Type|Description|
|:---|:---|:----------|
|ScalingGroupId|String|The ID of the scaling group|
|LifecycleHookId|String|The ID of the lifecycle hook|
|LifecycleHookName|String|The name of the lifecycle hook|
|DefaultResult|String|The action that the scaling group takes when the lifecycle hook times out|
|HeartbeatTimeout|Integer|The time, in seconds, that can elapse before the lifecycle hook times out. When the lifecycle hook times out, the scaling group performs the default action.|
|LifecycleTransition|String|The scaling activities to which lifecycle hooks apply|
|NotificationMetadata|String|The fixed string that you want to include when Auto Scaling sends a message about the wait state of the scaling activity to the notification target.|
|NotificationArn|String|The Alibaba Cloud Resource Name \(ARN\) of the notification target that Auto Scaling will use to notify you when an instance is in the transition state for the lifecycle hook.|

## Request example { .section}

```
http://ess.aliyuncs.com/?Action=DescribeLifecycleHooks
&ScalingGroupId=asg-xxxxx
&<Public request parameter>
```

## Response example { .section}

XML format:

```
<DescribeLifecycleHooksResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
  <PageNumber>1</PageNumber>
  <PageSize>50</PageSize>
  <TotalCount>1</TotalCount>
  <LifecycleHooks>
    <LifecycleHook>
      <ScalingGroupId>asg-xxx</ScalingGroupId>
      <LifecycleHookId>ash-xxx</LifecycleHookId>
      <LifecycleHookName>Test</LifecycleHookName>
      <DefaultResult>CONTINUE</DefaultResult>
      <HeartbeatTimeout>60</HeartbeatTimeout>
      <LifecycleTransition>SCALE_OUT</LifecycleTransition>
      <NotificationMetadata>Test</NotificationMetadata>
      <NotificationArn>acs:ess:cn-hangzhou:1111111111:queue/queue1</NotificationArn>
    </LifecycleHook>
  </LifecycleHooks>
</DescribeLifecycleHooksResponse>
```

JSON format:

```
{
  "lifecycleHooks": [
  {
    "defaultResult": "CONTINUE",
    "heartbeatTimeout": 600,
    "lifecycleHookId": "ash-xxx",
    "lifecycleHookName": "Test",
    "lifecycleTransition": "SCALE_OUT",
    "notificationArn": "acs:ess:cn-hangzhou:1111111111:queue/queue1",
    "notificationMetadata": "Test",
    "scalingGroupId": "asg-xxx"
  }
  ],
  "pageNumber": 1,
  "pageSize": 50,
  "requestId": "04F0F334-1335-436C-A1D7-6C044FE73368",
  "totalCount": 1
}
```

## Error code { .section}

Error code specific to this interface is as follows. For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|Error code|Error message|HTTP status code|Description|
|:---------|:------------|:---------------|:----------|
|InvalidParamter|The specified value of parameter is not valid.|400|The specified value of the parameter is invalid.|

