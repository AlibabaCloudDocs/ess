# DescribeScalingInstances

You can call this operation to query the list of ECS instances in a scaling group and list details about the instances.

## Description

You can query the list of ECS instances in a scaling group by specifying the scaling group ID, scaling configuration ID, health status, lifecycle status, and how an ECS instance is created.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ess&api=DescribeScalingInstances&type=RPC&version=2014-08-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeScalingInstances|The operation that you want to perform. Set the value to DescribeScalingInstances. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the scaling group. |
|ScalingGroupId|String|No|asg-bp1igpak5ft1flyp\*\*\*\*|The ID of the scaling group. |
|ScalingConfigurationId|String|No|asc-bp1i65jd06v04vdh\*\*\*\*|The ID of the associated scaling configuration. |
|HealthStatus|String|No|Healthy|The health status of the ECS instance in the scaling group. The ECS instance is unhealthy if it is not in the Running state. Valid values:

-   Healthy
-   Unhealthy

Auto Scaling automatically removes unhealthy ECS instances from the scaling group and releases them.

Whether to release ECS instances that are manually added to the scaling group depends on the management mode of the instances. If the lifecycle of the ECS instances is not managed by the scaling group, Auto Scaling removes the instances from the scaling group but does not release them. If the lifecycle of the ECS instances is managed by the scaling group, Auto Scaling removes the instances from the scaling group and releases them.

**Note:** Make sure that you have sufficient balance in your account. If you have overdue payments in your account, pay-as-you-go and preemptible instances will be stopped or even released. For information about status changes of ECS instances with overdue payments, see [Overdue payments](~~170589~~). |
|LifecycleState|String|No|InService|The lifecycle status of the ECS instance in the scaling group. Valid values:

-   InService: The ECS instance is added to the scaling group and can provide services normally.
-   Pending: The ECS instance is being added to the scaling group. During this process, Auto Scaling adds the ECS instance to the backend server groups of the associated Server Load Balancer \(SLB\) instances and to the whitelists of the associated ApsaraDB for RDS instances.
-   Pending:Wait: The ECS instance is being added to the scaling group and put into the wait state. If a lifecycle hook that applies to scale-out events is created for the scaling group, when the ECS instance is being added to the scaling group, the instance is put into the wait state until the lifecycle hook times out.
-   Protected: The ECS instance is being protected. The ECS instance can provide services normally. However, Auto Scaling does not manage the lifecycle of the instance. You must manage it manually.
-   Standby: The ECS instance is on standby. The ECS instance is put out of service. Its weight as an SLB backend server is set to zero. Auto Scaling does not manage the lifecycle of the instance. You must manage it manually.
-   Stopped: The ECS instance is stopped. The ECS instance is stopped and put out of service.
-   Removing: The ECS instance is being removed from the scaling group. During this process, Auto Scaling removes the instance from the backend server groups of the associated SLB instances and from the whitelists of the associated ApsaraDB for RDS instances.
-   Removing:Wait: The ECS instance is being removed from the scaling group and put into the wait state. If a lifecycle hook that applies to scale-in events is created for the scaling group, when the ECS instance is being removed from the scaling group, the instance is put into the wait state until the lifecycle hook times out. |
|CreationType|String|No|AutoCreated|Specifies how the ECS instance is created. Valid values:

-   AutoCreated: The ECS instance is automatically created by Auto Scaling based on the instance configuration source of the scaling group.
-   Attached: The ECS instance is manually added to the scaling group. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default value: 1 |
|PageSize|Integer|No|10|The number of entries to return on each page. Maximum value: 50.

Default value: 10 |
|InstanceId.1|String|No|i-bp109k5j3dum1ce6\*\*\*\*|The ID of ECS instance N. Valid values of N: 1 to 20. The IDs of inactive instances will not be displayed in the query result and no errors will be returned. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|B13527BF-1FBD-4334-A512-20F5E9D3FB4D|The ID of the request. |
|ScalingInstances|Array| |The collection of ECS instances. |
|ScalingInstance| | | |
|CreatedTime|String|2020-05-18T03:11:39Z|The time when the ECS instance was added to the scaling group. Unit: seconds. |
|CreationTime|String|2020-05-18T03:11Z|The time when the ECS instance was added to the scaling group. Unit: minutes. |
|CreationType|String|AutoCreated|Indicates how the ECS instance was created. Valid values:

-   AutoCreated: The ECS instance was automatically created by Auto Scaling based on the instance configuration source of the scaling group.
-   Attached: The ECS instance was manually added to the scaling group. |
|Entrusted|Boolean|true|Indicates whether the scaling group is enabled to manage the instance lifecycle when you manually add the instance. When the manually added instance in managed mode is automatically removed from the scaling group, the instance will be released. Valid values:

-   true: The instance lifecycle is managed by the scaling group.
-   false: The instance lifecycle is not managed by the scaling group. |
|HealthStatus|String|Healthy|The health status of the ECS instance in the scaling group. The ECS instance is unhealthy if it is not in the Running state. Valid values:

-   Healthy
-   Unhealthy

Auto Scaling automatically removes unhealthy ECS instances from the scaling group and releases them.

