# DeleteScalingConfiguration {#doc_api_1163510 .reference}

You can call this operation to delete a scaling configuration.

## Description {#description .section}

Active scaling configurations in a scaling group cannot be deleted.

If any ECS instances created based on a scaling configuration are still in the scaling group, the scaling configuration cannot be deleted.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=DeleteScalingConfiguration) simplifies API usage. You can use OpenAPI Explorer to perform operations such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|ScalingConfigurationId|String|Yes|eOs27Kb0oXvQcUYjEGel\*\*\*\*| The ID of the scaling configuration.

 |
|Action|String|No|DeleteScalingConfiguration| The operation that you want to perform. Set the value to DeleteScalingConfiguration.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DeleteScalingConfiguration
&ScalingConfigurationId=eOs27Kb0oXvQcUYjEGel****
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DeleteScalingConfigurationResponse> 
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</DeleteScalingConfigurationResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes {#section_ie3_882_5y8 .section}

[View error codes](https://error-center.aliyun.com/status/product/Ess)

| HTTP status code

 | Error code

 | Error message

 | Description

 |
|--------------------|--------------|-----------------|---------------|
| 404

 | InvalidScalingConfigurationId.NotFound

 | The specified scaling configuration does not exist.

 | The error message returned when the specified scaling configuration does not exist in the current account.

 |
| 400

 | IncorrectScalingConfigurationLifecycleState

 | The current lifecycle state of specified scaling configuration does not support this action.

 | The error message returned when the specified scaling configuration is in a state other than inactive.

 |
| 400

 | InstanceInUse

 | You cannot delete a scaling configuration or scaling group while there is an instance associated with it.

 | The error message returned when the specified scaling configuration still has associated ECS instances.

 |

