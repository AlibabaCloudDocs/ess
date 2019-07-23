# DescribeLifecycleHooks {#doc_api_1163758 .reference}

You can call this operation to query the list of lifecycle hooks that meet one or more specified conditions.

## Description {#description .section}

You can use one of the following three methods to query lifecycle hooks:

-   Specify the `LifecycleHookId.N` parameter. This way, you do not need to specify the `ScalingGroupId` or `LifecycleHookName` parameters.
-   Specify the `ScalingGroupId` parameter.
-   Specify the `ScalingGroupId` and `LifecycleHookName` parameters at the same time.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=DescribeLifecycleHooks) simplifies API usage. You can use OpenAPI Explorer to perform debugging operations, such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|No|DescribeLifecycleHooks|The operation that you want to perform. Set the value to DescribeLifecycleHooks.

 |
|LifecycleHookId.N|RepeatList|No|ash-\*\*\*\*|The ID of the lifecycle hook.

 |
|LifecycleHookName|String|No|Test|The name of the lifecycle hook.

 |
|PageNumber|Integer|No|1|The page number that you query in the instance status list. Starting value: 1. Default value: 1.

 |
|PageSize|Integer|No|50|The number of rows per page. Maximum value: 50. Default value: 50.

 |
|ScalingGroupId|String|No|asg-\*\*\*\*|The ID of the scaling group.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|LifecycleHooks| | |The list of lifecycle hook information.

 |
|└DefaultResult|String|CONTINUE|The action that the scaling group takes when the wait state terminates.

 |
|└HeartbeatTimeout|Integer|60|The time that can elapse before the lifecycle hook times out. If the lifecycle hook times out, the scaling group performs the default action \(DefaultResult\).

 |
|└LifecycleHookId|String|ash-\*\*\*\*|The ID of the lifecycle hook.

 |
|└LifecycleHookName|String|Test|The name of the lifecycle hook.

 |
|└LifecycleTransition|String|SCALE\_OUT|The type of the scaling activity to which the lifecycle hook corresponds.

 |
|└NotificationArn|String|acs:ess:cn-hangzhou:1111111111:queue/queue1|The Alibaba Cloud Resource Name \(ARN\) of the notification object that Auto Scaling uses to notify you when an instance is in the transition state for the lifecycle hook.

 |
|└NotificationMetadata|String|Test|The fixed string that is included in the message that is sent by Auto Scaling about the wait state of a scaling activity to the notification object.

 |
|└ScalingGroupId|String|asg-\*\*\*\*|The ID of the scaling group.

 |
|PageNumber|Integer|1|The initial page number for the query.

 |
|PageSize|Integer|50|The number of rows returned per page when you perform the query.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |
|TotalCount|Integer|1|The total count of lifecycle hooks.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DescribeLifecycleHooks
&ScalingGroupId=asg-****
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeLifecycleHooksResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
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

`JSON` format

``` {#json_return_success_demo}
{
	"lifecycleHooks":[
		{
			"notificationArn":"acs:ess:cn-hangzhou:1111111111:queue/queue1",
			"lifecycleHookId":"ash-****",
			"notificationMetadata":"Test",
			"lifecycleTransition":"SCALE_OUT",
			"defaultResult":"CONTINUE",
			"lifecycleHookName":"Test",
			"scalingGroupId":"asg-****",
			"heartbeatTimeout":600
		}
	],
	"totalCount":1,
	"requestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"pageSize":50,
	"pageNumber":1
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Ess)

|HTTP status code

|Error code

|Error message

|Description

|
|------------------|------------|---------------|-------------|
|400

|InvalidParamter

|The specified value of parameter is not valid.

|The error message returned when the value of the parameter is invalid.

|

