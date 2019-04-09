# ModifyScheduledTask {#doc_api_Ess_ModifyScheduledTask .reference}

修改定时任务的属性。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=ModifyScheduledTask)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ScheduledTaskId|String|是|edRtShc57WGXdt8TlPbr\*\*\*\*|定时任务的 ID。

 |
|Action|String|否|ModifyScheduledTask|操作接口名，系统规定参数，取值：ModifyScheduledTask。

 |
|Description|String|否|fortest|定时任务的描述信息。2~200 个英文或中文字符。

 |
|LaunchExpirationTime|Integer|否|600|定时任务触发操作失败后，在此时间内重试。 默认 600 秒。

 取值范围：0~21600

 |
|LaunchTime|String|否|2014-08-18T10:52Z|定时任务触发的时间点。 按照 ISO8601 标准表示，并需要使用 UTC 时间。格式为：YYYY-MM-DDThh:mmZ。

 如果指定了 RecurrenceType，则此属性指定的时间点，默认为循环执行的时间点。

 如果未指定 RecurrenceType，则按指定的日期和时间执行一次。 不能填写自创建或修改当天起 90 日后的时间。

 |
|RecurrenceEndTime|String|否|2014-08-20T16:55Z|重复执行定时任务的结束时间。按照 ISO8601 标准表示，并需要使用 UTC 时间。格式为：YYYY-MM-DDThh:mmZ

 不能填写自创建或修改当天起 90 日后的时间。

 修改后，RecurrenceType、RecurrenceValue 和 RecurrenceEndTime 需要同时有效。

 |
|RecurrenceType|String|否|Daily|重复执行定时任务的类型。可选值：

 -   Daily：每多少天重复执行一次定时任务。
-   Weekly：每周指定几天重复执行一次定时任务。
-   Monthly：每月内指定几天重复执行一次定时任务。
-   Cron：按照指定的 Cron 表达式执行定时任务。

 修改后，RecurrenceType、RecurrenceValue 和 RecurrenceEndTime 需要同时有效。

 |
|RecurrenceValue|String|否|2|重复执行定时任务的数值。

 -   Daily：只能填一个值，取值范围：1~31。
-   Weekly：可以填入多值。周日、周一……周六的值依次为：0, 1,2,…, 6，多天使用英文字符 “,” 分隔。
-   Monthly：格式为 A-B。A、B 的取值范围为 1~31 ，并且 B 必须大于等于 A。
-   Cron：支持分、时、日、月、星期的 5 域表达式，支持英文逗号（,）、连词符（-）、星号（\*）、斜线（/）。

 修改后，RecurrenceType、RecurrenceValue 和 RecurrenceEndTime 需要同时有效。

 |
|ScheduledAction|String|否|ari:acs:ess:cn-qingdao:1344371:scalingRule/cCBpdYdQuBe2cUxOdu6piOk|定时任务触发时需要执行的操作。此处填写伸缩规则的唯一标识符。

 |
|ScheduledTaskName|String|否|测试st|定时任务的显示名称，2~64 个英文或中文字符，以数字、大小字母或中文开头，可包含数字，“\_”、“-” 或 “.”。 同一用户账号同一地域内唯一。如果没有指定该参数，默认值为 ScheduledScalingTaskId。

 |
|TaskEnabled|Boolean|否|true|是否启动定时任务。

 -   true：启动任务
-   false：停止任务

 默认值：true

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=ModifyScheduledTask
&ScheduledTaskId=edRtShc57WGXdt8TlPbr****
&LaunchTime=2014-08-18T10:52Z
&RecurrenceEndTime=2014-08-20T16:55Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyScheduledTaskResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyScheduledTaskResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ess)

|HttpCode

|错误码

|错误信息

|描述

|
|----------|-----|------|----|
|404

|InvalidScheduledTaskId.NotFound

|The specified scheduled task does not exist.

|指定的定时任务在该用户账号下不存在。

|
|400

|InvalidScheduledTaskName.Duplicate

|The specified value of parameter

`ScheduledTaskName`is duplicated.

|定时任务名已存在。

|
|400

|ScheduledAction.RegionMismatch

|The specified scheduled task and the specified scheduled action are not in the same Region.

|指定的ScheduledAction与定时任务所在的地域不匹配。

|

