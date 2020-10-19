# DescribeLifecycleHooks

You can call this operation to query lifecycle hooks.

## Description

You can use one of the following methods to query lifecycle hooks:

-   Specify a list of lifecycle hook IDs by using the LifecycleHookId.N parameter. Then, the scaling group ID specified by ScalingGroupId and the lifecycle hook name specified by LifecycleHookName will be ignored.
-   Specify the scaling group ID by using the ScalingGroupId parameter.
-   Specify the scaling group ID by using the ScalingGroupId parameter and the lifecycle hook name by using the LifecycleHookName parameter.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeLifecycleHooks&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeLifecycleHooks|The operation that you want to perform. Set the value to DescribeLifecycleHooks. |
|ScalingGroupId|String|No|asg-bp1igpak5ft1flyp\*\*\*\*|The ID of the scaling group. |
|LifecycleHookName|String|No|lifecyclehook\*\*\*\*|The name of the lifecycle hook. |
|LifecycleHookId.N|RepeatList|No|ash-bp19d1032y9kij96\*\*\*\*|The ID of lifecycle hook N. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default: 1. |
|PageSize|Integer|No|50|The number of entries to return on each page. Maximum value: 50.

Default value: 50. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|LifecycleHooks|Array of LifecycleHook| |Details about the lifecycle hooks. |
|LifecycleHook| | | |
|DefaultResult|String|CONTINUE|The action that the scaling group takes when the lifecycle hook times out. |
|HeartbeatTimeout|Integer|60|The wait period before the lifecycle hook times out. When the lifecycle hook times out, the scaling group performs the default action. |
|LifecycleHookId|String|ash-bp19d1032y9kij96\*\*\*\*|The ID of the lifecycle hook. |
|LifecycleHookName|String|lifecyclehook\*\*\*\*|The name of the lifecycle hook. |
|LifecycleTransition|String|SCALE\_OUT|The type of the scaling activity to which the lifecycle hook applies. |
|NotificationArn|String|acs:ess:cn-beijing:161456884340\*\*\*\*:null/null|The Alibaba Cloud Resource Name \(ARN\) of the notification object that Auto Scaling uses to notify you when ECS instances are put into the wait state by the lifecycle hook. The following list describes the formats of this parameter:

-   When no notification is set, the format of this parameter is acs:ess:\{region-id\}:\{account-id\}:null/null.
-   When the notification method is set to MNS queue, the format of this parameter is acs:mns:\{region-id\}:\{account-id\}:queue/\{queuename\}.
-   When the notification method is set to MNS topic, the format of this parameter is acs:mns:\{region-id\}:\{account-id\}:topic/\{topicname\}.
-   When the notification method is set to Operation Orchestration Service \(OOS\) template, the format of this parameter is acs:oos:\{region-id\}:\{account-id\}:template/\{templatename\}.

The variables in the preceding parameter formats have the following meanings:

-   region-id: the region ID of the scaling group
-   account-id: the ID of the Alibaba Cloud account
-   queuename: the name of the MNS queue
-   topicname: the name of the MNS topic
-   templatename: the name of the OOS template |
|NotificationMetadata|String|Test Lifecycle Hook.|The fixed string to include when Auto Scaling sends a notification about the wait state of a scaling activity. |
|ScalingGroupId|String|asg-bp1igpak5ft1flyp\*\*\*\*|The ID of the scaling group. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|50|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Integer|1|The total number of lifecycle hooks. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DescribeLifecycleHooks
&ScalingGroupId=asg-bp1igpak5ft1flyp****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeLifecycleHooksResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
    <PageNumber>1</PageNumber>
    <PageSize>50</PageSize>
    <TotalCount>1</TotalCount>
    <LifecycleHooks>
        <LifecycleHook>
            <ScalingGroupId>asg-bp1igpak5ft1flyp****</ScalingGroupId>
            <LifecycleHookId>ash-bp19d1032y9kij96****</LifecycleHookId>
            <LifecycleHookName>lifecyclehook****</LifecycleHookName>
            <DefaultResult>CONTINUE</DefaultResult>
            <HeartbeatTimeout>60</HeartbeatTimeout>
            <LifecycleTransition>SCALE_OUT</LifecycleTransition>
            <NotificationMetadata>Test Lifecycle Hook. </NotificationMetadata>
            <NotificationArn>acs:ess:cn-beijing:161456884340****:null/null</NotificationArn>
        </LifecycleHook>
    </LifecycleHooks>
</DescribeLifecycleHooksResponse>
```

`JSON` format

```
{
    "RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "PageNumber":"1",
    "PageSize":"50",
    "TotalCount":"1",
    "LifecycleHooks":{
        "LifecycleHook":{
            "ScalingGroupId":"asg-bp1igpak5ft1flyp****",
            "LifecycleHookId":"ash-bp19d1032y9kij96****",
            "LifecycleHookName":"lifecyclehook****",
            "DefaultResult":"CONTINUE",
            "HeartbeatTimeout":"60",
            "LifecycleTransition":"SCALE_OUT",
            "NotificationMetadata":"Test Lifecycle Hook.",
            "NotificationArn":"acs:ess:cn-beijing:161456884340****:null/null"
        }
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

|InvalidParamter

|The specified value of parameter is not valid.

|The error message returned because the specified parameter is invalid. |

