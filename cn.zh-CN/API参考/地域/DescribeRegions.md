# DescribeRegions {#doc_api_Ess_DescribeRegions .reference}

调用DescribeRegions查询可以使用弹性伸缩服务的地域。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DescribeRegions&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AcceptLanguage|String|否|zh-CN|根据所选语言筛选返回结果，更多详情请参见[RFC7231](https://tools.ietf.org/html/rfc7231)，取值范围：

 -   zh-CN：根据汉语筛选
-   en-US：根据英语筛选
-   ja：根据日语筛选

 默认值：zh-CN。

 |
|Action|String|否|DescribeRegions|系统规定参数，取值：DescribeRegions。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Regions| | |地域信息的集合。

 |
|LocalName|String|华北 2|地域名称。

 |
|RegionEndpoint|String|ess.aliyuncs.com|地域对应的接入地址（Endpoint）。

 |
|RegionId|String|cn-beijing|地域ID。

 |
|RequestId|String|73469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ess.aliyuncs.com/?Action=DescribeRegions
&AcceptLanguage=zh-CN&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeRegionsResponse>
    <RequestId>38EC7366-F5A9-46B1-BDB1-0FDC2E296397</RequestId>
    <Regions>
        <Region>
            <RegionId>cn-beijing</RegionId>
            <RegionEndpoint>ess.aliyuncs.com</RegionEndpoint>
            <LocalName>华北 2</LocalName>
        </Region>
        <Region>
            <RegionId>cn-shanghai</RegionId>
            <RegionEndpoint>ess.aliyuncs.com</RegionEndpoint>
            <LocalName>华东 2</LocalName>
        </Region>
    </Regions>
</DescribeRegionsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"38EC7366-F5A9-46B1-BDB1-0FDC2E296397",
	"Regions":{
		"Region":[
			{
				"RegionId":"cn-beijing",
				"RegionEndpoint":"ess.aliyuncs.com",
				"LocalName":"华北 2"
			},
			{
				"RegionId":"cn-shanghai",
				"RegionEndpoint":"ess.aliyuncs.com",
				"LocalName":"华东 2"
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

|InvalidAcceptLanguage.NotFound

|Only Chinese \(zh-CN\), English \(en-US\), and Japanese \(ja\) are allowed.

|不支持指定的语言。

|

