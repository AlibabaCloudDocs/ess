# DescribeScalingGroups

调用DescribeScalingGroups查询伸缩组。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DescribeScalingGroups&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeScalingGroups|系统规定参数。取值：DescribeScalingGroups |
|RegionId|String|是|cn-qingdao|伸缩组所属地域的ID。 |
|PageNumber|Integer|否|1|伸缩组列表的页码。起始值：1。

 默认值：1 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。最大值：50。

 默认值：10 |
|ScalingGroupId.N|RepeatList|否|asg-bp14wlu85wrpchm0\*\*\*\*|ScalingGroupId.N为待查询伸缩组的ID，N的取值范围：1～20。查询结果会忽略失效的伸缩组ID，并且不报错。 |
|ScalingGroupName.1|String|否|scalinggroup\*\*\*\*|ScalingGroupName.N为待查询伸缩组的名称，N的取值范围：1～20。查询结果会忽略失效的伸缩组名称，并且不报错。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|当前页码。 |
|PageSize|Integer|10|每页行数。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|ScalingGroups|Array of ScalingGroup| |伸缩组信息的集合。 |
|ScalingGroup| | | |
|ActiveCapacity|Integer|1|已成功加入伸缩组，并正常运行的ECS实例数量。 |
|ActiveScalingConfigurationId|String|asc-bp1et2qekq3ojr33\*\*\*\*|伸缩组内生效的伸缩配置的ID。 |
|CompensateWithOnDemand|Boolean|true|当MultiAZPolicy取值为COST\_OPTIMIZED时，如果因价格、库存等原因无法创建足够的抢占式实例，是否允许自动尝试创建按量实例满足ECS实例数量要求。取值范围：

 -   true：允许。
-   false：不允许。 |
|CreationTime|String|2014-08-14T10:58Z|伸缩组的创建时间。 |
|DBInstanceIds|List|rm-bp15556qzebg1\*\*\*\*|伸缩组关联RDS实例的ID。 |
|DefaultCooldown|Integer|60|伸缩组默认的冷却时间。冷却时间内，该伸缩组不执行其它的伸缩活动，仅针对[云监控](~~35170~~)报警任务触发的伸缩活动有效。 |
|DesiredCapacity|Integer|5|伸缩组内ECS实例的期望数量，伸缩组会自动将ECS实例数量维持在期望实例数。 |
|GroupDeletionProtection|Boolean|true|是否开启了伸缩组删除保护。取值范围：

 -   true：开启伸缩组删除保护，此时不能删除该伸缩组。
-   false：关闭伸缩组删除保护。 |
|HealthCheckType|String|ECS|伸缩组的健康检查方式。取值范围：

 -   NONE：不做健康检查。
-   ECS：对伸缩组内的ECS实例做健康检查。 |
|LaunchTemplateId|String|lt-m5e3ofjr1zn1aw7\*\*\*\*|伸缩组使用的实例启动模板的ID。 |
|LaunchTemplateOverrides|Array of LaunchTemplateOverride| |扩展启动模板的实例规格信息。 |
|LaunchTemplateOverride| | | |
|InstanceType|String|ecs.c5.xlarge|指定的实例规格，会覆盖启动模板中的实例规格。 |
|WeightedCapacity|Integer|4|指定实例规格的权重，即实例规格的单台实例在伸缩组中表示的容量大小。权重越大，满足期望容量所需的本实例规格的实例数量越少。 |
|LaunchTemplateVersion|String|Default|伸缩组使用的实例启动模板的版本。 |
|LifecycleState|String|Active|伸缩组的状态信息。取值范围：

 -   Active：生效状态，处于生效状态的伸缩组才能接收执行伸缩规则的请求并触发伸缩活动。
-   Inactive：失效状态，处于失效状态的伸缩组不接收任何执行伸缩规则的请求。
-   Deleting：伸缩组正在删除，处于删除中状态的伸缩组不接收任何执行伸缩规则的请求，并且不能修改伸缩组相关参数。 |
|LoadBalancerIds|List|lb-bp19byhscefk3x0li\*\*\*\*|伸缩组关联的负载均衡实例的ID列表。 |
|MaxSize|Integer|2|伸缩组内ECS实例台数的最大值。 |
|MinSize|Integer|1|伸缩组内ECS实例台数的最小值。 |
|ModificationTime|String|2014-08-14T10:58Z|修改时间。 |
|MultiAZPolicy|String|PRIORITY|多可用区伸缩组ECS实例扩缩容策略。取值范围：

 -   PRIORITY：根据您定义的虚拟交换机（VSwitchIds.N）扩缩容。当优先级较高的虚拟交换机所在可用区无法创建ECS实例时，自动使用下一优先级的虚拟交换机创建ECS实例。
