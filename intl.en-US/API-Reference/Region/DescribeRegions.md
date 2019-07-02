# DescribeRegions {#doc_api_Ess_DescribeRegions .reference}

You can call this operation to query the regions that can use Auto Scaling.

## Debugging {#apiExplorer .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=DescribeRegions) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|AcceptLanguage|String|No|zh-CN|The language of the results returned. For more information, see [RFC7231](https://tools.ietf.org/html/rfc7231). Valid values:

 -   **zh-CN**: Chinese
-   **en-US**: English
-   **ja**: Japanese

 Default value: **zh-CN**.

 |
|Action|String|No|DescribeRegions|The operation that you want to perform. Set the value to **DescribeRegions**.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Regions| | |A collection of regions.

 |
|└LocalName|String|China \(Beijing\)|The name of a region.

 |
|└RegionEndpoint|String|ess.aliyuncs.com|The endpoint of a region.

 |
|└RegionId|String|cn-beijing|The ID of a region.

 |
|RequestId|String|73469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}

https://ess.aliyuncs.com/?Action=DescribeRegions
&AcceptLanguage=zh-CN&<Common request parameters>

```

Sample success response

`XML` format

``` {#xml_return_success_demo}
<DescribeRegionsResponse>
  <RequestId>38EC7366-F5A9-46B1-BDB1-0FDC2E296397</RequestId>
  <Regions>
    <Region>
      <RegionId>cn-beijing</RegionId>
      <RegionEndpoint>ess.aliyuncs.com</RegionEndpoint>
      <LocalName>China (Beijing)</LocalName>
    </Region>
    <Region>
      <RegionId>cn-shanghai</RegionId>
      <RegionEndpoint>ess.aliyuncs.com</RegionEndpoint>
      <LocalName>China (Shanghai)</LocalName>
    </Region>
  </Regions>
</DescribeRegionsResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"38EC7366-F5A9-46B1-BDB1-0FDC2E296397",
	"Regions":{
		"Region":[
			{
				"RegionId":"cn-beijing",
				"RegionEndpoint":"ess.aliyuncs.com",
				"LocalName":"China (Beijing)"
			},
			{
				"RegionId":"cn-shanghai",
				"RegionEndpoint":"ess.aliyuncs.com",
				"LocalName":"China (Shanghai)"
			}
		]
	}
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Ess)

|HTTP status code

|Error code

|Error message

|Description

|
|------------------|------------|---------------|-------------|
|404

|InvalidAcceptLanguage. NotFound

|Only Chinese \(zh-CN\), English \(en-US\), and Japanese \(ja\) are allowed.

|The error message returned because the specified language is not supported.

|

