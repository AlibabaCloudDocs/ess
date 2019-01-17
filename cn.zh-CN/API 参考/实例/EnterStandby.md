# EnterStandby {#concept_69678_zh .concept}

设置伸缩组内的ECS实例为备用状态（`EnterStandby`）。

## 描述 {#section_e1k_3ll_lgb .section}

如果伸缩组设置了负载均衡，则会把负载均衡对应的实例权重设置为0。

-   当实例处于备用状态的时候，如果您自行移出伸缩组并释放，可以正常移出伸缩组并释放。
-   对于伸缩组数量变化或监控任务触发的自动缩容的伸缩活动，不会移除处于备用状态的实例。
-   当实例处于备用状态的时候，实例如果出现非健康状态（停止、重启等），实例的健康检查状态不会被更新，并且不会触发移除不健康实例的伸缩活动，只有实例 [退出备用状态](cn.zh-CN/API 参考/实例/ExitStandby.md#) 才会重新更新健康检查状态。

## 请求参数 { .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：EnterStandby。|
|ScalingGroupId|String|是|伸缩组ID。|
|InstanceId.N|String|是|ECS实例ID。|

## 返回参数 { .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|请求 ID。|

## 示例 { .section}

请求示例

```
http://ess.aliyuncs.com/?Action=EnterStandby
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&InstanceId.1=i-28wt48iaa
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<EnterStandbyResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</EnterStandbyResponse>
```

`JSON` 格式

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|说明|
|--------|:--|:---|:-|
|403|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|RAM用户无权限调用该接口。请联系主账号授权后重试。|
|404|InvalidInstanceId.NotFound|Instance “XXX” does not exist.|指定的ECS实例不存在。|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|指定的伸缩组不存在。|

