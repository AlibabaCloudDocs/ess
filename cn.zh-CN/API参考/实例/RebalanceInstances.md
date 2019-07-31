# RebalanceInstances {#doc_api_Ess_RebalanceInstances .reference}

调用RebalanceInstances重新平衡多可用区伸缩组内ECS实例的分布。

## 接口说明 {#description .section}

分布再平衡会通过新建ECS实例替换已有ECS实例补偿平衡可用区，终止已有ECS实例前会先启动新ECS实例，分布再平衡不会影响您的应用程序性能或可用性。

-   只支持设置了MultiAZPolicy为BALANCE的多可用区伸缩组，用于平衡多可用区间ECS实例的分布。
-   只有伸缩组内实例分布严重不平衡时可以执行再平衡操作。
-   一次分布再平衡活动最多只替换20台ECS实例。
-   分布再平衡活动期间，如果组内实例数量接近或达到指定的最大ECS实例台数（MaxSize），但需要继续分布再平衡，弹性伸缩允许暂时超出MaxSize的10%，最低允许超出1台ECS实例。该超出状态持续重新平衡该伸缩组所需的时间，通常为1至6分钟。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=RebalanceInstances&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ScalingGroupId|String|是|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组的ID。

 |
|Action|String|否|RebalanceInstances|系统规定参数，取值： RebalanceInstances。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |
|ScalingActivityId|String|asa-kjgffgdfadah\*\*\*\*|伸缩活动的ID。

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

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

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

|指定伸缩组的扩缩容策略MultiAZPolicy不是BALANCE，或者ECS实例分布不存在严重不平衡的情况。

|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|您还未被授权使用RebalanceInstances接口。

|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|指定的伸缩组在该用户账号下不存在。

|