-   COST\_OPTIMIZED：按vCPU单价从低到高进行尝试创建。当伸缩配置设置了抢占式计费方式的多实例规格时，优先创建对应抢占式实例。您可以继续通过CompensateWithOnDemand参数指定当抢占式实例由于库存等原因无法创建时，是否自动尝试以按量付费的方式创建。

**说明：** COST\_OPTIMIZED仅在伸缩配置设置了多实例规格或者选用了抢占式实例的情况下生效。

-   BALANCE：在伸缩组指定的多可用区之间均匀分配ECS实例。如果由于库存不足等原因可用区之间变得不平衡，您可以通过API [RebalanceInstance](~~71516~~)平衡资源。 |
|OnDemandBaseCapacity|Integer|30|伸缩组所需要按量实例个数的最小值，取值范围：0~1000。当按量实例个数少于该值时，将优先创建按量实例。 |
|OnDemandPercentageAboveBaseCapacity|Integer|20|伸缩组满足最小按量实例数（OnDemandBaseCapacity）要求后，超出的实例中按量实例应占的比例，取值范围：0～100。 |
|PendingCapacity|Integer|0|正在加入伸缩组，还未完成相关配置的ECS实例的数量。 |
|PendingWaitCapacity|Integer|1|伸缩组中处于加入挂起状态的ECS实例的数量。 |
|ProtectedCapacity|Integer|1|伸缩组中处于保护中状态的ECS实例的数量。 |
|RegionId|String|cn-qingdao|伸缩组所属的地域的ID。 |
|RemovalPolicies|List|OldestScalingConfiguration|ECS实例移出伸缩组的策略的集合。取值范围：

 -   OldestInstance：取最早创建的 ECS 实例。
-   NewestInstance：取最新创建的实例。
-   OldestScalingConfiguration：取最早伸缩配置创建的 ECS 实例。 |
|RemovingCapacity|Integer|0|正在移出伸缩组的ECS实例的数量。 |
|RemovingWaitCapacity|Integer|1|伸缩组中处于移除挂起状态的ECS实例的数量。 |
|ScalingGroupId|String|asg-bp14wlu85wrpchm0\*\*\*\*|伸缩组的ID。 |
|ScalingGroupName|String|dyrSuvBOtO1dEdIlIbp\*\*\*\*|伸缩组的名称。 |
|ScalingPolicy|String|recycle|指定伸缩组的回收模式。取值范围：

 -   recycle：伸缩组的回收模式为停机回收模式 。
-   release：伸缩组的回收模式为释放模式 。

 关于被移出实例的动作，请参见[RemoveInstances](~~25955~~)。 |
|SpotInstancePools|Integer|5|指定可用实例规格的个数，伸缩组将按成本最低的多个规格均衡创建抢占式实例。取值范围：0~10。 |
|SpotInstanceRemedy|Boolean|true|是否开启补齐抢占式实例。开启后，当收到抢占式实例将被回收的系统消息时，伸缩组将尝试创建新的实例，替换掉将被回收的抢占式实例。 |
|StandbyCapacity|Integer|1|伸缩组中处于备用状态的实例数量。 |
|StoppedCapacity|Integer|1|伸缩组中处于停机不收费状态的实例数量。 |
|SuspendedProcesses|List|ScaleIn|暂停中的流程，没有则返回空。取值范围：

 -   ScaleIn：缩容流程。
