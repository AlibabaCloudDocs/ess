# DescribeRegions

You can call this operation to query the regions where Auto Scaling is available.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeRegions&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeRegions|The operation that you want to perform. Set the value to DescribeRegions. |
|AcceptLanguage|String|No|zh-CN|The language that is used as a filter condition to filter returned results. For more information, see [RFC 7231](https://tools.ietf.org/html/rfc7231). Valid values:

-   zh-CN: Chinese
-   en-US: English
-   ja: Japanese

Default value: zh-CN. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Regions|Array of Region| |Details about the regions. |
|Region| | | |
|ClassicUnavailable|Boolean|false|Indicates whether the region supports scaling groups of the classic network type. Valid values:

-   true: The region does not support scaling groups of the classic network type.
-   false: The region supports scaling groups of the classic network type. |
|LocalName|String|China \(Beijing\)|The name of the region. |
|RegionEndpoint|String|ess.aliyuncs.com|The endpoint of the region. |
|RegionId|String|cn-beijing|The region ID. |
|VpcUnavailable|Boolean|false|Indicates whether the region supports scaling groups of the VPC type. Valid values:

-   true: The region does not support scaling groups of the VPC type.
-   false: The region supports scaling groups of the VPC type. |
|RequestId|String|73469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DescribeRegions
&AcceptLanguage=zh-CN
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeRegionsResponse> 
      <RequestId>38EC7366-F5A9-46B1-BDB1-0FDC2E296397</RequestId>
      <Regions>
            <Region>
                  <ClassicUnavailable>false</ClassicUnavailable>
                  <RegionId>cn-beijing</RegionId>
                  <VpcUnavailable>false</VpcUnavailable>
                  <RegionEndpoint>ess.aliyuncs.com</RegionEndpoint>
                  <LocalName>China (Beijing)</LocalName>
            </Region>
            <Region>
                  <ClassicUnavailable>false</ClassicUnavailable>
                  <RegionId>cn-shanghai</RegionId>
                  <VpcUnavailable>false</VpcUnavailable>
                  <RegionEndpoint>ess.aliyuncs.com</RegionEndpoint>
                  <LocalName>China (Shanghai)</LocalName>
            </Region>
      </Regions>
</DescribeRegionsResponse>
```

`JSON` format

```
{
    "RequestId":"38EC7366-F5A9-46B1-BDB1-0FDC2E296397",
    "Regions":{
        "Region":[
            {
                "ClassicUnavailable": false,
                "RegionId":"cn-beijing",
                "VpcUnavailable": false,
                "RegionEndpoint":"ess.aliyuncs.com",
                "LocalName":"China (Beijing)"
            },
            {
                "ClassicUnavailable": false,
                "RegionId":"cn-shanghai",
                "VpcUnavailable": false,
                "RegionEndpoint":"ess.aliyuncs.com",
                "LocalName":"China (Shanghai)"
            }
        ]
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|404

|InvalidAcceptLanguage.NotFound

|Only Chinese \(zh-CN\), English \(en-US\), and Japanese \(ja\) are allowed.

|The error message returned because the specified language is not supported. |

