# CompleteLifecycleAction

调用CompleteLifecycleAction提前结束伸缩活动的等待状态。

## 接口说明

允许设置结束等待状态后的下一步动作是继续完成伸缩活动（CONTINUE），还是弃用此次伸缩活动（ABANDON）。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=CompleteLifecycleAction&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CompleteLifecycleAction|系统规定参数。取值：CompleteLifecycleAction |
|LifecycleActionToken|String|是|aaaa-bbbbb-cccc-ddddd|伸缩活动的等待状态标识符，您可以从生命周期挂钩指定的消息服务队列或主题中获取该值。 |
|LifecycleHookId|String|是|ash-bp14g3ee6bt3sc98\*\*\*\*|生命周期挂钩的ID。 |
|LifecycleActionResult|String|否|CONTINUE|生命周期挂钩等待状态结束后的下一步动作。取值范围：

 -   CONTINUE：继续响应弹性扩张活动，将ECS实例添加至伸缩组；继续响应弹性收缩活动，将ECS实例从伸缩组移除。
-   ABANDON：终止弹性扩张活动，直接释放创建出来的ECS实例；继续响应弹性收缩活动，将ECS实例从伸缩组移除。

 默认值：CONTINUE

 伸缩组中存在多个生命周期挂钩时同步触发，最终的下一步动作如下：

 -   对弹性收缩活动，在ABANDON类型生命周期挂钩触发的等待状态结束时，会将提前结束后续生命周期挂钩的等待状态，将ECS实例从伸缩组移除。
-   在挂起弹性收缩活动的生命周期挂钩类型为CONTINUE时，或者对弹性扩张活动，后续生命周期挂钩会继续挂起伸缩活动，直到最后一个生命周期挂钩触发的等待状态结束。最终的下一步动作以最后一个结束等待状态的生命周期挂钩类型为准。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25965~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=CompleteLifecycleAction
&LifecycleHookId=ash-bp14g3ee6bt3sc98****
&LifecycleActionToken=aaaa-bbbbb-cccc-ddddd
&LifecycleActionResult=CONTINUE
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CompleteLifecycleActionResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</CompleteLifecycleActionResponse>
```

`JSON` 格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ess)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|400

|InvalidParamter

|The specified value of parameter is invalid.

|指定的参数值不合法。 |
|400

|LifecycleHookIdAndLifecycleActionToken.Invalid

|The specified lifecycleActionToken and lifecycleHookId you provided does not match any in process lifecycle action.

|根据指定的LifecycleActionToken无法匹配LifecycleHookId。 |