-   ScaleOut：扩容流程。
-   HealthCheck：健康检查。
-   AlarmNotification：报警任务。
-   ScheduledAction：定时任务。 |
|TotalCapacity|Integer|1|当伸缩组设置了实例规格权重，表示伸缩组内所有ECS实例的加权容量总和。否则，表示伸缩组内所有ECS实例的数量。 |
|TotalInstanceCount|Integer|1|伸缩组内所有ECS实例的数量。 |
|VServerGroups|Array of VServerGroup| |后端服务器组列表。 |
|VServerGroup| | | |
|LoadBalancerId|String|147b46d767c-cn-qingdao-cm5\*\*\*\*|后端服务器组所属的负载均衡实例的ID。 |
|VServerGroupAttributes|Array of VServerGroupAttribute| |后端服务器组属性。 |
|VServerGroupAttribute| | | |
|Port|Integer|22|负载均衡实例对外提供服务的端口号。 |
|VServerGroupId|String|rsp-bp12bjrny\*\*\*\*|后端服务器组的ID。 |
|Weight|Integer|1|后端服务器组的权重。 |
|VSwitchId|String|vsw-bp1whw2u46cn8zubm\*\*\*\*|伸缩组关联虚拟交换机的ID。 |
|VSwitchIds|List|vsw-bp1whw2u46cn8zubm\*\*\*\*|伸缩组关联虚拟交换机的ID集合。如果您使用了VSwitchIds参数，VSwitchId参数将被忽略。 |
|VpcId|String|vpc-bp1vwnn14rqpyiczj\*\*\*\*|伸缩组所属VPC的ID。 |
|TotalCount|Integer|1|伸缩组的总数。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=DescribeScalingGroups
&RegionId=cn-qingdao
&PageSize=10
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeScalingGroupsResponse>
      <RequestId>68386699-8B9E-4D5B-BC4C-75A28F6C2A00</RequestId>
      <TotalCount>1</TotalCount>
      <PageSize>10</PageSize>
      <PageNumber>1</PageNumber>
      <ScalingGroups>
            <ScalingGroup>
                  <ScalingGroupId>asg-bp14wlu85wrpchm0****</ScalingGroupId>
                  <ScalingGroupName>scalinggroup****</ScalingGroupName>
                  <RegionId>cn-qingdao</RegionId>
                  <RemovingCapacity>0</RemovingCapacity>
                  <DefaultCooldown>300</DefaultCooldown>
                  <MinSize>1</MinSize>
                  <MaxSize>2</MaxSize>
                  <LifecycleState>Inactive</LifecycleState>
                  <TotalInstanceCount>0</TotalInstanceCount>
                  <ActiveScalingConfigurationId>asc-bp1et2qekq3ojr33****</ActiveScalingConfigurationId>
                  <LoadBalancerIds>
                        <LoadBalancerId>lb-bp19byhscefk3x0li****</LoadBalancerId>
                  </LoadBalancerIds>
                  <PendingCapacity>0</PendingCapacity>
                  <TotalCapacity>0</TotalCapacity>
                  <ActiveCapacity>0</ActiveCapacity>
                  <CreationTime>2014-08-14T10:58Z</CreationTime>
                  <DBInstanceIds>
                        <DBInstanceId>rm-bp15556qzebg1****</DBInstanceId>
                        <DBInstanceId>rm-bp52316qzhbg6****</DBInstanceId>
                  </DBInstanceIds>
                  <VSwitchId>vsw-bp1whw2u46cn8zubm****</VSwitchId>
                  <RemovalPolicies>
                        <RemovalPolicy>OldestScalingConfiguration</RemovalPolicy>
                        <RemovalPolicy>OldestInstance</RemovalPolicy>
                  </RemovalPolicies>
            </ScalingGroup>
      </ScalingGroups>
</DescribeScalingGroupsResponse>
```

`JSON`格式

```
{
    "RequestId": "68386699-8B9E-4D5B-BC4C-75A28F6C2A00",
    "TotalCount": 1,
    "PageSize": 10,
    "PageNumber": 1,
    "ScalingGroups": {
        "ScalingGroup": [
            {
                "ScalingGroupId": "asg-bp14wlu85wrpchm0****",
                "ScalingGroupName": "scalinggroup****",
                "RegionId": "cn-qingdao",
                "RemovingCapacity": 0,
                "DefaultCooldown": 300,
                "MinSize": 1,
                "MaxSize": 2,
                "LifecycleState": "Inactive",
                "TotalInstanceCount": 0,
                "ActiveScalingConfigurationId": "asc-bp1et2qekq3ojr33****",
                "LoadBalancerIds": {
                    "LoadBalancerId": [
                        "lb-bp19byhscefk3x0li****"
                    ]
                },
                "PendingCapacity": 0,
                "TotalCapacity": 0,
                "ActiveCapacity": 0,
                "CreationTime": "2014-08-14T10:58Z",
                "DBInstanceIds": {
                    "DBInstanceId": [
                        "rm-bp15556qzebg1****",
                        "rm-bp52316qzhbg6****"
                    ]
                },
                "VSwitchId": "vsw-bp1whw2u46cn8zubm****",
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

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

