# DescribeNotificationConfigurations {#doc_api_Ess_DescribeNotificationConfigurations .reference}

调用DescribeNotificationConfigurations查询您创建的弹性伸缩事件及资源变化通知。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DescribeNotificationConfigurations&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ScalingGroupId|String|是|AG6CQdPU8OKdwLjgZcJ\*\*\*\*|伸缩组的ID。

 |
|Action|String|否|DescribeNotificationConfigurations|系统规定参数。取值：DescribeNotificationConfigurations。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|NotificationConfigurationModels| | |弹性伸缩事件及资源变化通知的集合。

 |
|NotificationArn|String|acs:ess:cn-hangzhou:1111111111:queue/queue1|通知对象标识符。格式为`acs:ess:{region}:{account-id}:{resource-relative-id}`，其中：

 -   region为伸缩组所在地域的ID。
-   account-id为您账号的ID。
-   resource-relative-id为通知方式。

 |
|NotificationTypes| |AUTOSCALING:SCALE\_IN\_SUCCESS|弹性伸缩事件及资源变化通知类型列表。

 |
|ScalingGroupId|String|asg-\*\*\*\*|伸缩组的ID。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

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
                  <NotificationArn>acs:ess:cn-hangzhou:1111111111:queue/qu****</NotificationArn>
                  <ScalingGroupId>asg-****</ScalingGroupId>
                  <NotificationTypes>
                        <NotificationType>AUTOSCALING:SCALE_IN_SUCCESS</NotificationType>
                        <NotificationType>AUTOSCALING:SCALE_IN_ERROR</NotificationType>
                  </NotificationTypes>
            </NotificationConfigurationModel>
            <NotificationConfigurationModel>
                  <NotificationArn>acs:ess:cn-hangzhou:1111111111:queue/qu****</NotificationArn>
                  <ScalingGroupId>asg-****</ScalingGroupId>
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
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"NotificationConfigurationModels":{
		"NotificationConfigurationModel":[
			{
				"NotificationArn":"acs:ess:cn-hangzhou:1111111111:queue/qu****",
				"ScalingGroupId":"asg-****",
				"NotificationTypes":{
					"NotificationType":[
						"AUTOSCALING:SCALE_IN_SUCCESS",
						"AUTOSCALING:SCALE_IN_ERROR"
					]
				}
			},
			{
				"NotificationArn":"acs:ess:cn-hangzhou:1111111111:queue/qu****",
				"ScalingGroupId":"asg-****",
				"NotificationTypes":{
					"NotificationType":[
						"AUTOSCALING:SCALE_IN_SUCCESS",
						"AUTOSCALING:SCALE_IN_ERROR"
					]
				}
			}
		]
	}
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
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|指定的伸缩组不存在。

|

