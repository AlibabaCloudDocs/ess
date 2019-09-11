# DescribeScalingInstances {#doc_api_Ess_DescribeScalingInstances .reference}

You can call this operation to query the list of ECS instances in a scaling group and list details about the instances.

## Description {#description .section}

You can query the list of ECS instances in a scaling group by scaling group ID, scaling configuration ID, health status, lifecycle status, and how an ECS instance is created.

## Debugging {#api_explorer .section}

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeScalingInstances&type=RPC&version=2014-08-28)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|RegionId|String|Yes|cn-qingdao|The region ID of the scaling group.

 |
|Action|String|No|DescribeScalingInstances|The operation that you want to perform. Set the value to DescribeScalingInstances.

 |
|CreationType|String|No|AutoCreated|Specifies how to create an ECS instance. Valid values:

 -   AutoCreated: The ECS instance is automatically created by a scaling group based on scaling configurations and rules.
-   Attached: The ECS instance is manually added to a scaling group.

 |
|HealthStatus|String|No|Healthy|The health status of the ECS instance in the scaling group. The ECS instance is unhealthy if it is not in the Running state. Valid values:

 -   Healthy: a healthy ECS instance.
-   Unhealthy: an unhealthy ECS instance.

 Auto Scaling automatically removes unhealthy ECS instances from the scaling group. Auto Scaling stops and releases only automatically created ECS instances.

 |
|InstanceId.1|String|No|i-281vv\*\*\*\*|The ID of ECS instance N. Valid values of N: 1 to 20. The IDs of inactive instances will not be displayed in the query result and no errors will be returned.

 |
|LifecycleState|String|No|InService|The lifecycle status of the ECS instance in the scaling group. Valid values:

 -   InService: The ECS instance has been added to the scaling group and is providing services normally.
-   Pending: The ECS instance is being added to the scaling group, but is still being configured. For example, the instance is being created, attached to an SLB instance, or added to an RDS whitelist.
-   Removing: The ECS instance is being removed from the scaling group.

 |
|PageNumber|Integer|No|1|The page number of the ECS instance list to return. Pages start from page 1.

 Default value: 1.

 |
|PageSize|Integer|No|10|The number of entries to return on each page. Maximum value: 50.

 Default value: 10.

 |
|ScalingConfigurationId|String|No|asc-\*\*\*\*|The ID of the associated scaling configuration.

 |
|ScalingGroupId|String|No|asg-\*\*\*\*|The ID of the scaling group.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The current page number.

 |
|PageSize|Integer|10|The number of entries returned on each page.

 |
|RequestId|String|E481B3F5-F290-4F3E-AB40-F980FB8E098A|The ID of the request.

 |
|ScalingInstances| | |The set of ECS instances.

 |
|CreationTime|String|2019-03-06T08:06Z|The time when the ECS instance was added to the scaling group.

 |
|CreationType|String|AutoCreated|Indicates how the ECS instance was created. Valid values:

 -   AutoCreated: The ECS instance is automatically created by a scaling group based on scaling configurations and rules.
-   Attached: The ECS instance is manually added to a scaling group.

 |
|HealthStatus|String|Healthy|The health status of the ECS instance in the scaling group. Valid values:

 -   Healthy: a healthy ECS instance.
-   Unhealthy: an unhealthy ECS instance.

 |
|InstanceId|String|i-283vv\*\*\*\*|The ID of the ECS instance.

 |
|LaunchTemplateId|String|lt-m5e3ofjr1zn1aw7\*\*\*\*|The ID of the instance launch template.

 |
|LaunchTemplateVersion|String|1|The version number of the instance launch template.

 |
|LifecycleState|String|InService|The lifecycle status of the ECS instance in the scaling group. Valid values:

 -   InService: The ECS instance has been added to the scaling group and is providing services normally.
-   Pending: The ECS instance is being added to the scaling group, but is still being configured. For example, the instance is being created, attached to an SLB instance, or added to an RDS whitelist.
-   Removing: The ECS instance is being removed from the scaling group.

 |
|LoadBalancerWeight|Integer|1|The weight of the SLB instance.

 |
|ScalingConfigurationId|String|asg-\*\*\*\*|The ID of the associated scaling configuration.

 |
|ScalingGroupId|String|asg-\*\*\*\*|The ID of the scaling group to which an ECS instance belongs.

 |
|WarmupState|String|NoNeedWarmup|The warmup state of the ECS instance. Valid values:

 -   NoNeedWarmup: No warmup is required.
-   WaitingForInstanceWarmup: You must wait for the instance to finish warmup.
-   InstanceWarmupFinish: The warmup is completed.

 |
|TotalCount|Integer|1|The total number of ECS instances.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

https://ess.aliyuncs.com/?Action=DescribeScalingInstances
&RegionId=cn-qingdao
&<Common request parameters>

```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
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
                   <InstanceId>i-283vv****</InstanceId>
                  <LifecycleState>InService</LifecycleState>
                  <ScalingConfigurationId>cGsGHrdMBa3DcDrrBVcc****</ScalingConfigurationId>
                  <ScalingGroupId>dBCYxE26IHKcGq1xPcT****</ScalingGroupId>
             </ScalingInstance>
      </ScalingInstances>
</DescribeScalingInstancesResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":50,
	"RequestId":"13305F2D-A4C2-4E6B-B7C7-0F2150842EA3",
	"ScalingInstances":{
		 "ScalingInstance":[
			{
				"CreationTime":"2014-08-14T10:59Z",
				"ScalingConfigurationId":"bU5uZHcAgtzwcL4IeDe****",
				 "CreationType":"AutoCreated",
				 "HealthStatus":"Healthy",
				"ScalingGroupId":"dE9YbOdCHqaFdFZHXVdD****",
				"InstanceId":"i-28sov****",
				"LifecycleState":"InService"
			}
		]
	}
}
```

## Error codes { .section}

