# SetInstancesProtection {#doc_api_Ess_SetInstancesProtection .reference}

保护或者停止保护伸缩组内的一台或者多台 ECS 实例（SetInstancesProtection）。

## 描述 {#description .section}

ECS 实例开启保护状态后：

-   实例保持此状态，直至您停止保护状态。
-   由于伸缩组内实例数量的变化和监控任务触发的自动缩容的伸缩活动不会移除处于保护状态的 ECS 实例。您需要自行 [移出ECS实例](~~25955~~) 后才能释放实例。
-   ECS 实例被停止或者重启，不会更新 ECS 实例的健康检查状态。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=SetInstancesProtection)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId.N|RepeatList|是|i-28wt4\*\*\*\*|ECS 实例 ID，N 的取值范围为 1~20。

 |
|ProtectedFromScaleIn|Boolean|是|true|伸缩组自动缩容时是否保护 ECS 实例而使其不被终止或移出伸缩组。取值范围：

 -   true
-   false

 |
|ScalingGroupId|String|是|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组 ID。

 |
|Action|String|否|SetInstancesProtection|系统规定参数。取值：SetInstancesProtection。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=SetInstancesProtection
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&InstanceId.1=i-28wt4****
&InstanceId.2=i-28wt4****
&ProtectedFromScaleIn=true
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<SetInstancesProtectionResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</SetInstancesProtectionResponse>

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
|400

|IncorrectScalingGroupStatus

|The current status of the specified scaling group does not support this action.

|您需要启用伸缩组。

|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|您还未被授权使用 SetInstancesProtection 接口

|
|404

|InvalidInstanceId.NotFound

|Instance “XXX” does not exist.

|指定的 ECS 实例不存在。

|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|指定的伸缩组不存在。

|

