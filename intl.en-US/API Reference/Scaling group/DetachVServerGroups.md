# DetachVServerGroups

You can call this operation to remove one or more VServer groups.

## Description

You must set the following parameters to specify the VServer groups to be removed:

-   VServerGroup.N.LoadBalancerId: the ID of the SLB instance
-   VServerGroup.N.VServerGroupAttribute.N.VServerGroupId: the ID of the VServer group
-   VServerGroup.N.VServerGroupAttribute.N.Port: the port number of the VServer group

If the VServer groups specified in the request parameters match VServer groups in the scaling group, the matched VServer groups are removed. If no VServer groups specified in the request parameters match VServer groups in the scaling group, the request is ignored and no error is reported.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DetachVServerGroups&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DetachVServerGroups|The operation that you want to perform. Set the value to DetachVServerGroups. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the scaling group. Example: cn-hangzhou or cn-shanghai. For more information, see [Regions and zones](~~40654~~). |
|ScalingGroupId|String|Yes|asg-bp1fo0dbtsbmqa9h\*\*\*\*|The ID of the scaling group. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-42665544\*\*\*\*|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25965~~). |
|VServerGroup.N.LoadBalancerId|String|No|lb-bp1p90y3ya9h8s62d\*\*\*\*|The ID of SLB instance N with which the VServer group is associated.

N specifies the number of the SLB instance. Valid values of N: 1 to 5. |
|VServerGroup.N.VServerGroupAttribute.N.VServerGroupId|String|No|rsp-bp1jp1rge\*\*\*\*|The ID of VServer group M.

N specifies the number of the SLB instance. Valid values of N: 1 to 5.

M specifies the number of the VServer group that is associated with SLB instance N. Valid values of M: 1 to 5. |
|VServerGroup.N.VServerGroupAttribute.N.Port|Integer|No|22|The port number that is used by Auto Scaling to add the ECS instances to VServer group M. Valid values: 1 to 65535.

N specifies the number of the SLB instance. Valid values of N: 1 to 5.

M specifies the number of the VServer group that is associated with the SLB instance. Valid values of M: 1 to 5. |
|ForceDetach|Boolean|No|false|Specifies whether to remove the ECS instances in the specified scaling group from the VServer group to be removed.

-   true: removes the ECS instances.
-   false: does not remove the ECS instances.

Default value: false. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DetachVServerGroups
&ScalingGroupId=asg-bp1fo0dbtsbmqa9h****
&RegionId=cn-hangzhou
&VServerGroup.1.LoadBalancerId=lb-bp1p90y3ya9h8s62d****
&VServerGroup.1.VServerGroupAttribute.1.VServerGroupId=rsp-bp1jp1rge****
&VServerGroup.1.VServerGroupAttribute.1.Port=22
&VServerGroup.1.VServerGroupAttribute.2.VServerGroupId=rsp-bp1lczyc5****
&VServerGroup.1.VServerGroupAttribute.2.Port=80
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DetachVServerGroupsResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DetachVServerGroupsResponse>
```

`JSON` format

```
{
    "requestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

|HTTP status code

|Error code

|Error message

|Description |
|------------------|------------|---------------|-------------|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned because Auto Scaling is not authorized to call the specified operation. |
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned because the specified scaling group does not exist in the current account. |
|400

|InvalidParameter

|The specified value of parameter "%s" is not valid.

|The error message returned because a specified parameter is invalid. |
|400

|MissingParameter

|The input parameter "%s" that is mandatory for processing this request is not supplied.

|The error message returned because a required parameter is not specified. |

