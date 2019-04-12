# DescribeScalingGroups {#concept_25938_zh .concept}

This topic introduces how to query a scaling group using the API.

## Description {#section_wdv_5zj_sfb .section}

Queries the information of a scaling group. Scaling groups have the following life cycle states:

-   Active: In this state, the scaling group can receive scaling rule execution requests and trigger scaling activities.
-   Inactive: In this state, the scaling group does not receive scaling rule execution requests.
-   Deleting: The scaling group is being deleted and does not receive scaling rule execution requests.

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|Operation interface name, required parameter. Value: DescribeScalingGroups|
|RegionId|String|Yes|ID of the region where the scaling group is located.|
|ScalingGroupId.N|String|No|Scaling group ID. You can enter up to 20 IDs. Invalid scaling group IDs are not displayed in query results, and no error is reported.|
|ScalingGroupName.N|String|No|Scaling group name. You can enter up to 20 names. Invalid scaling group names are not displayed in query results, and no error is reported.|
|PageNumber|Integer|No|Page number of the scaling group list, staring from 1. Default value: 1.|
|PageSize|Integer|No|When querying by page, this parameter indicates the number of lines per page. Maximum value: 50; default value: 10.|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|TotalCount|Integer|Total number of scaling groups|
|PageNumber|Integer|Current page number|
|PageSize|Integer|Number of lines per page|
|ScalingGroups|ScalingGroupSetType|Scaling group information set|

ScalingGroupSetType is a set of ScalingGroupItemTypes.

|Name|Type|Description|
|:---|:---|:----------|
|ScalingGroup|ScalingGroupItemType|Scaling group information|

The attributes of ScalingGroupItemType are listed as follows.

|Name|Type|Description|
|:---|:---|:----------|
|ScalingGroupId|String|Scaling group ID.|
|ScalingGroupName|String|Name shown for the scaling group.|
|ActiveScalingConfigurationId|String|ID of the active scaling configuration in the scaling group.|
|LaunchTemplateId|String|ID of the launch template used by the scaling group.|
|LaunchTemplateVersion|String|Version of the launch template used by the scaling group.|
|RegionId|String|ID of the region where the scaling group is located.|
|MinSize|Integer|Minimum number of ECS instances in the scaling group.|
|MaxSize|Integer|Maximum number of ECS instances in the scaling group.|
|DefaultCooldown|Integer|Default cool-down time of the scaling group.|
|RemovalPolicies|RemovalPolicySetType|A set of policies for removing ECS instances from the scaling group.|
|LoadBalancerIds|List of LoadBalancerId|ID of the Server Load Balancer instance.|
|DBInstanceIds|DBInstanceIdSetType|ID of the RDS instance.|
|VSwitchId|String|ID of the virtual switch corresponding to the scaling group.|
|LifecycleState|String|Status of the scaling group.|
|TotalCapacity|Integer|Total number of ECS instances in the scaling group.|
|ActiveCapacity|Integer|Number of ECS instances which have been attached to the scaling group and are running properly.|
|PendingCapacity|Integer|Number of ECS instances which are being attached to the scaling group with relevant configurations not completed.|
|RemovingCapacity|Integer|Number of ECS instances which are being removed from the scaling group .|
|CreationTime|String|Time when the scaling group is created.|

RemovalPolicySetType is a set of String types.

|Name|Type|Description|
|:---|:---|:----------|
|RemovalPolicy|String|Policy for removing ECS instances from the scaling group.|

DBInstanceIdSetType is a set of String types.

|Name|Type|Description|
|:---|:---|:----------|
|DBInstanceId|String|ID of the RDS instance|

## Error code {#section_q3h_r1k_sfb .section}

For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

## Request example { .section}

```
http://ess.aliyuncs.com/?Action=DescribeScalingGroups
&RegionId=cn-qingdao
&PageSize=50
&<Public Request Parameters>
```

## Response example { .section}

XML format:

```
<DescribeScalingGroupsResponse>
    <RequestId>6393C3A8-B611-42F2-AFA6-F080FC45D5D0</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <ScalingGroups> 
        <ScalingGroup>
            <ActiveCapacity>1</ActiveCapacity>
            <ActiveScalingConfigurationId>dyo713cNYIB4ddEVlKbcpOef</ActiveScalingConfigurationId>
            <DBInstanceIds>
                <DBInstanceId>rdszzzyyunybaeu</DBInstanceId>
            </DBInstanceIds>
            <VSwitchId>vpc-25j4god4l</VSwitchId>
            <DefaultCooldown>20</DefaultCooldown>
            <LifecycleState>Active</LifecycleState>
            <LoadBalancerIds>
                <LoadBalancerId>147b46d767c-cn-qingdao-cm5-a01</LoadBalancerId>
            </LoadBalancerIds>
            <MaxSize>1</MaxSize>
            <MinSize>0</MinSize>
            <PendingCapacity>0</PendingCapacity>
            <RegionId>cn-qingdao</RegionId>
            <RemovingCapacity>0</RemovingCapacity>
            <ScalingGroupId>dyrSuvBOtO1dEdIlIbplQb8</ScalingGroupId>
            <ScalingGroupName>dyrSuvBOtO1dEdIlIbplQb8</ScalingGroupName>
            <RemovalPolicies>
                <RemovalPolicy>OldestScalingConfiguration</RemovalPolicy>
                <RemovalPolicy>OldestInstance</RemovalPolicy>
            </RemovalPolicies>
            <TotalCapacity>1</TotalCapacity>
            <CreationTime>2014-08-14T10:58Z</CreationTime>
        </ScalingGroup>
    </ScalingGroups>
</DescribeScalingGroupsResponse>
```

JSON format:

```
{
"RequestId": "68386699-8B9E-4D5B-BC4C-75A28F6C2A00",
"TotalCount": 1,
"PageSize": 10,
"PageNumber": 1,
  "ScalingGroups": {
    "ScalingGroup": [
      {
        "ScalingGroupId": "b8pYCVbIV5k9cz4PWpbe0k19",
        "ScalingGroupName": "b8pYCVbIV5k9cz4PWpbe0k19",
        "RegionId": "cn-qingdao",
        "RemovingCapacity": 0,
        "DefaultCooldown": 300,
        "MinSize": 1,
        "MaxSize": 2,
        "LifecycleState": "Inactive",
        "ActiveScalingConfigurationId": " dyo713cNYIB4ddEVlKbcpOef",
        "LoadBalancerIds": {
          "LoadBalancerId": [
            "147b46d767c-cn-qingdao-cm5-a01"
          ]
        },
        "PendingCapacity": 0,
        "TotalCapacity": 0,
        "ActiveCapacity": 0,
        "CreationTime": "2014-08-14T10:58Z",
        "DBInstanceIds": {
          "DBInstanceId": [
            "rdsia3u3yia3u3y",
            "rdszzzyyunybaeu"
          ]
        },
        "VSwitchId":"vpc-25j4god4l",
        "RemovalPolicies": {
          "RemovalPolicy": [
            "OldestScalingConfiguration",
            "OldestInstance"
          ]
        }
      }
    ]
  }
 }
```

