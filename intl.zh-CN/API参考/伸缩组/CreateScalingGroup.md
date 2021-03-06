# CreateScalingGroup

调用CreateScalingGroup创建一个伸缩组。

## 接口说明

伸缩组是具有相同应用场景的ECS实例的集合。

一个地域下支持创建的伸缩组数量和弹性伸缩使用情况有关，请前往[配额中心](https://quotas.console.aliyun.com/products/ess/quotas)查看**伸缩组总数**对应的配额值。

伸缩组创建成功后不会立即生效。您需要先调用[EnableScalingGroup](~~25939~~)接口启用伸缩组，伸缩组才能触发伸缩活动和执行伸缩规则。

伸缩组、关联的传统型负载均衡CLB（原SLB）实例和关联的RDS实例必须在同一个地域。更多信息，请参见[地域与可用区](~~40654~~)。

如果您为伸缩组关联了CLB实例，伸缩组会自动将加入伸缩组的ECS实例添加到CLB实例的后端服务器组。您可以指定ECS实例需要加入的服务器组，支持以下两种服务器组：

-   默认服务器组：用来接收前端请求的ECS实例，如果监听没有设置虚拟服务器组或主备服务器组，默认将请求转发至默认服务器组中的ECS实例。
-   虚拟服务器组：当您需要将不同的请求转发到不同的后端服务器上时，或需要通过域名和URL进行请求转发时，可以选择使用虚拟服务器组。

**说明：** 如果您同时指定了默认服务器组和多个虚拟服务器组，ECS实例会同时添加至这些服务器组中。


ECS实例在加入CLB实例的后端服务器组后，权重默认为50。CLB实例需要满足以下条件：

-   该CLB实例的状态必须是active，您可以调用[DescribeLoadBalancers](~~27582~~)接口查看指定CLB实例的状态。
-   该CLB实例配置的所有监听端口必须开启健康检查，否则伸缩组创建失败。

如果您为伸缩组关联了应用型负载均衡ALB服务器组，伸缩组会自动将加入伸缩组的ECS实例添加为ALB服务器组的后端服务器，处理ALB实例分发的访问请求。您可以指定多个ALB服务器组，但服务器组必须与伸缩组属于同一个VPC。更多信息，请参见[AttachAlbServerGroups](~~266800~~)。

如果您为伸缩组关联了RDS实例，伸缩组会自动将加入伸缩组的ECS实例的内网IP添加到RDS实例的访问白名单。RDS实例需要满足以下条件：

-   该RDS实例的状态必须是Running，您可以调用[DescribeDBInstances](~~26232~~)接口查看指定RDS实例的状态。
-   该RDS实例访问白名单的IP数不能超过上限值。更多信息，请参见RDS文档[设置白名单](~~43185~~)。

如果伸缩组的MultiAZPolicy设置为COST\_OPTIMIZED：

-   当指定OnDemandBaseCapacity、OnDemandPercentageAboveBaseCapacity和SpotInstancePools参数时，即指定成本优化策略下的实例分配方式，在扩缩容时将优先满足该实例分配方式。
-   当不指定OnDemandBaseCapacity、OnDemandPercentageAboveBaseCapacity或SpotInstancePools参数时，成本优化策略下将仅按照成本最低的方式进行实例创建。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=CreateScalingGroup&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateScalingGroup|系统规定参数。取值：CreateScalingGroup |
|AlbServerGroup.N.AlbServerGroupId|String|是|sgp-ddwb0y0g6y9bjm\*\*\*\*|ALB服务器组ID。

 N为ALB服务器组的编号。一个伸缩组支持关联的ALB服务器组数量有限，如需查看或手动申请提升配额值，请前往[配额中心](https://quotas.console.aliyun.com/products/ess/quotas)。 |
|AlbServerGroup.N.Port|Integer|是|22|弹性伸缩将ECS实例添加到ALB服务器组后，ECS实例使用的端口号，取值范围：1~65535。

 N为ALB服务器组的编号。

 **说明：** 如果N相同，Port不同，系统会默认向伸缩组关联多个不同Port的该ALB服务器组。 |
|AlbServerGroup.N.Weight|Integer|是|100|弹性伸缩将ECS实例添加到ALB服务器组后，ECS实例作为后端服务器的权重。权重越高，ECS实例将被分配到越多的访问请求。如果权重为0，则ECS实例不会收到访问请求。取值范围：0~100。

 N为ALB服务器组的编号。 |
|MaxSize|Integer|是|20|伸缩组内ECS实例台数的最大值，当伸缩组内ECS实例数大于MaxSize时，弹性伸缩会自动移出ECS实例。

 MaxSize的取值范围和弹性伸缩使用情况有关，请前往[配额中心](https://quotas.console.aliyun.com/products/ess/quotas)查看**单个伸缩组可以设置的组内最大实例数**对应的配额值。

 例如，如果**单个伸缩组可以设置的组内最大实例数**对应的配额值为2000，则MaxSize的取值范围为0~2000。 |
|MinSize|Integer|是|2|伸缩组内ECS实例台数的最小值，当伸缩组内ECS实例数小于MinSize时，弹性伸缩会自动创建ECS实例。

 **说明：** MinSize的值必须小于或等于MaxSize。 |
|RegionId|String|是|cn-qingdao|伸缩组所属的地域ID。更多详情，请参见[地域与可用区](~~40654~~)。 |
|ScalingGroupName|String|否|scalinggroup\*\*\*\*|伸缩组的名称，同一地域下伸缩组名称唯一。长度为2~64个英文或中文字符，以数字、大小英文字母或中文开头，可以包含数字、下划线（\_）、连字符（-）和小数点（.）。

 默认值为ScalingGroupId的值。 |
|LaunchTemplateId|String|否|lt-m5e3ofjr1zn1aw7\*\*\*\*|实例启动模板ID，用于指定伸缩组从实例启动模板获取启动配置信息。 |
|LaunchTemplateVersion|String|否|Default|实例启动模板的版本。取值范围：

 -   固定的模板版本号。
-   Default：始终使用模板默认版本。
-   Latest：始终使用模板最新版本。 |
|InstanceId|String|否|i-28wt4\*\*\*\*|ECS实例的ID。创建伸缩组时，将从指定的实例获取所需的配置信息，并自动创建伸缩配置。 |
|DefaultCooldown|Integer|否|300|一次伸缩活动（添加或移出ECS实例）结束后的一段冷却时间。取值范围：0~86400，单位：秒。

 冷却时间内，该伸缩组不执行其它的伸缩活动，仅针对云监控报警任务触发的伸缩活动有效。

 默认值：300 |
|LoadBalancerIds|String|否|\["lb-bp1u7etiogg38yvwz\*\*\*\*", "lb-bp168cqrux9ai9l7f\*\*\*\*", "lb-bp1jv3m9zvj22ufxp\*\*\*\*"\]|传统型负载均衡CLB（原SLB）实例ID。取值可以是由多台CLB实例ID组成一个JSON数组，ID之间用半角逗号（,）隔开。

 单个伸缩组可以关联的CLB总数和弹性伸缩使用情况有关，请前往[配额中心](https://quotas.console.aliyun.com/products/ess/quotas)查看**单个伸缩组可以关联的负载均衡实例总数**对应的配额值。 |
|DBInstanceIds|String|否|\["rm-bp142f86de0t7\*\*\*\*", "rm-bp18l1z42ar4o\*\*\*\*", "rm-bp1lqr97h4aqk\*\*\*\*"\]|RDS实例ID。取值可以是由多台RDS实例ID组成一个JSON数组，ID之间用半角逗号（,）隔开。

 单个伸缩组可以关联的RDS实例总数和弹性伸缩使用情况有关，请前往[配额中心](https://quotas.console.aliyun.com/products/ess/quotas)查看**单个伸缩组可以关联的RDS实例总数**对应的配额值。 |
|RemovalPolicy.1|String|否|OldestScalingConfiguration|指定实例移出策略的第一段筛选策略。取值范围：

 -   OldestInstance：移出最早加入伸缩组的ECS实例。
-   NewestInstance：移出最新加入伸缩组的ECS实例。
-   OldestScalingConfiguration：移出最早伸缩配置创建的ECS实例。

 **说明：** OldestScalingConfiguration中提到的伸缩配置泛指组内实例配置信息来源，包括伸缩配置和启动模板。

 启动模板的版本号低不代表添加时间早，例如在创建伸缩组时选择实例启动模板lt-foress的版本2，然后修改伸缩组，选择实例启动模板lt-foress的版本1，则对伸缩组来说，启动模板lt-foress的版本2是最早的。

 仅当RemovalPolicy.1和RemovalPolicy.2均未设置取值时，RemovalPolicy.1有默认值，默认为OldestScalingConfiguration。

 **说明：** 伸缩组移出ECS实例还受伸缩组的扩缩容策略（MultiAZPolicy）影响。更多信息，请参见[设置移出实例的组合策略](~~254822~~)。 |
|RemovalPolicy.2|String|否|OldestInstance|指定实例移出策略的第二段筛选策略，不允许与RemovalPolicy.1取值相同。取值范围：

 -   OldestInstance：移出最早加入伸缩组的ECS实例。
-   NewestInstance：移出最新加入伸缩组的ECS实例。
-   OldestScalingConfiguration：移出最早伸缩配置创建的ECS实例。

 仅当RemovalPolicy.1和RemovalPolicy.2均未设置取值时，RemovalPolicy.2有默认值，默认为OldestInstance。

 **说明：** 伸缩组移出ECS实例还受伸缩组的扩缩容策略（MultiAZPolicy）影响。更多信息，请参见[设置移出实例的组合策略](~~254822~~)。 |
|VSwitchId|String|否|vsw-bp14zolna43z266bq\*\*\*\*|虚拟交换机的ID。指定后，伸缩组的网络类型为专有网络。

 **说明：** 当伸缩组未指定VSwitchId或VSwitchIds.N参数时，伸缩组的网络类型默认为经典网络。 |
|VSwitchIds.N|RepeatList|否|vsw-bp14zolna43z266bq\*\*\*\*|一台或多台虚拟交换机的ID，N的取值范围：1~5。如果您使用了VSwitchIds.N参数，VSwitchId参数将被忽略。指定后，伸缩组的网络类型为专有网络。

 指定多台虚拟交换机时：

 -   所属的VPC必须相同。
-   所属的可用区可以不同。
-   虚拟交换机的优先级按照数字升序排序，1表示最高优先级。当优先级较高的虚拟交换机所在可用区无法创建ECS实例时，自动选择下一优先级的虚拟交换机创建ECS实例。

 **说明：** 当伸缩组未指定VSwitchId或VSwitchIds.N参数时，伸缩组的网络类型默认为经典网络。 |
|MultiAZPolicy|String|否|PRIORITY|多可用区伸缩组ECS实例扩缩容策略。取值范围：

 -   PRIORITY：先指定的虚拟交换机（VSwitchIds.N）优先级最高。弹性伸缩优先在优先级最高的交换机所在可用区尝试扩缩容，如果无法扩缩容，则自动在下一优先级的交换机所在可用区进行扩缩容。
-   COST\_OPTIMIZED：扩容时弹性伸缩按vCPU单价从低到高尝试创建ECS实例，缩容时按vCPU单价从高到低尝试移出ECS实例。当伸缩配置设置了抢占式计费方式的多实例规格时，优先创建对应抢占式实例。您可以继续通过CompensateWithOnDemand参数指定当抢占式实例由于库存等原因无法创建时，是否自动尝试以按量付费的方式创建。

**说明：** COST\_OPTIMIZED仅在伸缩配置设置了多实例规格或者选用了抢占式实例的情况下生效。

-   BALANCE：在伸缩组指定的多可用区之间均匀分配ECS实例。如果由于库存不足等原因可用区之间变得不平衡，您可以通过API [RebalanceInstance](~~71516~~)平衡资源。

 默认值：PRIORITY |
|HealthCheckType|String|否|ECS|伸缩组的健康检查方式。取值范围：

 -   NONE：不做健康检查。
-   ECS：对伸缩组内的ECS实例做健康检查。

 默认值：ECS |
|LifecycleHook.N.LifecycleHookName|String|否|lifecyclehook\*\*\*\*|生命周期挂钩名称，指定后不支持修改，未指定时默认与生命周期挂钩ID相同。 |
|LifecycleHook.N.LifecycleTransition|String|否|SCALE\_OUT|生命周期挂钩适用的伸缩活动类型，取值范围：

 -   SCALE\_OUT：伸缩组弹性扩张活动。
-   SCALE\_IN：伸缩组弹性收缩活动。

 **说明：** 若伸缩组指定生命周期挂钩，此参数必选，其他相关参数可选。 |
|LifecycleHook.N.DefaultResult|String|否|CONTINUE|等待状态结束后的下一步动作。取值范围：

 -   CONTINUE：继续响应弹性扩张活动或者继续响应弹性收缩活动。
-   ABANDON：直接释放弹性扩张活动创建出来的ECS实例或者直接将弹性收缩活动中的ECS实例从伸缩组移除。

 当伸缩组发生弹性收缩活动（SCALE\_IN）并触发多个生命周期挂钩时，DefaultResult取值为ABANDON的生命周期挂钩触发的等待状态结束时，会提前结束其它对应的等待状态。其他情况下，下一步动作均以最后一个结束等待状态的下一步动作为准。

 默认值：CONTINUE |
|LifecycleHook.N.HeartbeatTimeout|Integer|否|600|生命周期挂钩为伸缩组活动设置的等待时间，等待状态超时后会执行下一步动作。取值范围：30~21600，单位：秒。

 创建了生命周期挂钩后，您可以调用[RecordLifecycleActionHeartbeat](~~73846~~)延长ECS实例的等待时间，也可以调用[CompleteLifecycleAction](~~73847~~)提前结束伸缩活动的等待状态。

 默认值：600 |
|LifecycleHook.N.NotificationMetadata|String|否|Test|伸缩活动的等待状态的固定字符串信息。参数长度不能超过128个字符。弹性伸缩每次推送消息到通知对象时，会同时发送您预先指定的NotificationMetadata参数值，便于管理和标记不同类别的通知信息。当您同时指定了NotificationArn参数时，NotificationMetadata参数方可生效。 |
|LifecycleHook.N.NotificationArn|String|否|acs:ess:cn-hangzhou:1111111111:queue/queue2|生命周期挂钩通知对象标识符，支持消息服务MNS队列或主题，参数取值格式：acs:ess:\{region\}:\{account-id\}:\{resource-relative-id\}。

 -   region：伸缩组所在的地域。
-   account-id：阿里云账号ID。

 例如：

 -   MNS队列：acs:ess:\{region\}:\{account-id\}:queue/\{queuename\}
-   MNS主题：acs:ess:\{region\}:\{account-id\}:topic/\{topicname\} |
|VServerGroup.N.LoadBalancerId|String|否|lb-bp1u7etiogg38yvwz\*\*\*\*|虚拟服务器组所属传统型负载均衡CLB（原SLB）实例的ID。

 更多信息，请参见[AttachVServerGroups](~~98983~~)。 |
|VServerGroup.N.VServerGroupAttribute.N.VServerGroupId|String|否|rsp-bp1443g77\*\*\*\*|虚拟服务器组ID。

 更多信息，请参见[AttachVServerGroups](~~98983~~)。 |
|VServerGroup.N.VServerGroupAttribute.N.Port|Integer|否|22|弹性伸缩将ECS实例添加到虚拟服务器组后，ECS实例使用的端口号，取值范围：1~65535。

 更多信息，请参见[AttachVServerGroups](~~98983~~)。 |
|VServerGroup.N.VServerGroupAttribute.N.Weight|Integer|否|100|弹性伸缩将ECS实例添加到虚拟服务器组后，ECS实例作为后端服务器的权重。权重越高，ECS实例将被分配到越多的访问请求。如果权重为0，则ECS实例不会收到访问请求。取值范围：0~100。默认值：50。

 N的取值范围：1~5。

 更多信息，请参见[AttachVServerGroups](~~98983~~)。 |
|ScalingPolicy|String|否|recycle|指定伸缩组的回收模式。取值范围：

 -   recycle：伸缩组的回收模式为停机回收模式。
-   release：伸缩组的回收模式为释放模式。

 ScalingPolicy指定伸缩组的回收模式，但实例被移出伸缩组时的具体动作，由RemoveInstances的RemovePolicy参数决定，更多说明请参见[RemoveInstances](~~25955~~)。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |
|OnDemandBaseCapacity|Integer|否|30|伸缩组所需要按量实例个数的最小值，取值范围：0~1000。当按量实例个数少于该值时，将优先创建按量实例。 |
|OnDemandPercentageAboveBaseCapacity|Integer|否|20|伸缩组满足最小按量实例数（OnDemandBaseCapacity）要求后，超出的实例中按量实例应占的比例，取值范围：0～100。 |
|SpotInstanceRemedy|Boolean|否|true|是否开启补齐抢占式实例。开启后，当收到抢占式实例将被回收的系统消息时，伸缩组将尝试创建新的实例，替换掉将被回收的抢占式实例。 |
|CompensateWithOnDemand|Boolean|否|true|当MultiAZPolicy取值为COST\_OPTIMIZED时，如果因价格、库存等原因无法创建足够的抢占式实例，是否允许自动尝试创建按量实例满足ECS实例数量要求。取值范围：

 -   true：允许。
-   false：不允许。

 默认值：true |
|SpotInstancePools|Integer|否|5|指定可用实例规格的个数，伸缩组将按成本最低的多个规格均衡创建抢占式实例。取值范围：1~10。 |
|DesiredCapacity|Integer|否|5|伸缩组内ECS实例的期望数量，伸缩组会自动将ECS实例数量维持在期望实例数。取值不得大于MaxSize，且不得小于MinSize。 |
|GroupDeletionProtection|Boolean|否|true|是否开启伸缩组删除保护。取值范围：

 -   true：开启伸缩组删除保护，此时不能删除该伸缩组。
-   false：关闭伸缩组删除保护。

 默认值：false |
|Tag.N.Key|String|否|Department|伸缩组的标签键。 |
|Tag.N.Value|String|否|Finance|伸缩组的标签值。 |
|LaunchTemplateOverride.N.InstanceType|String|否|ecs.c5.xlarge|当您需要伸缩组按照实例规格容量进行伸缩时，请同时指定本参数和LaunchTemplateOverride.N.WeightedCapacity。

 本参数用于指定实例规格，会覆盖启动模板中的实例规格。您可以指定N个本参数，扩展启动模板支持N个实例规格。N的取值范围：1~10。

 **说明：** 仅当LaunchTemplateId参数指定了启动模板时，本参数生效。

 InstanceType的取值范围：在售的ECS实例规格，请参见[实例规格族](~~25378~~)。 |
|LaunchTemplateOverride.N.WeightedCapacity|Integer|否|4|当您需要伸缩组按照实例规格容量进行伸缩时，在指定LaunchTemplateOverride.N.InstanceType后，再指定本参数。两个参数一一对应，N需要保持一致。

 本参数用于指定实例规格的权重，即实例规格的单台实例在伸缩组中表示的容量大小。权重越大，满足期望容量所需的本实例规格的实例数量越少。

 由于每个实例规格的vCPU个数、内存大小等性能指标会有差异，您可以根据自身需求，给不同的实例规格配置不同的权重。

 例如：

 -   当前容量：0
-   期望容量：6
-   ecs.c5.xlarge规格容量：4

 为满足期望容量，伸缩组将为用户扩容2台ecs.c5.xlarge实例。

 **说明：** 扩容时伸缩组的容量不得超过最大容量（MaxSize）与实例规格的最大权重之和。

 WeightedCapacity的取值范围：1~500。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ScalingGroupId|String|asg-bp14wlu85wrpchm0\*\*\*\*|伸缩组ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
http(s)://ess.aliyuncs.com/?Action=CreateScalingGroup
&AlbServerGroup.1.AlbServerGroupId=sgp-ddwb0y0g6y9bjm****
&AlbServerGroup.1.Port=22
&AlbServerGroup.1.Weight=100
&MaxSize=20
&MinSize=2
&RegionId=cn-qingdao
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateScalingGroupResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <ScalingGroupId>asg-bp14wlu85wrpchm0****</ScalingGroupId>
</CreateScalingGroupResponse>
```

`JSON`格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "ScalingGroupId": "asg-bp14wlu85wrpchm0****"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ess)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|400

|IncorrectDBInstanceStatus

|The current status of DB instance “XXX” does not support this action.

|指定RDS实例的状态必须是Running。 |
|400

|IncorrectLoadBalancerHealthCheck

|The current health check type of specified load balancer does not support this action.

|指定的CLB实例必须开启健康检查。 |
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|指定CLB实例的状态必须是active。 |
|400

|IncorrectVSwitchStatus

|The current status of virtual switch does not support this operation.

|虚拟交换机不可用，无法创建ECS实例。 |
|400

|InvalidDBInstanceId. RegionMismatch

|DB instance “XXX” and the specified scaling group are not in the same Region.

|指定的RDS实例与伸缩组必须在同一地域。 |
|400

|InvalidLoadBalancerId.IncorrectAddressType

|The current address type of specified load balancer does not support this action.

|指定虚拟交换机后，CLB实例为私网类型。 |
|400

|InvalidLoadBalancerId.IncorrectInstanceNetworkType

|The network type of the instance in specified Load Balancer does not support this action.

|指定的CLB实例内搭载的ECS实例的网络类型与伸缩组的网络类型必须一致。 |
|400

|InvalidLoadBalancerId.RegionMismatch

|The specified Load Balancer and the specified scaling group are not in the same Region.

|指定的CLB实例与伸缩组必须在同一地域。 |
|400

|InvalidLoadBalancerId.VPCMismatch

|The specified virtual switch and the instance in specified Load Balancer are not in the same VPC.

|伸缩组内的CLB实例搭载的ECS实例与虚拟交换机应该在同一个VPC中。 |
|400

|InvalidParameter

|The specified value of parameter "ScalingPolicy" is not valid.

|指定的回收模式参数不存在。 |
|400

|InvalidParameter.Conflict

|The value of parameter &lt;parameter name&gt; and parameter &lt;parameter name&gt; are conflict.

|指定的MinSize不能大于MaxSize。 |
|400

|InvalidScalingGroupName.Duplicate

|The specified value of parameter &lt;parameter name&gt; is duplicated.

|伸缩组名已存在。 |
|400

|QuotaExceeded.DBInstanceSecurityIP

|Security IP quota exceeded in DB instance “XXX”.

|指定的RDS实例访问白名单的IP个数达到上限。 |
|400

|QuotaExceeded.PrivateIpAddress

|Private IP address quota exceeded in the specified virtual switch.

|虚拟交换机无法再分配多余的私有IP地址。 |
|400

|QuotaExceeded.ScalingGroup

|Scaling group quota exceeded.

|用户的伸缩组使用个数达到上限。 |
|400

|QuotaExceeded.VPCInstance

|Instance quota exceeded in the specified VPC.

|该VPC内的实例数超过数量限制。 |
|404

|InvalidDBInstanceId.NotFound

|DB instance “XXX” does not exist.

|指定的RDS实例不存在。 |
|404

|InvalidLoadBalancerId.NotFound

|The specified Load Balancer does not exist.

|指定的CLB实例不存在。 |
|404

|InvalidRegionId.NotFound

|The specified region does not exist.

|指定的地域不存在。 |
|404

|InvalidVSwitchId.NotFound

|The specified virtual switch does not exist.

|指定的虚拟交换机不存在。 |
|400

|LaunchTemplateVersionSet.NotFound

|The specific version of launch template is not exist.

|实例启动模板指定版本不存在。 |
|400

|LaunchTemplateSet.NotFound

|The specified launch template set is not found.

|指定实例启动模板不存在。 |
|400

|TemplateMissingParameter.ImageId

|The input parameter "ImageId" that is mandatory for processing this request is not supplied.

|实例启动模板指定版本缺少镜像信息。 |
|400

|TemplateMissingParameter.InstanceTypes

|The input parameter "InstanceTypes" that is mandatory for processing this request is not supplied.

|实例启动模板指定版本缺少实例规格信息。 |
|400

|TemplateMissingParameter.SecurityGroup

|The input parameter "SecurityGroup" that is mandatory for processing this request is not supplied.

|实例启动模板指定版本缺少安全组信息。 |
|400

|TemplateVersion.NotNumber

|The input parameter "LaunchTemplateVersion" is supposed to be a string representing the version number.

|指定实例启动模板固定版本号为非数字。 |
|400

|AlbServerGroup.NotExist

|The ServerGroup "%s" do\(es\) not exist.

|账号下不存在指定的ALB服务器组。 |

