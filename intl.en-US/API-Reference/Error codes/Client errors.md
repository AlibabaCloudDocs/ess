# Client errors {#concept_25963_zh .concept}

This topic describes the client errors.

|Error message|Error code|Description|HTTP status code|
|:------------|:---------|:----------|:---------------|
|The parameter is missing.|MissingParameter|The input parameter `<parameter name>` that is mandatory for processing this request is not supplied|400|
|The parameter value is invalid.|InvalidParameter|The specified value of parameter `<parameter name>` is not valid.|400|
|The interface is invalid.|UnsupportedOperation|The specified action is not supported.|400|
|The version is invalid.|NoSuchVersion|The specified version does not exist.|400|
|The operation is rejected by the traffic control system.|Throttling|Request was denied due to request throttling.|400|
|The AccessKey is invalid.|InvalidAccessKeyId.NotFound|The AccessKey ID provided does not exist in our records.|400|
|The operation is forbidden.|Forbidden|Users are not authorized to operate on the specified resource.|403|
|The operation is forbidden by the risk control system.|Forbidden.RiskControl|This operation is forbidden by Aliyun Risk Control system.|403|
|The signature is invalid.|SignatureDoesNotMatch|The signature we calculated does not match the one you provided.|403|
|Auto Scaling is not activated and thus the API cannot be called.|Forbidden.Unsubscribed|Do not have permission to access this API.|403|
|Real-name verification is missing.|Forbidden.UserVerification|Your user account is not verified by Aliyun.|403|
|Auto Scaling is not supported by the specified region.|ResourceNotAvailable|Resource you requested is not available in this region or zone.|400|

