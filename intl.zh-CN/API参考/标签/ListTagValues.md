# ListTagValues

调用ListTagValues查询弹性伸缩资源标签键对应的标签值。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=ListTagValues&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListTagValues|系统规定参数。取值：ListTagValues |
|Key|String|是|ESS|标签键。 |
|RegionId|String|是|cn-hangzhou|弹性伸缩资源所属地域的ID。 |
|ResourceType|String|是|scalinggroup|弹性伸缩资源类型。取值：scalinggroup，表示标签绑定的对象是伸缩组。 |
|NextToken|String|否|caeba0bbb2be03f84eb48b699f0a\*\*\*\*|下一个查询开始的Token，NextToken为空表示没有下一个。 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。最大值：50。

 默认值：10 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|NextToken|String|caeba0bbb2be03f84eb48b699f0a\*\*\*\*|下一个查询开始的Token，NextToken为空表示没有下一个。 |
|PageSize|Integer|10|输入时设置的每页行数。 |
|RequestId|String|AB444F46-1CFF-4B06-B8F0-B45D3158F95B|请求ID。 |
|Values|List|Doc|标签值信息。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=ListTagValues
&RegionId=cn-hangzhou
&ResourceType=scalinggroup
&Key=ESS
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ListTagValuesResponse>
    <RequestId>178E635A-11AF-4214-A65E-50B67B3CA548</RequestId>
    <NextToken></NextToken>
    <PageSize>1</PageSize>
    <Values>
        <Value>Doc</Value>
    </Values>
</ListTagValuesResponse>
```

`JSON` 格式

```
{
	"RequestId": "178E635A-11AF-4214-A65E-50B67B3CA548",
	"NextToken": "",
	"PageSize": 1,
	"Values": {
		"Value": [
			"Doc"
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

|InvalidResourceType.NotFound

|The ResourceType provided does not exist in our records.

|资源类型参数非法。 |
|400

|InvalidTagKey.Malformed

|The specified tag key \\"%s\\" is not valid.

|指定的标签键不存在。 |

