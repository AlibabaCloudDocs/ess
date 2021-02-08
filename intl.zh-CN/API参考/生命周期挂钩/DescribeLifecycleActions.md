# DescribeLifecycleActions

调用DescribeLifecycleActions查看伸缩活动对应的生命周期操作。

## 接口说明

如果发生了和生命周期挂钩适用类型一致的伸缩活动，每个生命周期挂钩都会触发一次生命周期操作，生命周期操作有三种状态：

-   Pending：挂起中。表示ECS实例仍处于挂起中状态。
-   Timeout：已超时。表示已超过生命周期挂钩的超时时间，自动结束了ECS实例的挂起中状态。
-   Completed：已处理。表示您手动提前结束了ECS实例的挂起中状态。

如果在创建生命周期挂钩时没有设置后续动作，例如在结束挂起后触发执行指定的OOS模板。您可以调用本接口获取当前伸缩活动对应生命周期操作的标识符，以便自行定制后续动作。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DescribeLifecycleActions&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeLifecycleActions|系统规定参数。取值：DescribeLifecycleActions |
|ScalingActivityId|String|是|asa-bp17mug9t0pegagw\*\*\*\*|伸缩活动的ID。 |
|LifecycleActionStatus|String|否|Pending|生命周期操作的状态。取值范围：

 -   Pending：挂起中。表示ECS实例仍处于挂起中状态。
-   Timeout：已超时。表示已到达生命周期挂钩的超时时间，自动结束ECS实例的挂起中状态。
-   Completed：已处理。表示您手动提前结束了ECS实例的挂起中状态。 |
|NextToken|String|否|AAAAAcSz4VTb1Nq\*\*\*\*|查询凭证，用于指定开始查询的位置，例如上次查询10条生命周期操作后，本次从第11条生命周期操作开始查询。取值为上次调用本接口返回的NextToken参数值，不填写取值则表示从头开始查询。 |
|MaxResults|Integer|否|1|设置单页查询的最大条目数。取值范围：1~50。

 默认值：10 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|LifecycleActions|Array of LifecycleAction| |各个生命周期挂钩对应的生命周期操作列表。 |
|LifecycleAction| | | |
|InstanceIds|List|\["i-bp11m3fzlqrgk5vh\*\*\*\*","i-bp11m3fzlqrgk5vh\*\*\*\*"\]|该生命周期挂钩挂起的ECS实例的ID列表。 |
|LifecycleActionResult|String|CONTINUE|该生命周期挂钩触发的生命周期操作结束后的下一步动作。取值范围：

 -   CONTINUE：继续响应弹性扩张活动，将ECS实例添加至伸缩组；继续响应弹性收缩活动，将ECS实例从伸缩组移除。
