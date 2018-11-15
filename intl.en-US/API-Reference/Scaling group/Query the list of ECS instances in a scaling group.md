# Query the list of ECS instances in a scaling group {#concept_25942_zh .concept}

This topic introduces how to query the list of ECS instances in a scaling group using the API.

## Description {#section_try_jbk_sfb .section}

Queries the list of ECS instances in a scaling group. You can query by scaling group ID, scaling configuration ID, health status, lifecycle status, and creation type.

-   The ECS instances in a scaling group can be created automatically or attached manually.
    -   ECS instances can be automatically created by the Auto Scaling service based on your scaling configurations and rules.
    -   ECS instances can also be manually attached to a scaling group.
-   An ECS instance in a scaling group may be in the following states during its lifecycle:
    -   Pending: The ECS instance is being attached to the scaling group, with operations such as instance creation, attaching to Server Load Balancer, and adding to the RDS access whitelist.
    -   InService: The ECS instance is successfully added to the scaling group and provides services properly.
    -   Removing: The ECS instance is being removed from the scaling group.
-   An ECS instance in a scaling group may be in the following health states:
    -   Healthy: The ECS instance is healthy.
    -   Unhealthy: The ECS instance is unhealthy if it is not in the **Running** \(`Running`\) status.
-   The Auto Scaling service automatically removes unhealthy ECS instances from scaling groups.
    -   If the unhealthy ECS instances are automatically created, the Auto Scaling service disables and releases them.
    -   If the unhealthy ECS instances are manually attached, the Auto Scaling service does not disable or release them.

## Request parameters { .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|Operation interface name, required parameter. Value: DescribeScalingInstances.|
|RegionId|String|Yes|ID of the region where the scaling group is located.|
|ScalingGroupId|String|No|Scaling group ID.|
|ScalingConfigurationId|String|No|ID of the associated scaling configuration.|
|InstanceId.N|String|No|ECS instance ID. You can input up to 20 IDs. Invalid instance IDs are not displayed in query results, and no error is reported.|
|HealthStatus|String|No|Health status of an ECS instance in the scaling group. Optional values:-   Healthy
-   Unhealthy

|
|LifecycleState|String|No|Lifecycle status of an ECS instance in the scaling group. Optional values:-   InService: the ECS instance has been added to the scaling group and runs properly.
-   Pending: the ECS instance is being attached to the scaling group with relevant configurations not completed.
-   Removing: the ECS instance is being removed from the scaling group.

|
|CreationType|String|No|ECS instance creation type. Optional values:-   AutoCreated: the ECS instance is automatically created by the Auto Scaling service in the scaling group.
-   Attached: the ECS instance is created outside the Auto Scaling service and manually attached to the scaling group.

|
|PageNumber|Integer|No|Page number of the ECS instance list, staring from 1. Default value: 1|
|PageSize|Integer|No|When querying by page, this parameter indicates the number of lines per page. Maximum value: 50; default value: 10|

## Response parameters { .section}

|Name|Type|Description|
|:---|:---|:----------|
|TotalCount|Integer|Total number of ECS instances|
|PageNumber|Integer|Current page number|
|PageSize|Integer|Number of lines per page|
|ScalingInstances|ScalingInstanceSetType|A set of ECS instance information|

ScalingInstanceSetType is a set of ScalingInstanceItemTypes.

|Name|Type|Description|
|:---|:---|:----------|
|ScalingInstance|ScalingInstanceItemType|ECS instance information|

The attributes of ScalingInstanceItemType are listed as follows.

|Name|Type|Description|
|:---|:---|:----------|
|InstanceId|String|ECS instance ID.|
|ScalingGroupId|String|ID of the scaling group to which the ECS instance belongs.|
|ScalingConfigurationId|String|ID of the associated scaling configuration.|
|HealthStatus|String|Health status of the ECS instance in the scaling group.|
|LifecycleState|String|Lifecycle status of the ECS instance in the scaling group.|
|CreationTime|String|Time when the ECS instance is attached to the scaling group.|
|CreationType|String|ECS instance creation type.|

## Error code { .section}

For common errors, see [client errors](reseller.en-US/API-Reference/Error codes/Client errors.md#) or [server errors](reseller.en-US/API-Reference/Error codes/Server errors.md#).

## Request example { .section}

```
http://ess.aliyuncs.com/?Action=DescribeScalingInstances 
&RegionId=cn-qingdao
&ScalingGroupId=dBCYxE26IHKcGq1xPcTNBwV
&<Public Request Parameters>
```

## Response example { .section}

XML format:

```
<DescribeScalingInstancesResponse>
    <RequestId>DFF8797F-5B73-4BD7-A7D0-03479C458F7A</RequestId>
<TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <ScalingInstances>
        <ScalingInstance>
            <CreationTime>2014-08-15T17:37Z</CreationTime>
            <CreationType>AutoCreated</CreationType>
            <HealthStatus>Healthy</HealthStatus>
            <InstanceId>i-283vvyytn</InstanceId>
            <LifecycleState>InService</LifecycleState>         <ScalingConfigurationId>
cGsGHrdMBa3DcDrrBVcc4k2H
</ScalingConfigurationId>
            <ScalingGroupId>dBCYxE26IHKcGq1xPcTNBwV</ScalingGroupId>
        </ScalingInstance>
    </ScalingInstances>
</DescribeScalingInstancesResponse>
```

JSON format:

```
{
  "RequestId": "13305F2D-A4C2-4E6B-B7C7-0F2150842EA3",
"TotalCount": 1,
"PageNumber": 1,
"PageSize": 50,
  "ScalingInstances": {
    "ScalingInstance": [
      {
        "ScalingConfigurationId": "bU5uZHcAgtzwcL4IeDeavqTS",
        "CreationType": "AutoCreated",
        "InstanceId": "i-28sov3exk",
        "CreationTime": "2014-08-14T10:59Z",
        "HealthStatus": "Healthy",
        "LifecycleState": "InService",
        "ScalingGroupId": "dE9YbOdCHqaFdFZHXVdDjQCB"
      }
    ]
  }
}
```

