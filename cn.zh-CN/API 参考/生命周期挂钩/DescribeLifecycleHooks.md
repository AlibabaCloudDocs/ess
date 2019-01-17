# DescribeLifecycleHooks {#concept_73843_zh .concept}

查询一个或多个满足指定条件的生命周期挂钩列表（`DescribeLifecycleHooks`）。

## 描述 {#section_mbd_r3l_lgb .section}

您可以通过以下三种方式查询生命周期挂钩：

-   指定一个生命周期挂钩 ID 列表（`LifecycleHookId.N`），此时将忽略 `ScalingGroupId` 和 `LifecycleHookName` 参数。
-   指定伸缩组 ID（`ScalingGroupId`）。
-   同时指定伸缩组 ID（`ScalingGroupId`）和生命周期挂钩名称（`LifecycleHookName`）。

## 请求参数 { .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DescribeLifecycleHooks|
|LifecycleHookId.N|String|否|生命周期挂钩 ID 列表，`N` 的取值范围：\[1, 50\]。|
|ScalingGroupId|String|否|伸缩组 ID。|
|LifecycleHookName|String|否|生命周期挂钩名称。|
|PageNumber|Integer|否|实例状态列表的页码。起始值：1，默认值：1。|
|PageSize|Integer|否|分页查询时设置的每页行数。最大值：50，默认值：50。|

## 返回参数 { .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|请求 ID。|
|PageNumber|Integer|查询起始页数。|
|PageSize|String|查询每页返回行数。|
|TotalCount|String|生命周期挂钩总个数。|
|LifecycleHooks| [LifecycleHookModelSet](#) |生命周期挂钩信息列表。|

## LifecycleHookModelSet {#hxone .section}

|名称|类型|描述|
|:-|:-|:-|
|ScalingGroupId|String|伸缩组 ID。|
|LifecycleHookId|String|生命周期挂钩 ID。|
|LifecycleHookName|String|生命周期挂钩名称。|
|DefaultResult|String|等待状态结束后的下一步动作。|
|HeartbeatTimeout|Integer|生命周期挂钩为伸缩组活动设置的等待时间，等待状态超时后会执行下一步动作。|
|LifecycleTransition|String|生命周期挂钩对应伸缩活动类型。|
|NotificationMetadata|String|伸缩活动的等待状态的固定字符串信息。|
|NotificationArn|String|生命周期挂钩通知对象标识符。|

## 示例 { .section}

请求示例

```
http://ess.aliyuncs.com/?Action=DescribeLifecycleHooks
&ScalingGroupId=asg-xxxxx
&<公共请求参数>
```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码 { .section}

以下为本接口特有的错误码。对于所有接口的通用性错误，请参考 [客户端错误](cn.zh-CN/API 参考/错误代码/客户端错误.md#) 或 [服务器端错误](cn.zh-CN/API 参考/错误代码/服务器端错误.md#)。

|HttpCode|错误码|错误信息|描述|
|--------|:--|:---|:-|
|400|InvalidParamter|The specified value of parameter is not valid.|指定的参数值不合法。|

