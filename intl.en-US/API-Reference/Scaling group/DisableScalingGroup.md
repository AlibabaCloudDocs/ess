# DisableScalingGroup {#concept_25940_zh .concept}

This topic introduces how to disable a scaling group using the API.

## Description {#section_qtb_jy2_sfb .section}

This operation disables a specified scaling group.

-   The scaling activities in progress before the scaling group is disabled are continued until completion, whereas scaling activities triggered after the scaling group is disabled are rejected.
-   The interface can be called only when the scaling group is active.

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|Operation interface name, required parameter. Value: DisableScalingGroup|
|ScalingGroupId|String|Yes|Scaling group ID|

## Response parameters { .section}

Public parameters.

## Error code { .section}

For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|Error message|Error code|Description|HTTP status code|
|:------------|:---------|:----------|:---------------|
|The specified scaling group does not exist in this account.|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|404|

## Request example { .section}

```
http://ess.aliyuncs.com/?Action=DisableScalingGroup 
&ScalingGroupId=dmIDKNcyWfzncX9MWX1bwFV
&<Public Request Parameters>
```

## Response example { .section}

XML format:

```
< DisableScalingGroupResponse>
    <RequestId>6469DCD0-13AC-487E-85A0-CE4922908FDE</RequestId>
</ DisableScalingGroupResponse>
```

JSON format:

```
{
"RequestId": "6469DCD0-13AC-487E-85A0-CE4922908FDE"
}
```

