# DeleteScheduledTask {#concept_25960_zh .concept}

删除一个指定的伸缩规则。

## 请求参数 {#section_znf_jjl_sfb .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：DeleteScheduledTask。|
|ScheduledTaskId|String|是|定时任务的ID。|

## 返回参数 {#section_kfy_kjl_sfb .section}

[公共参数](cn.zh-CN/API 参考/公共参数.md#)。

## 示例 {#section_epb_4jl_sfb .section}

请求示例

```
http://ess.aliyuncs.com/?Action=DeleteScheduledTask
&ScheduledTaskId=edRtShc57WGXdt8TlPbrjsnV
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteScheduledTaskResponse>
    <RequestId>7683D637-CF8A-41DC-85A8-E128061E65FC</RequestId>
</DeleteScheduledTaskResponse>
```

`JSON` 格式

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 {#section_gwm_ljl_sfb .section}

对于所有接口的通用性错误，请参考 [客户端错误](cn.zh-CN/API 参考/错误代码/客户端错误.md#) 或 [服务器端错误](cn.zh-CN/API 参考/错误代码/服务器端错误.md#)。

|HttpCode|错误码|描述|错误信息|
|:-------|:--|:-|:---|
|404|InvalidScheduledTaskId.NotFound|The specified scheduled task does not exist.|指定的定时任务在该用户账号下不存在。|

