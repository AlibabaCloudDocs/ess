# EnterStandby {#concept_69678_zh .concept}

Move an ECS instance to standby \(`EnterStandby`\) in a scaling group.

If Server Load Balancer is configured for the scaling group, the load balancing weight of the instance is set to zero.

-   When an instance is in standby status, you can manually remove it from the scaling group before releasing it independently.
-   When the number of scaling groups changes or a monitoring task triggers an automatic scaling event, instances in standby status are not removed.
-   When an instance is in standby status, if it is in an unhealthy status \(stopped, restarting, etc.\), the instance health check status is not updated and it does not trigger a scaling event to remove unhealthy instances. The health check status is only updated after the instance leaves the standby status \([ExitStandby](intl.en-US/API-Reference/Instance/ExitStandby.md#)\).

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: EnterStandby.|
|ScalingGroupId|String|Yes|The scaling group ID.|
|InstanceId.N|String|Yes|The ECS instance ID.|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|RequestId|String|The request ID|

## Request example { .section}

```
Http://ess.aliyuncs.com /? Action = enterstandby
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ2eaQ
&InstanceId. 1=i-28wt48iaa
&<Common Request Parameters>
```

## Response example { .section}

XML format:

```
<EnterStandbyResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</EnterStandbyResponse>
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
|InvalidInstanceId.NotFound|Instance “XXX” does not exist.|404|The specified ECS instance does not exist.|
|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|404|The specified scaling group does not exist.|

