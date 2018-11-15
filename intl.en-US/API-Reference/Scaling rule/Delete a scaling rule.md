# Delete a scaling rule {#concept_25951_zh .concept}

This topic describes how to delete a scaling rule using the API.

## Description {#section_xmk_skk_sfb .section}

Deletes a specified scaling rule.

## Request parameters {#section_z21_tkk_sfb .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|Operation interface, required. The parameter value is DeleteScalingRule.|
|ScalingRuleId|String|Yes|ID of a scaling rule.|

## Response parameters {#section_gfp_5kk_sfb .section}

Public parameters.

## Error code {#section_cwc_vkk_sfb .section}

For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|Error message|Error code|Description|HTTP status code|
|:------------|:---------|:----------|:---------------|
|The specified scaling rule does not exist in this account.|InvalidScalingRuleId.NotFound|The specified scaling rule does not exist.|404|

## Request example {#section_scx_ykk_sfb .section}

```
http://ess.aliyuncs.com/?Action=DeleteScalingRule
&ScalingRuleId=eMKWG8SRNb9dBLAjweNI1Ik
&<Public Request Parameters>
```

## Response example { .section}

XML format:

```
<DeleteScalingRuleResponse>
    <RequestId>F0595173-CA3A-4597-B0D3-97A07A042B9C</RequestId>
</DeleteScalingRuleResponse>
```

JSON format:

```
"RequestId": "F0595173-CA3A-4597-B0D3-97A07A042B9C"
```

