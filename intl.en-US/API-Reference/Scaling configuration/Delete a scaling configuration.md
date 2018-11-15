# Delete a scaling configuration {#concept_25946_zh .concept}

Deletes a specified scaling configuration.

An active scaling configuration in a scaling group cannot be deleted.

If any ECS instance created according to a scaling configuration is still in the scaling group, the scaling configuration cannot be deleted.

## Request parameters {#section_hwn_ghk_sfb .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|Operation interface, required. The parameter value is DeleteScalingConfiguration.|
|ScalingConfigurationId|String|Yes|ID of a scaling configuration.|

## Response parameters {#section_pr1_jhk_sfb .section}

Public parameters.

## Error codes {#section_ic1_khk_sfb .section}

For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

|Error message|Error code|Description|HTTP status code|
|:------------|:---------|:----------|:---------------|
|The specified scaling configuration does not exist in this account.|InvalidScalingConfigurationId.NotFound|The specified scaling configuration does not exist.|404|
|The specified scaling configuration is not in inactive state.|IncorrectScalingConfigurationLifecycleState|The current lifecycle state of specified scaling configuration does not support this action.|400|
|The scaling configuration has an associated ECS instance not deleted yet.|InstanceInUse|You cannot delete a scaling configuration or scaling group while there is an instance associated with it.|400|

## Request example {#section_gxn_phk_sfb .section}

```
http://ess.aliyuncs.com/?Action=DeleteScalingConfiguration
&ScalingConfigurationId=eOs27Kb0oXvQcUYjEGelJqUy
&<Public Request Parameters>
```

## Response example { .section}

XML format:

```
<DeleteScalingConfigurationResponse>
    <RequestId>61D30272-7111-44D9-BB45-FCB55E4A1410</RequestId>
</DeleteScalingConfigurationResponse>
```

JSON format:

```
"RequestId": "61D30272-7111-44D9-BB45-FCB55E4A1410"
```

