# ExitStandby {#concept_69682_zh .concept}

Removes an ECS instance from standby status in a scaling group \(`ExitStandby`\).

If Server Load Balancer is configured for the scaling group, the load balancing weight of the instance is set to the value defined in the scaling configuration.

## Request parameters { .section}

|Name|Type|Required|Description|
|----|----|--------|-----------|
|Action|String|Yes|The name of this interface. Value: ExitStandby.|
|ScalingGroupId|String|Yes|The scaling group ID.|
|InstanceId.N|String|Yes|The ECS instance ID. This value can be a JSON array composed of multiple instance IDs, with the format: \["i-xxxxxxxxx", "i-yyyyyyyyy", … "i-zzzzzzzzz"\]. This parameter supports up to 20 IDs, separated by commas \(`,`\).|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|RequestId|String|Unique request ID|

## Request example { .section}

```
http://ess.aliyuncs.com/?Action=ExitStandby
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&InstanceId. 1=i-28wt48iaa
&<Common Request Parameters>
```

## Response example { .section}

XML format:

```
<ExitStandbyResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ExitStandbyResponse>
```

JSON format:

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## Error codes { .section}

|Error code|Error message|HTTP status code|Description|
|:---------|:------------|:---------------|:----------|
|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|403|The RAM user does not have permission to call this API. Contact the account owner and request this permission before trying again.|
|InvalidInstanceId.NotFound|A required authorization for the specified action is not supplied.|404|The specified ECS instance does not exist.|
|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|404|The specified scaling group does not exist.|