-   ABANDON：终止弹性扩张活动，直接释放创建出来的ECS实例；继续响应弹性收缩活动，将ECS实例从伸缩组移除。 |
|LifecycleActionStatus|String|Pending|生命周期操作的状态。 |
|LifecycleActionToken|String|9C2E9DA7-F794-449A-ACF6-CEE24444F7BB|生命周期操作的标识符。 |
|LifecycleHookId|String|ash-bp18uoft0deax0f7\*\*\*\*|生命周期挂钩的ID。 |
|MaxResults|Integer|3|单页查询的最大条目数。 |
|NextToken|String|AAAAAcSz4VTb1Nq\*\*\*\*|本次调用返回的查询凭证。 |
|RequestId|String|42A742EB-FCF3-459E-9C62-E107048C17E3|请求ID。 |
|TotalCount|Integer|3|本次查询到的生命周期操作的总数。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=DescribeLifecycleActions
&ScalingActivityId=asa-bp17mug9t0pegagw****
&MaxResults=3
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeLifecycleActionsResponse>
      <TotalCount>3</TotalCount>
      <RequestId>678A42DB-A9CE-44C7-95B0-9E4150E6308F</RequestId>
      <NextToken>AAAAAcSz4VTb****</NextToken>
      <MaxResults>3</MaxResults>
      <LifecycleActions>
            <LifecycleAction>
                  <LifecycleActionStatus>Pending</LifecycleActionStatus>
                  <LifecycleActionResult>CONTINUE</LifecycleActionResult>
                  <InstanceIds>
                        <InstanceId>i-bp11m3fzlqrgk5vh****</InstanceId>
                        <InstanceId>i-bp11m3fzlqrgk5vh****</InstanceId>
                  </InstanceIds>
                  <LifecycleActionToken>9C2E9DA7-F794-449A-ACF6-CEE24444F7BB</LifecycleActionToken>
                  <LifecycleHookId>ash-bp16ed9xxytrxdlt****</LifecycleHookId>
            </LifecycleAction>
            <LifecycleAction>
                  <LifecycleActionStatus>Pending</LifecycleActionStatus>
                  <LifecycleActionResult>CONTINUE</LifecycleActionResult>
                  <InstanceIds>
                        <InstanceId>i-bp11m3fzlqrgk5vh****</InstanceId>
                        <InstanceId>i-bp11m3fzlqrgk5vh****</InstanceId>
                  </InstanceIds>
                  <LifecycleActionToken>35D11A1F-A2CF-4B6E-B164-B19CC94D1A33</LifecycleActionToken>
                  <LifecycleHookId>ash-bp18uoft0deax0f7****</LifecycleHookId>
            </LifecycleAction>
            <LifecycleAction>
                  <LifecycleActionStatus>Pending</LifecycleActionStatus>
                  <LifecycleActionResult>CONTINUE</LifecycleActionResult>
                  <InstanceIds>
                        <InstanceId>i-bp11m3fzlqrgk5vh****</InstanceId>
                        <InstanceId>i-bp11m3fzlqrgk5vh****</InstanceId>
                  </InstanceIds>
                  <LifecycleActionToken>25547B8D-05D8-44D7-84D4-3E594556CAD3</LifecycleActionToken>
                  <LifecycleHookId>ash-bp18uoft0deayjo2****</LifecycleHookId>
            </LifecycleAction>
      </LifecycleActions>
</DescribeLifecycleActionsResponse>
```

`JSON`格式

```
{
	"TotalCount": 3,
	"RequestId": "678A42DB-A9CE-44C7-95B0-9E4150E6308F",
	"NextToken": "AAAAAcSz4VTb****",
	"MaxResults": 3,
	"LifecycleActions": {
		"LifecycleAction": [
			{
				"LifecycleActionStatus": "Pending",
				"LifecycleActionResult": "CONTINUE",
				"InstanceIds": {
					"InstanceId": [
						"i-bp11m3fzlqrgk5vh****",
						"i-bp11m3fzlqrgk5vh****"
					]
				},
				"LifecycleActionToken": "9C2E9DA7-F794-449A-ACF6-CEE24444F7BB",
				"LifecycleHookId": "ash-bp16ed9xxytrxdlt****"
			},
			{
				"LifecycleActionStatus": "Pending",
				"LifecycleActionResult": "CONTINUE",
				"InstanceIds": {
					"InstanceId": [
						"i-bp11m3fzlqrgk5vh****",
						"i-bp11m3fzlqrgk5vh****"
					]
				},
				"LifecycleActionToken": "35D11A1F-A2CF-4B6E-B164-B19CC94D1A33",
				"LifecycleHookId": "ash-bp18uoft0deax0f7****"
			},
			{
				"LifecycleActionStatus": "Pending",
				"LifecycleActionResult": "CONTINUE",
				"InstanceIds": {
					"InstanceId": [
						"i-bp11m3fzlqrgk5vh****",
						"i-bp11m3fzlqrgk5vh****"
					]
				},
				"LifecycleActionToken": "25547B8D-05D8-44D7-84D4-3E594556CAD3",
				"LifecycleHookId": "ash-bp18uoft0deayjo2****"
			}
		]
	}
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

|InvalidParameter

|The specified value of parameter "ScalingActivityId" is not valid.

|指定的参数无效。 |
|400

|InvalidParameter

|The specified value of parameter "MaxResults" is not valid.

|指定的参数无效。 |
|400

|InvalidParameter

|The specified value of parameter "LifecycleActionStatus" is not valid.

|指定的参数无效。 |

