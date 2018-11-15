# Response results {#concept_25932_zh .concept}

This topic introduces the response results.

We return the results in either XML or JSON format, but JSON is the default choice. You can switch to XML schema by specifying the request parameter `Format`. For more information, see [common parameters](reseller.en-US/API-Reference/Common parameters.md#).

**Note:** Response examples in our API documents have line breaks and indentions to make them easy to read. The actual response results are not formatted.

## Success response example {#section_t2p_gt2_sfb .section}

Every successful response has a request ID in the RequestId element and other API-specific response parameters. The HTTP status code for a success response is 2XX.

`XML` format:

```
<? xml version="1.0" encoding="UTF-8"? > <! --Result root node-->
<ActionResponse> <! --Response request tag->
    <RequestId>4C467B38-3910-447D-87BC-AC049166F223</RequestId> <! --Response result data-->
</ActionResponse>
```

`JSON` format:

```
{
    "RequestId": "4C467B38-3910-447D-87BC-AC049166F223" /* Response result data */
}
```

## Error response example {#section_evj_mt2_sfb .section}

Every error response consists of a request ID in the RequestId element and access endpoint in the HostId element, the error code, and the error message. The HTTP status code for an error response is 4xx or 5xx.

You can fix the exception according to the API-specific error codes or [common error codes](#) and try the request again. Alternatively, you can open a ticket and provide additional inputs such as the `HostId` and `RequestId` to get technical support from us.

`XML` format:

```
<? xml version="1.0" encoding="UTF-8"? ><! --Result root node-->
<Error>
    <RequestId>540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx</RequestId> <! --Request ID-->
    <HostId>ess.aliyuncs.com</HostId> <! --Endpoint-->
    <Code>InternalError</Code> <! --Error code-->
    <Message>The request processing has failed due to some unknown error, exception or failure. </Message> <! --Error message-->
</Error>
```

`JSON` format:

```
{
    "RequestId": "540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx", /* Request ID */
    "HostId": "ess.aliyuncs.com", /* Endpoint */
    "Code": "InternalError", /* Error code */
    "Message": "The request processing has failed due to some unknown error, exception or failure." /* Error message */
}
```

## Common error codes {#section_d1v_wt2_sfb .section}

|Error code|Error message|HTTP status code|Description|
|:---------|:------------|:---------------|:----------|
|InvalidAccessKeyId.NotFound|The Access Key ID provided does not exist in our records.|400|The specified AccessKey does not exist.|
|InvalidParameter|The specified value of parameter <parameter name\> is not valid.|400|The specified parameter is invalid.|
|MissingParameter|The input parameter <parameter name\> that is mandatory for processing this request is not supplied.|400|You must specify the required parameters.|
|NoSuchVersion|The specified version does not exist.|400|The specified API version does not exist.|
|ResourceNotAvailable|Resource you requested is not available in this region or zone.|400|ESS service is unavailable in the specified region.|
|Throttling|Request was denied due to request throttling.|400|You have made too many frequent requests in short time. Please try again later.|
|UnsupportedOperation|The specified action is not supported.|400|Unable to call the specified API.|
|Forbidden|Users are not authorized to operate on the specified resource.|403|You cannot perform the specified action.|
|Forbidden.RiskControl|This operation is forbidden by Aliyun Risk Control system.|403|The specified action is under risk control.|
|Forbidden.Unsubscribed|Do not have permission to access this API.|403|You must enable the ESS service before calling this API.|
|Forbidden.UserVerification|Your user account is not verified by Aliyun.|403|You must complete the real-name registration.|
|SignatureDoesNotMatch|The signature we calculated does not match the one you provided.|403|The signature calculated by us is different from the one you provide.|
|InternalError|The request processing has failed due to some unknown error, exception or failure.|500|Internal error.|
|ServiceUnavailable|The request has failed due to a temporary failure of the server.|503|The server cannot respond to your request. Please try again later.|

