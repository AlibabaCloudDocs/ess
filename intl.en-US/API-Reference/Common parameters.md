# Common parameters {#concept_25929_zh .concept}

This topic describes the common parameters.

Common parameters include the [common request parameters](#) and the [common request parameters](#hxsix).

## Common request parameters {#section_m5s_5p2_sfb .section}

The following table describes the common parameters that comprise of a URL for a GET request over HTTP or HTTPS protocol.

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The target API.|
|AccessKeyId|String|Yes|Equivalent to a logon password. However, an AccessKey is used to call APIs, while logon password is used to log on to the [console](https://partners-intl.console.aliyun.com/#/ess). For more information, see [Create an AccessKey](../../../../reseller.en-US/General Reference/Create an AccessKey.md#).|
|Signature|String|Yes|Your signature. For more information, see [signatures](reseller.en-US/API-Reference/Signatures.md#).|
|SignatureMethod|String|Yes|Signature method. Value: HMAC-SHA1.|
|SignatureVersion|String|Yes|Signature algorithm version. Value: 1.0.|
|SignatureNonce|String|Yes|Unique random number, which is used to prevent network replay attacks. Different random numbers must be used for different requests.|
|Timestamp|String|Yes|Request time stamp. Use the offset from Coordinated Universal Time \(UTC\), the time display is based on ISO8601. Format: YYYY-MM-DDThh:mm:ssZ. For example, `2018-01-01T12:00:00Z` indicates 20:00:00, Jan 01, 2018, Beijing time \(UTC+8\).

|
|Version|String|Yes|The API version to use. Value: 2014-08-28.|
|Format|String|No|Type of the response parameters. Optional values: json | xml. Default value: json.|

## Request example { .section}

```
https://ess.aliyuncs.com/?Action=XXXXXX
&Format=xml
&Version=2014-08-28
&Signature=Pc5WB8gokVn0xfeu%2FZV%2BiNM1dgI%3D
&SignatureMethod=HMAC-SHA1
&SignatureNonce=15215528852396
&SignatureVersion=1.0
&AccessKeyId=key-test
&Timestamp=2018-01-01T12:00:00Z
…
```

## Common response parameter {#hxsix .section}

|Name|Type|Description|
|:---|:---|:----------|
|RequestId|String|The request ID. We return a unique RequestId for every API request, whether the request is successful or not.|

