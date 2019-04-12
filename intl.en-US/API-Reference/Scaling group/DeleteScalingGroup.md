# DeleteScalingGroup {#concept_25941_zh .concept}

This topic introduces how to delete a scaling group using the API.

## Description {#section_u1x_tz2_sfb .section}

This operation deletes a specified scaling group.

-   ForceDelete indicates whether to forcibly delete a scaling group and remove and release ECS instances if the scaling group has ECS instances or scaling activities are in progress.
-   If ForceDelete is set to false, the scaling group can be deleted only when the following conditions are met:
    -   Condition 1: No scaling activities are in progress in the scaling group.
    -   Condition 2: The current number \(total capacity\) of ECS instances in the scaling group is 0.\\
    -   When the two conditions are met, the scaling group is disabled and then deleted.
-   When ForceDelete is set to true:
    -   The scaling group is disabled to reject new scaling activity requests. When the existing scaling activity is completed, all ECS instances are removed from the scaling group and the group is then deleted \(manually attached ECS instances are removed from the scaling group, whereas ECS instances automatically created by the Auto Scaling service are deleted\).
-   Deleting a scaling group also deletes scaling configurations, rules, activities, and requests.
-   The following tasks or instances are not deleted: scheduled tasks, Cloud Monitor alarm tasks, Server Load Balancer instances, and RDS instances.

## Request parameters {#section_jrn_11f_sfb .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|Operation interface name, required parameter. Value: DeleteScalingGroup|
|ScalingGroupId|String|Yes|Scaling group ID|
|ForceDelete|Bool|No|Indicates whether to forcibly delete a scaling group and remove and release ECS instances if the scaling group has ECS instances or scaling activities are in progress. The default value is false, indicating that the scaling group is not forcibly deleted.|

## Response parameters {#section_et5_g1f_sfb .section}

Public parameters.

## Error codes {#section_n4d_n1f_sfb .section}

|Error message|Error code|Description|HTTP status code|
|:------------|:---------|:----------|:---------------|
|The specified scaling group does not exist in this account.|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|404|
|API is not fully authorized to the Auto Scaling service.|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|403|
|The specified scaling group still has ECS instances.|InstanceInUse|You cannot delete a scaling configuration or scaling group while there is an instance associated with it.|400|

## Request example {#section_pvz_51f_sfb .section}

```
http://ess.aliyuncs.com/?Action=DeleteScalingGroup
&ScalingGroupId=dmIDKNcyWfzncX9MWX1bwFV
&<Public Request Parameters>
```

## Response example {#section_gm4_w1f_sfb .section}

XML format:

```
<DeleteScalingGroupResponse>
    <RequestId>6469DCD0-13AC-487E-85A0-CE4922908FDE</RequestId>
</DeleteScalingGroupResponse>
```

JSON format:

```
{
"RequestId": "6469DCD0-13AC-487E-85A0-CE4922908FDE"
}
```

