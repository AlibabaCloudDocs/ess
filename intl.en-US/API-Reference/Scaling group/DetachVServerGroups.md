# DetachVServerGroups {#doc_api_Ess_DetachVServerGroups .reference}

You can call this operation to remove one or more VServer groups.

## Description {#description .section}

To remove a VServer group from a scaling group, you must specify the SLB instance ID \(**LoadBalancerId**\),

-   the VServer group ID \(**VServerGroupId**\),
-   and the port number of the VServer group \(**Port**\). The VServer group is removed if the VServer group specified by the request parameters matches the VServer group in the scaling group. Otherwise, the request is ignored and no error message will be returned by the operation.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=DetachVServerGroups) simplifies API usage. You can use OpenAPI Explorer to perform operations such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou|The ID of the region where the scaling group is created, such as cn-hangzhou or cn-shanghai. For more information, see [Regions and zones](~~40654~~).

 |
|ScalingGroupId|String|Yes|asg-\*\*\*\*|The ID of the scaling group.

 |
|Action|String|No|DetachVServerGroups|The operation that you want to perform. Set the value to DetachVServerGroups.

 |
|ForceDetach|Boolean|No|false|Indicates whether the ECS instances that belong to the specified scaling group are to be removed from the VServer being detached.

 -   true: Remove the ECS instances.
-   false: Do not remove the ECS instances.

 Default value: false.

 |
|VServerGroup.N.LoadBalancerId|String|No|lb-\*\*\*\*|The ID of the SLB instance with which the VServer group is associated. N represents the SLB instance number. Valid values of N: 1 to 5.

 |
|VServerGroup.N.VServerGroupAttribute.N.Port|Integer|No|22|The port number used by Auto Scaling to add the ECS instances to the VServer group. Valid values: 1 to 65,535.

 N represents the SLB instance number. Valid values of N: 1 to 5. M represents the VServer group number that is associated with the SLB instance. Valid values of M: 1 to 5.

 |
|VServerGroup.N.VServerGroupAttribute.N.VServerGroupId|String|No|rsp-\*\*\*\*|The ID of the VServer group. N represents the SLB instance number. Valid values of N: 1 to 5.

 M represents the VServer group number that is associated with the SLB instance. Valid values of M: 1 to 5.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description |
|---------|----|-------|------------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DetachVServerGroups
&ScalingGroupId=asg-****
&RegionId=cn-hangzhou 
&VServerGroup. 1.LoadBalancerId=lb-****
&VServerGroup. 1.VServerGroupAttribute. 1.VServerGroupId=rsp-****
&VServerGroup. 1.VServerGroupAttribute. 1.Port=22
&VServerGroup. 1.VServerGroupAttribute. 2.VServerGroupId=rsp-****
&VServerGroup. 1.VServerGroupAttribute. 2.Port=80
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DetachVServerGroupsResponse> 
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</DetachVServerGroupsResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"requestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Ess)

|HTTP status code

|Error code

|Error message

|Description

|
|------------------|------------|---------------|-------------|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned when Auto Scaling is not authorized to call the specified operation.

|
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned when the specified scaling group does not exist in the current account.

|
|400

|InvalidParameter

|The specified value of parameter "%s" is not valid.

|The error message returned when the value of the parameter is invalid.

|
|400

|MissingParameter

|The input parameter "%s" that is mandatory for processing this request is not supplied.

|The error message returned when the required parameter is not specified.

|

