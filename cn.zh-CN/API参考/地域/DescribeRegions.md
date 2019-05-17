# DescribeRegions {#doc_api_Ess_DescribeRegions .reference}

调用DescribeRegions查询可以使用弹性伸缩服务的地域。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ess&api=DescribeRegions)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AcceptLanguage|String|否|zh-CN|根据所选语言筛选返回结果。更多详情，请参见[RFC7231](https://tools.ietf.org/html/rfc7231)。取值范围：

 -   **zh-CN**：根据汉语筛选
-   **en-US**：根据英语筛选
-   **ja**：根据日语筛选

 默认值：**zh-CN**。

 |
|Action|String|否|DescribeRegions|系统规定参数，取值：**DescribeRegions**。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Regions| | |地域信息的集合。

 |
|└LocalName|String|华北 2|地域名称。

 |
|└RegionEndpoint|String|ess.aliyuncs.com|地域对应的接入地址（Endpoint）。

 |
|└RegionId|String|cn-beijing|地域ID。

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

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ess)

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

