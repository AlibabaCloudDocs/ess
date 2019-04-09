# DescribeNotificationConfigurations {#doc_api_1163768 .reference}

查询您创建的弹性伸缩事件及资源变化通知（\`DescribeNotificationConfigurations\`）。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=DescribeNotificationConfigurations)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ScalingGroupId|String|是|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组 ID。

 |
|Action|String|否|DescribeNotificationConfigurations|系统规定参数。取值：DescribeNotificationConfigurations。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|NotificationConfigurationModels| | |事件及资源变化通知集合。

 |
|└NotificationArn|String|acs:ess:cn-hangzhou:1111111111:queue/queue1|事件及资源变化通知集合。

 |
|└NotificationTypes| |AUTOSCALING:SCALE\_IN\_SUCCESS|弹性伸缩事件及资源变化通知类型列表。

 |
|└ScalingGroupId|String|asg-\*\*\*\*|请求 ID。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DescribeNotificationConfigurations
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeNotificationConfigurationsResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
  <NotificationConfigurationModels>
    <NotificationConfigurationModel>
      <NotificationArn>xxxxxxxxx</NotificationArn>
      <ScalingGroupId>xxxxxxxxxxx</ScalingGroupId>
      <NotificationTypes>
        <NotificationType>AUTOSCALING:SCALE_IN_SUCCESS</NotificationType>
        <NotificationType>AUTOSCALING:SCALE_IN_ERROR</NotificationType>
      </NotificationTypes>
    </NotificationConfigurationModel>
    <NotificationConfigurationModel>
      <NotificationArn>xxxxxxxxx</NotificationArn>
      <ScalingGroupId>xxxxxxxxxx</ScalingGroupId>
      <NotificationTypes>
        <NotificationType>AUTOSCALING:SCALE_IN_SUCCESS</NotificationType>
        <NotificationType>AUTOSCALING:SCALE_IN_ERROR</NotificationType>
      </NotificationTypes>
    </NotificationConfigurationModel>
  </NotificationConfigurationModels>
</DescribeNotificationConfigurationsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"notificationConfigurationModels":[
		{
			"notificationArn":"xxxxxxxxxx",
			"notificationTypes":[
				"AUTOSCALING:SCALE_OUT_SUCCESS",
				"AUTOSCALING:SCALE_OUT_ERROR",
				"AUTOSCALING:SCALE_IN_SUCCESS",
				"AUTOSCALING:SCALE_IN_ERROR",
				"AUTOSCALING:SCALE_REJECT"
			],
			"scalingGroupId":"xxxxxxxxxx"
		},
		{
			"notificationArn":"xxxxxxxxxx",
			"notificationTypes":[
				"AUTOSCALING:SCALE_OUT_SUCCESS",
				"AUTOSCALING:SCALE_OUT_ERROR",
				"AUTOSCALING:SCALE_IN_SUCCESS",
				"AUTOSCALING:SCALE_IN_ERROR",
				"AUTOSCALING:SCALE_REJECT"
			],
			"scalingGroupId":"xxxxxxxxxx"
		}
	]
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

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|指定的伸缩组不存在。

|