Whether to release ECS instances that are manually added to the scaling group depends on the management mode of the instances. If the lifecycle of the ECS instances is not managed by the scaling group, Auto Scaling removes the instances from the scaling group but does not release them. If the lifecycle of the ECS instances is managed by the scaling group, Auto Scaling removes the instances from the scaling group and releases them.

**Note:** Make sure that you have sufficient balance in your account. If you have overdue payments in your account, pay-as-you-go and preemptible instances will be stopped or even released. For information about status changes of ECS instances with overdue payments, see [Overdue payments](~~170589~~). |
|InstanceId|String|i-bp109k5j3dum1ce6\*\*\*\*|The ID of the ECS instance. |
|LaunchTemplateId|String|lt-m5e3ofjr1zn1aw7\*\*\*\*|The ID of the instance launch template. |
|LaunchTemplateVersion|String|1|The version number of the instance launch template. |
|LifecycleState|String|InService|The lifecycle status of the ECS instance in the scaling group. Valid values:

-   InService: The ECS instance is added to the scaling group and can provide services normally.
-   Pending: The ECS instance is being added to the scaling group. During this process, Auto Scaling adds the ECS instance to the backend server groups of the associated SLB instances and to the whitelists of the associated ApsaraDB for RDS instances.
-   Pending:Wait: The ECS instance is being added to the scaling group and put into the wait state. If a lifecycle hook that applies to scale-out events is created for the scaling group, when the ECS instance is being added to the scaling group, the instance is put into the wait state until the lifecycle hook times out.
-   Protected: The ECS instance is being protected. The ECS instance can provide services normally. However, Auto Scaling does not manage the lifecycle of the instance. You must manage it manually.
-   Standby: The ECS instance is on standby. The ECS instance is put out of service. Its weight as an SLB backend server is set to zero. Auto Scaling does not manage the lifecycle of the instance. You must manage it manually.
-   Stopped: The ECS instance is stopped. The ECS instance is stopped and put out of service.
-   Removing: The ECS instance is being removed from the scaling group. During this process, Auto Scaling removes the instance from the backend server groups of the associated SLB instances and from the whitelists of the associated ApsaraDB for RDS instances.
-   Removing:Wait: The ECS instance is being removed from the scaling group and put into the wait state. If a lifecycle hook that applies to scale-in events is created for the scaling group, when the ECS instance is being removed from the scaling group, the instance is put into the wait state until the lifecycle hook times out. |
|LoadBalancerWeight|Integer|50|The weight of the ECS instance as an SLB backend server. |
|ScalingConfigurationId|String|asc-bp1i65jd06v04vdh\*\*\*\*|The ID of the associated scaling configuration. |
|ScalingGroupId|String|asg-bp1igpak5ft1flyp\*\*\*\*|The ID of the scaling group to which the instance belongs. |
|WarmupState|String|NoNeedWarmup|The warmup status of the ECS instance. Valid values:

-   NoNeedWarmup: No warmup is required.
-   WaitingForInstanceWarmup: You must wait for the instance to complete warmup.
-   InstanceWarmupFinish: The warmup is complete. |
|TotalCount|Integer|1|The total number of ECS instances. |

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
    <RequestId>B13527BF-1FBD-4334-A512-20F5E9D3FB4D</RequestId>
    <PageNumber>1</PageNumber>
    <ScalingInstances>
        <ScalingInstance>
            <LoadBalancerWeight>50</LoadBalancerWeight>
            <CreatedTime>2020-05-18T03:11:39Z</CreatedTime>
            <WarmupState>NoNeedWarmup</WarmupState>
            <InstanceId>i-bp109k5j3dum1ce6****</InstanceId>
            <ScalingGroupId>asg-bp1igpak5ft1flyp****</ScalingGroupId>
            <HealthStatus>Healthy</HealthStatus>
            <CreationTime>2020-05-18T03:11Z</CreationTime>
            <LifecycleState>InService</LifecycleState>
            <Entrusted>true</Entrusted>
            <ScalingConfigurationId>asc-bp1i65jd06v04vdh****</ScalingConfigurationId>
            <CreationType>AutoCreated</CreationType>
        </ScalingInstance>
    </ScalingInstances>
</DescribeScalingInstancesResponse>
```

`JSON` format

```
{
    "TotalCount": 1,
    "PageSize": 10,
    "RequestId": "B13527BF-1FBD-4334-A512-20F5E9D3FB4D",
    "PageNumber": 1,
    "ScalingInstances": {
        "ScalingInstance": [
            {
                "LoadBalancerWeight": 50,
                "CreatedTime": "2020-05-18T03:11:39Z",
                "WarmupState": "NoNeedWarmup",
                "InstanceId": "i-bp109k5j3dum1ce6****",
                "ScalingGroupId": "asg-bp1igpak5ft1flyp****",
                "HealthStatus": "Healthy",
                "CreationTime": "2020-05-18T03:11Z",
                "LifecycleState": "InService",
                "Entrusted": true,
                "ScalingConfigurationId": "asc-bp1i65jd06v04vdh****",
                "CreationType": "AutoCreated"
            }
        ]
    }
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ess).

