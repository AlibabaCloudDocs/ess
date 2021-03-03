# DescribeScalingInstances

You can call this operation to query the ECS instances in a scaling group and list details about the instances.

## Description

You can query the ECS instances in a scaling group by specifying the scaling group ID, scaling configuration ID, health status, lifecycle status, and how an ECS instance is created.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeScalingInstances&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeScalingInstances|The operation that you want to perform. Set the value to DescribeScalingInstances. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the scaling group. |
|ScalingGroupId|String|No|asg-bp1igpak5ft1flyp\*\*\*\*|The ID of the scaling group. |
|ScalingConfigurationId|String|No|asc-bp1i65jd06v04vdh\*\*\*\*|The ID of the associated scaling configuration. |
|HealthStatus|String|No|Healthy|The health status of the ECS instance in the scaling group. The ECS instance is considered unhealthy if it is not in the Running state. Valid values:

-   Healthy
-   Unhealthy

Auto Scaling automatically removes from the scaling group the unhealthy ECS instances that were automatically created and releases these instances.

Whether to release the unhealthy ECS instances that were manually added to the scaling group depends on the management mode of the instance lifecycle. If the lifecycle of the ECS instances is not managed by the scaling group, Auto Scaling removes the instances from the scaling group but does not release them. If the lifecycle of the ECS instances is managed by the scaling group, Auto Scaling removes the instances from the scaling group and releases them.

**Note:** Make sure that you have sufficient balance in your account. If you have overdue payments in your account, pay-as-you-go and preemptible instances are stopped or even released. For information about status changes of ECS instances with overdue payments, see [Overdue payments](~~170589~~). |
|LifecycleState|String|No|InService|The lifecycle status of the ECS instance in the scaling group. Valid values:

-   InService: The ECS instance is added to the scaling group and can provide services normally.
-   Pending: The ECS instance is being added to the scaling group. During this process, Auto Scaling adds the ECS instance to the backend server groups of the associated SLB instances and to the whitelists of the associated ApsaraDB RDS instances.
-   Pending:Wait: The ECS instance is being added to the scaling group and put into the wait state. If a lifecycle hook that applies to scale-out events is created for the scaling group, when the ECS instance is being added to the scaling group, the instance is put into the wait state until the lifecycle hook times out.
-   Protected: The ECS instance is being protected. The ECS instance can provide services normally. However, Auto Scaling does not manage the lifecycle of the instance. You must manage it manually.
-   Standby: The ECS instance is on standby. The ECS instance is put out of service. Its weight as an SLB backend server is set to zero. Auto Scaling does not manage the lifecycle of the instance. You must manage it manually.
-   Stopped: The ECS instance is stopped. The ECS instance is stopped and put out of service.
-   Removing: The ECS instance is being removed from the scaling group. During this process, Auto Scaling removes the instance from the backend server groups of the associated SLB instances and from the whitelists of the associated ApsaraDB RDS instances.
-   Removing:Wait: The ECS instance is being removed from the scaling group and put into the wait state. If a lifecycle hook that applies to scale-in events is created for the scaling group, when the ECS instance is being removed from the scaling group, the instance is put into the wait state until the lifecycle hook times out. |
|CreationType|String|No|AutoCreated|Specifies how the ECS instance is created. Valid values:

-   AutoCreated: The ECS instance is automatically created by Auto Scaling based on the instance configuration source of the scaling group.
-   Attached: The ECS instance is manually added to the scaling group. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default value: 1. |
|PageSize|Integer|No|10|The number of entries to return on each page. Maximum value: 50.

Default value: 10. |
|InstanceId.N|RepeatList|No|i-bp109k5j3dum1ce6\*\*\*\*|The ID of ECS instance N. Valid values of N: 1 to 20. The IDs of inactive instances are not displayed in the query result and no errors are returned. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The number of the returned page. |
|PageSize|Integer|10|The number of entries per page. |
|RequestId|String|B13527BF-1FBD-4334-A512-20F5E9D3FB4D|The ID of the request. |
|ScalingInstances|Array of ScalingInstance| |The collection of ECS instances. |
|ScalingInstance| | | |
|CreatedTime|String|2020-05-18T03:11:39Z|The time when the ECS instance was added to the scaling group. The value is accurate to seconds. |
|CreationTime|String|2020-05-18T03:11Z|The time when the ECS instance was added to the scaling group. The value is accurate to minutes. |
|CreationType|String|AutoCreated|Indicates how the ECS instance is created. Valid values:

-   AutoCreated: The ECS instance is automatically created by Auto Scaling based on the instance configuration source of the scaling group.
-   Attached: The ECS instance is manually added to the scaling group. |
|Entrusted|Boolean|true|Indicates whether the scaling group is enabled to manage the instance lifecycle when you manually add the instance. When the manually added instance in managed mode is automatically removed from the scaling group, the instance is released. Valid values:

-   true: The instance lifecycle is managed by the scaling group.
-   false: The instance lifecycle is not managed by the scaling group. |
|HealthStatus|String|Healthy|The health status of the ECS instance in the scaling group. The ECS instance is considered unhealthy if it is not in the Running state. Valid values:

-   Healthy
-   Unhealthy

Auto Scaling automatically removes from the scaling group the unhealthy ECS instances that were automatically created and releases these instances.

Whether to release the unhealthy ECS instances that were manually added to the scaling group depends on the management mode of the instance lifecycle. If the lifecycle of the ECS instances is not managed by the scaling group, Auto Scaling removes the instances from the scaling group but does not release them. If the lifecycle of the ECS instances is managed by the scaling group, Auto Scaling removes the instances from the scaling group and releases them.

