# Delete a scheduled task {#concept_25960_zh .concept}

Deletes a specified scaling rule.

## Request parameters {#section_znf_jjl_sfb .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|Operation interface name, required parameter. Value:DeleteScheduledTask.|
|ScheduledTaskId|String|Yes|ID of the scheduled task.|

## Response parameters {#section_kfy_kjl_sfb .section}

Public parameters.

## Error code {#section_gwm_ljl_sfb .section}

For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|Error message|Error code|Description|HTTP status codes|
|:------------|:---------|:----------|:----------------|
|The specified scheduled task does not exist in your account.|InvalidScheduledTaskId.NotFound|The specified scheduled task does not exist.|404|

## Request example {#section_epb_4jl_sfb .section}

```
http://ess.aliyuncs.com/?Action=DeleteScheduledTask
&ScheduledTaskId=edRtShc57WGXdt8TlPbrjsnV
&<Public Request Parameters>
```

## Response example { .section}

XML format:

```
<DeleteScheduledTaskResponse>
    <RequestId>7683D637-CF8A-41DC-85A8-E128061E65FC</RequestId>
</DeleteScheduledTaskResponse>
```

JSON format:

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

