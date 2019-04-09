# DeleteScheduledTask {#doc_api_1163279 .reference}

删除一个指定的伸缩规则。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=DeleteScheduledTask)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ScheduledTaskId|String|是|edRtShc57WGXdt8TlPbr\*\*\*\*|定时任务的 ID。

 |
|Action|String|否|DeleteScheduledTask|操作接口名，系统规定参数，取值：DeleteScheduledTask。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DeleteScheduledTask
&ScheduledTaskId=edRtShc57WGXdt8TlPbr****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteScheduledTaskResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DeleteScheduledTaskResponse>

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

