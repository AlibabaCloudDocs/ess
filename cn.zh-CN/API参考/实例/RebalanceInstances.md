# RebalanceInstances {#doc_api_Ess_RebalanceInstances .reference}

重新平衡多可用区伸缩组内 ECS 实例分布（RebalanceInstances）。

## 描述 {#description .section}

分布再平衡会通过新建 ECS 实例替换已有 ECS 实例补偿平衡可用区，终止已有 ECS 实例前会先启动新 ECS 实例，分布再平衡不会影响您的应用程序性能或可用性。

-   只支持设置了 `MultiAZPolic=Balance` 的多可用区伸缩组内 ECS 实例分布不平衡时，可以重新平衡可用区。
-   只有伸缩组内实例分布严重不平衡时可以执行再平衡操作。
-   一次分布再平衡活动最多只替换 20 台 ECS 实例。
-   分布再平衡活动期间，当该组接近或达到指定的最大 ECS 实例台数（`MaxSize`）时，并需要继续分布再平衡时，我们允许可以暂时超出伸缩组的容量的 10 %，最低允许超出 1 台 ECS 实例。该超出状态持续重新平衡该伸缩组所需的时间，通常为 1 至 6 分钟。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=RebalanceInstances)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ScalingGroupId|String|是|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组 ID。

 |
|Action|String|否|RebalanceInstances|系统规定参数。取值： RebalanceInstances。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |
|ScalingActivityId|String|asa-kjgffgdfadah\*\*\*\*|伸缩活动 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=RebalanceInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RebalanceInstancesResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
  <ScalingActivityId>asa-kjgffgdfadah****</ScalingActivityId>
</RebalanceInstancesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"ScalingActivityId":"asa-kjgffgdfadah****"
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
|400

|OperationDenied

|This operation is denied because the specified scaling group does not support this action.

|指定伸缩组的扩缩容策略 MultiAZPolicy 不是 Balance，或者 ECS 实例分布不存在严重不平衡的情况。

|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|您还未被授权使用 RebalanceInstances 接口。

|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|指定的伸缩组在该用户账号下不存在。

|