**Note:** Make sure that you have sufficient balance in your account. If you have overdue payments in your account, pay-as-you-go and preemptible instances are stopped or even released. For information about status changes of ECS instances with overdue payments, see [Overdue payments](~~170589~~). |
|InstanceId|String|i-bp109k5j3dum1ce6\*\*\*\*|The ID of the ECS instance. |
|LaunchTemplateId|String|lt-m5e3ofjr1zn1aw7\*\*\*\*|The ID of the launch template. |
|LaunchTemplateVersion|String|1|The version number of the launch template. |
|LifecycleState|String|InService|The lifecycle status of the ECS instance in the scaling group. Valid values:

-   InService: The ECS instance is added to the scaling group and can provide services normally.
-   Pending: The ECS instance is being added to the scaling group. During this process, Auto Scaling adds the ECS instance to the backend server groups of the associated SLB instances and to the whitelists of the associated ApsaraDB RDS instances.
-   Pending:Wait: The ECS instance is being added to the scaling group and put into the wait state. If a lifecycle hook that applies to scale-out events is created for the scaling group, when the ECS instance is being added to the scaling group, the instance is put into the wait state until the lifecycle hook times out.
-   Protected: The ECS instance is being protected. The ECS instance can provide services normally. However, Auto Scaling does not manage the lifecycle of the instance. You must manage it manually.
-   Standby: The ECS instance is on standby. The ECS instance is put out of service. Its weight as an SLB backend server is set to zero. Auto Scaling does not manage the lifecycle of the instance. You must manage it manually.
-   Stopped: The ECS instance is stopped. The ECS instance is stopped and put out of service.
-   Removing: The ECS instance is being removed from the scaling group. During this process, Auto Scaling removes the instance from the backend server groups of the associated SLB instances and from the whitelists of the associated ApsaraDB RDS instances.
-   Removing:Wait: The ECS instance is being removed from the scaling group and put into the wait state. If a lifecycle hook that applies to scale-in events is created for the scaling group, when the ECS instance is being removed from the scaling group, the instance is put into the wait state until the lifecycle hook times out. |
|LoadBalancerWeight|Integer|50|The weight of the ECS instance as an SLB backend server. |
|ScalingConfigurationId|String|asc-bp1i65jd06v04vdh\*\*\*\*|The ID of the associated scaling configuration. |
|ScalingGroupId|String|asg-bp1igpak5ft1flyp\*\*\*\*|The ID of the scaling group to which the instance belongs. |
|SpotStrategy|String|SpotWithPriceLimit|The preemption policy for the pay-as-you-go instance. Valid values:

-   SpotWithPriceLimit: applies to preemptible instances with maximum hourly prices.
-   SpotAsPriceGo: applies to pay-as-you-go instances that are of the market price at the time of purchase. |
|WarmupState|String|NoNeedWarmup|The warmup status of the ECS instance. Valid values:

-   NoNeedWarmup: No warmup is required.
-   WaitingForInstanceWarmup: You must wait for the instance to complete warmup.
-   InstanceWarmupFinish: The warmup is complete. |
|WeightedCapacity|Integer|4|The weight of the instance type, which indicates the capacity of a single instance of the specified instance type in the scaling group. A greater weight indicates that a less number of instances of the specified instance type is required to meet the expected capacity. |
|TotalCount|Integer|1|The total number of ECS instances. |
|TotalSpotCount|Integer|4|The total number of running preemptible instances in the scaling group. |

## Examples

Sample requests

```
https://ess.aliyuncs.com/?Action=DescribeScalingInstances
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeScalingInstancesResponse>
      <TotalCount>1</TotalCount>
      <PageSize>10</PageSize>
      <RequestId>D66AC79E-8299-4E0B-B681-3063C88E215B</RequestId>
      <PageNumber>1</PageNumber>
      <ScalingInstances>
            <ScalingInstance>
                  <LoadBalancerWeight>50</LoadBalancerWeight>
                  <CreatedTime>2020-12-21T03:11:00Z</CreatedTime>
                  <WarmupState>NoNeedWarmup</WarmupState>
                  <InstanceId>i-m5e3z5l951fibnd9****</InstanceId>
                  <ScalingGroupId>asg-m5e8n5qw4atki7f6****</ScalingGroupId>
                  <HealthStatus>Healthy</HealthStatus>
                  <CreationTime>2020-12-21T03:11Z</CreationTime>
                  <LifecycleState>InService</LifecycleState>
                  <Entrusted>true</Entrusted>
                  <ScalingConfigurationId>asc-m5e9vcoen45jspz7****</ScalingConfigurationId>
                  <CreationType>AutoCreated</CreationType>
            </ScalingInstance>
      </ScalingInstances>
      <TotalSpotCount>0</TotalSpotCount>
</DescribeScalingInstancesResponse>
```

`JSON` format

```
{
 "TotalCount": 1,
 "PageSize": 10,
 "RequestId": "D66AC79E-8299-4E0B-B681-3063C88E215B",
 "PageNumber": 1,
 "ScalingInstances": {
  "ScalingInstance": [
   {
    "LoadBalancerWeight": 50,
    "CreatedTime": "2020-12-21T03:11:00Z",
    "WarmupState": "NoNeedWarmup",
    "InstanceId": "i-m5e3z5l951fibnd9****",
    "ScalingGroupId": "asg-m5e8n5qw4atki7f6****",
    "HealthStatus": "Healthy",
    "CreationTime": "2020-12-21T03:11Z",
    "LifecycleState": "InService",
    "Entrusted": true,
    "ScalingConfigurationId": "asc-m5e9vcoen45jspz7****",
    "CreationType": "AutoCreated"
   }
  ]
 },
 "TotalSpotCount": 0
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

