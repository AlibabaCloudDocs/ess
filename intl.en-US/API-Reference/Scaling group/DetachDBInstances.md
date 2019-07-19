# DetachDBInstances {#doc_api_1163787 .reference}

You can call this operation to remove one or more RDS instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=DetachDBInstances) simplifies API usage. You can use OpenAPI Explorer to perform operations such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|DBInstance.N|RepeatList|Yes|rm-bp12cy3\*\*\*\*| The IDs of RDS instances. Up to five RDS instances can be removed at a time.

 |
|ScalingGroupId|String|Yes|AG6CQdPU8OKdwLjgZcJ\*\*\*\*| The ID of the scaling group.

 |
|Action|String|No|DetachDBInstances| The operation that you want to perform. Set the value to DetachDBInstances.

 |
|ForceDetach|Boolean|No|false| Indicates whether to remove the private IP addresses of instances in the scaling group from the IP whitelist of the RDS instance:

 -   true: Remove the private IP addresses.
-   false: Do not remove the private IP addresses.

 Default value: false.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DetachDBInstances
&ScalingGroupId=AG6CQdPU8OKdwLjgZcJ****
&DBInstance. 1=rm-bp12cy3****
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DetachDBInstancesResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</DetachDBInstancesResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes {#section_53c_f5s_cbd .section}

[View error codes](https://error-center.aliyun.com/status/product/Ess)

| HTTP status code

 | Error code

 | Error message

 | Description

 |
|--------------------|--------------|-----------------|---------------|
| 404

 | InvalidScalingGroupId.NotFound

 | The specified scaling group does not exist.

 | The error message returned when the specified scaling group does not exist in the current account.

 |
| 400

 | InvalidDBInstanceId.NotFound

 | DB instance "%s" does not exist.

 | The error message returned when the specified RDS instance does not exist.

 |

