# DeleteScalingGroup {#doc_api_1163781 .reference}

You can call this operation to delete a scaling group.

## Description {#description .section}

This operation deletes a specified scaling group.

-   ForceDelete indicates whether to forcibly delete a scaling group and remove or release its associated ECS instances regardless of whether it is undergoing a scaling activity.
-   If ForceDelete is set to false, the scaling group can be deleted only when the following conditions are met:
    -   Condition 1: The scaling group is not currently undergoing a scaling activity.
    -   Condition 2: The number of ECS instances currently in the scaling group \(Total Capacity\) is 0.
    -   If both of these conditions are met, the scaling group can be disabled and deleted.
-   If ForceDelete is set to true, we recommend that you perform the following procedure:
    -   Disable the scaling group to reject new scaling activity requests. Remove all ECS instances from the scaling group after the ongoing scaling activities are completed and then delete the scaling group. Manually added ECS instances are only removed from the scaling group, whereas automatically created instances are deleted.
-   Note that deleting a scaling group also deletes its scaling configurations, rules, activities, and requests.
-   The following tasks and instances are not deleted when a scaling group is deleted: scheduled tasks, CloudMonitor alert tasks, SLB instances, and RDS instances.

## Debugging {#apiExplorer .section}

[OpenAPI Explorer](https://api.aliyun.com/#product=Ess&api=DeleteScalingGroup) simplifies API usage. You can use OpenAPI Explorer to perform operations such as retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description |
|---------|----|--------|-------|------------|
|ScalingGroupId|String|Yes|dmIDKNcyWfzncX9MWX1\*\*\*\*|The ID of the scaling group.

 |
|Action|String|No|DeleteScalingGroup|The operation that you want to perform. Set the value to DeleteScalingGroup.

 |
|ForceDelete|Boolean|No|false|Indicates whether to forcibly delete the scaling group and remove or release its associated ECS instances regardless of whether it is undergoing a scaling activity. Default value: false, indicating that the scaling group is not to be forcibly deleted.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description |
|---------|----|-------|------------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DeleteScalingGroup
&ScalingGroupId=dmIDKNcyWfzncX9MWX1****
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DeleteScalingGroupResponse> 
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</DeleteScalingGroupResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
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
|404

|InvalidScalingGroupId.NotFound

|The specified scaling group does not exist.

|The error message returned when the specified scaling group does not exist in the current account.

|
|403

|Forbidden.Unauthorized

|A required authorization for the specified action is not supplied.

|The error message returned when Auto Scaling is not authorized to call the specified operation.

|
|400

|InstanceInUse

|You cannot delete a scaling configuration or scaling group while there is an instance associated with it.

|The error message returned when the specified scaling group still contains ECS instances and cannot be deleted.

|

