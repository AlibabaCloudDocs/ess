# CreateScalingGroup {#doc_api_Ess_CreateScalingGroup .reference}

调用CreateScalingGroup创建一个伸缩组。

## 接口说明 {#description .section}

伸缩组是具有相同应用场景的ECS实例的集合。

-   最多支持在一个地域下创建50个伸缩组。
-   伸缩组创建成功后不会立即生效。您需要先调用[EnableScalingGroup](~~25939~~)接口启用伸缩组，伸缩组才能触发伸缩活动和执行伸缩规则。
-   伸缩组、关联的负载均衡实例和关联的RDS实例必须在同一个地域。更多详情，请参见[地域与可用区](~~40654~~)。
-   如果您为伸缩组关联了负载均衡实例，伸缩组会自动将加入伸缩组的ECS实例添加到负载均衡实例的后端服务器组。ECS实例在加入负载均衡实例的后端服务器组后，权重默认为50。负载均衡实例需要满足以下条件：
    -   该负载均衡实例的状态必须是active，您可以调用[DescribeLoadBalancers](~~27582~~)接口查看指定负载均衡实例的状态。
    -   该负载均衡实例配置的所有监听端口必须开启健康检查，否则伸缩组创建失败。
-   如果您为伸缩组关联了RDS实例，伸缩组会自动将加入伸缩组的ECS实例的内网IP添加到RDS实例的访问白名单。RDS实例需要满足以下条件：
    -   该RDS实例的状态必须是Running，您可以调用[DescribeDBInstances](~~26232~~)接口查看指定RDS实例的状态。
    -   该RDS实例访问白名单的IP数不能超过上限值。更多详情，请参见RDS文档[设置白名单](~~26198~~)。
-   如果伸缩组的MultiAZPolicy设置为COST\_OPTIMIZED：
    -   当指定OnDemandBaseCapacity、OnDemandPercentageAboveBaseCapacity和SpotInstancePools参数时，

        即指定成本优化策略下的实例分配方式，在扩缩容时将优先满足该实例分配方式。

    -   当不指定OnDemandBaseCapacity、OnDemandPercentageAboveBaseCapacity或SpotInstancePools参数时，

        成本优化策略下将仅按照成本最低的方式进行实例创建。


## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=CreateScalingGroup&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|MaxSize|Integer|是|20|伸缩组内ECS实例台数的最大值，取值范围：0~1000。 当伸缩组内ECS实例数大于MaxSize时，弹性伸缩会自动移出ECS实例。

 |
|MinSize|Integer|是|2|伸缩组内ECS实例台数的最小值，取值范围：0~1000 。当伸缩组内ECS实例数小于MinSize时，弹性伸缩会自动创建ECS实例。

 |
|RegionId|String|是|cn-qingdao|伸缩组所属的地域ID。更多详情，请参见[地域与可用区](~~40654~~)。

 |
|Action|String|否|CreateScalingGroup|系统规定参数。取值：CreateScalingGroup。

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。

 |
|DBInstanceIds|String|否|\["rm-idx", "rm-idy", "rm-idz"\]|RDS实例ID。取值可以是由多台RDS实例ID组成一个JSON数组，最多支持8个ID，ID之间用半角逗号（,）隔开。

 |
|DefaultCooldown|Integer|否|300|一次伸缩活动（添加或移出ECS实例）结束后的一段冷却时间。取值范围：0~86400，单位：秒。

 默认值：300。

 冷却时间内，该伸缩组不执行其它的伸缩活动，仅针对[云监控](~~35170~~)报警任务触发的伸缩活动有效。

 |
|HealthCheckType|String|否|tcp|TCP协议监听的健康检查方式，取值范围：

 -   tcp
-   http

 |
|LaunchTemplateId|String|否|lt-m5e3ofjr1zn1aw7\*\*\*\*|实例启动模板ID，用于指定伸缩组从实例启动模板获取启动配置信息。

 |
|LaunchTemplateVersion|String|否|Default|实例启动模板的版本，取值范围：

 -   固定的模板版本号
-   Default：始终使用模板默认版本
-   Latest：始终使用模板最新版本

 |
|LifecycleHook.N.DefaultResult|String|否|CONTINUE|等待状态结束后的下一步动作，取值范围：

 -   CONTINUE：继续响应弹性扩张活动或者继续响应弹性收缩活动。
-   ABANDON：直接释放弹性扩张活动创建出来的ECS实例或者直接将弹性收缩活动中的ECS实例从伸缩组移除。

 默认值：CONTINUE。

 当伸缩组发生弹性收缩活动（SCALE\_IN）并触发多个生命周期挂钩时，DefaultResult取值为ABANDON的生命周期挂钩触发的等待状态结束时，会提前将其它对应的等待状态提前结束。其他情况下，下一步动作均以最后一个结束等待状态的下一步动作为准。

 |
|LifecycleHook.N.HeartbeatTimeout|Integer|否|600|生命周期挂钩为伸缩组活动设置的等待时间，等待状态超时后会执行下一步动作。取值范围：30~21600，单位：秒。

 默认值：600。

 创建了生命周期挂钩后，您可以调用[RecordLifecycleActionHeartbeat](~~73846~~)延长ECS实例的等待时间，也可以调用[CompleteLifecycleAction](~~73847~~)提前结束伸缩活动的等待状态。

 |
|LifecycleHook.N.LifecycleHookName|String|否|lifecycle\_hook|生命周期挂钩名称，用于指定生命周期挂钩，不支持修改。

 |
|LifecycleHook.N.LifecycleTransition|String|否|SCALE\_OUT|生命周期挂钩适用的伸缩活动类型，取值范围：

 -   SCALE\_OUT：伸缩组弹性扩张活动
-   SCALE\_IN：伸缩组弹性收缩活动

 |
|LifecycleHook.N.NotificationArn|String|否|acs:ess:cn-hangzhou:1111111111:queue/queue2|生命周期挂钩通知对象标识符，支持消息服务MNS队列或主题，参数取值格式：acs:ess:\{region\}:\{account-id\}:\{resource-relative-id\}。

 -   region：伸缩组所在的地域
-   account-id：阿里云账号ID

 例如：

 -   MNS队列：acs:ess:\{region\}:\{account-id\}:queue/\{queuename\}
-   MNS主题：acs:ess:\{region\}:\{account-id\}:topic/\{topicname\}

 |
|LifecycleHook.N.NotificationMetadata|String|否|Test|伸缩活动的等待状态的固定字符串信息。参数长度不能超过128个字符。弹性伸缩每次推送消息到通知对象时，会同时发送您预先指定的NotificationMetadata参数值，便于管理和标记不同类别的通知信息。当您同时指定了NotificationArn参数时，NotificationMetadata参数方可生效。

 |
|LoadBalancerIds|String|否|\["lb-idx", "lb-idy", "lb-idz"\]|负载均衡实例ID。取值可以是由多台负载均衡实例ID组成一个JSON数组，最多支持5个ID，ID之间用半角逗号（,）隔开。

 |
|MultiAZPolicy|String|否|PRIORITY|多可用区伸缩组ECS实例扩缩容策略。取值范围：

 -   PRIORITY：根据您定义的虚拟交换机（VSwitchIds.N）扩缩容。当优先级较高的虚拟交换机所在可用区无法创建ECS实例时，自动使用下一优先级的虚拟交换机创建ECS实例。
-   COST\_OPTIMIZED：按vCPU单价从低到高进行尝试创建。当伸缩配置设置了抢占式计费方式的多实例规格时，优先创建对应抢占式计费实例。当抢占式计费实例由于库存等原因无法创建时，自动尝试以按量付费的方式创建。

**说明：** COST\_OPTIMIZED仅在伸缩配置设置了多实例规格或者选用了抢占式实例的情况下生效。

-   BALANCE：在伸缩组指定的多可用区之间均匀分配ECS实例。如果由于库存不足等原因可用区之间变得不平衡，您可以通过API [RebalanceInstance](~~71516~~)平衡资源。

 默认值：PRIORITY 。

 |
|OnDemandBaseCapacity|Integer|否|30|伸缩组所需要按量实例个数的最小值，取值范围：0~1000。当按量实例个数少于该值时，将优先创建按量实例。

 |
|OnDemandPercentageAboveBaseCapacity|Integer|否|20|伸缩组满足最小按量实例数（OnDemandBaseCapacity）要求后，超出的实例中按量实例应占的比例，取值范围：0～100。

 |
|RemovalPolicy.1|String|否|OldestScalingConfiguration|RemovalPolicy.N指定移出ECS实例的伸缩组策略，N的取值范围：1~2。更多详情，请参见[移出策略](~~25910~~)。取值范围：

 -   OldestInstance：移出最早加入伸缩组的ECS实例
-   NewestInstance：移出最新加入伸缩组的ECS实例
-   OldestScalingConfiguration：移出最早伸缩配置创建的ECS实例

 RemovalPolicy.1的默认值：OldestScalingConfiguration。

 RemovalPolicy.2的默认值：OldestInstance。

 |
|ScalingGroupName|String|否|测试sg|伸缩组的名称，同一地域下伸缩组名称唯一。长度为2~40个英文或中文字符，以数字、大小英文字母或中文开头，可以包含数字、下划线（\_）、连字符（-）和小数点（.）。

 默认值为伸缩组ID。

 |
|ScalingPolicy|String|否|recycle|指定伸缩组的回收模式，取值范围：

 -   recycle：伸缩组的回收模式为停机回收模式
-   release：伸缩组的回收模式为释放模式

 关于被移出实例的动作，请参见[RemoveInstances](~~25955~~)。

 |
|SpotInstancePools|Integer|否|5|指定可用实例规格的个数，伸缩组将按成本最低的多个规格均衡创建抢占式实例。取值范围：0~10。

 |
|SpotInstanceRemedy|Boolean|否|true|是否开启补齐抢占式实例。开启后，当收到抢占式实例将被回收的系统消息时，伸缩组将尝试创建新的实例，替换掉将被回收的抢占式实例。

 |
|VServerGroup.N.LoadBalancerId|String|否|lb-\*\*\*\*|虚拟服务器组所属负载均衡实例的ID。

 更多信息，请参见[AttachVServerGroups](~~98983~~)。

 |
|VServerGroup.N.VServerGroupAttribute.N.Port|Integer|否|22|弹性伸缩将ECS实例添加到虚拟服务器组时使用的端口号，取值范围：1~65535。

 更多信息，请参见[AttachVServerGroups](~~98983~~)。

 |
|VServerGroup.N.VServerGroupAttribute.N.VServerGroupId|String|否|rsp-\*\*\*\*|虚拟服务器组ID。

 更多信息，请参见[AttachVServerGroups](~~98983~~)。

 |
|VServerGroup.N.VServerGroupAttribute.N.Weight|Integer|否|100|弹性伸缩将ECS实例添加到虚拟服务器组时设置的权重，取值范围：0~100。

 默认值：50。

 更多信息，请参见[AttachVServerGroups](~~98983~~)。

 |
|VSwitchId|String|否|vsw-\*\*\*\*|创建VPC类型的伸缩组时，指定的虚拟交换机ID。

 |
|VSwitchIds.N|RepeatList|否|vsw-\*\*\*\*|一台或多台虚拟交换机的ID，N的取值范围：1~5。如果您使用了VSwitchIds.N参数，VSwitchId参数将被忽略。

 只有当伸缩组网络类型为VPC时，当前参数才生效。指定虚拟交换机所属的VPC必须和伸缩组所属的VPC相同。

 虚拟交换机可以来自多个可用区。虚拟交换机的优先级按照数字升序排序，1表示最高优先级。当优先级较高的虚拟交换机所在可用区无法创建ECS实例时，自动选择下一优先级的虚拟交换机创建ECS实例。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|ScalingGroupId|String|dP8VqSd9ENXPc0ciVmbc\*\*\*\*|伸缩组ID。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=CreateScalingGroup
&RegionId=cn-qingdao
&MaxSize=20
&MinSize=2
&LoadBalancerId=147b46d767c-cn-qingdao-cm5****
&DBInstanceId.1=rdszzzyyuny****
&DBInstanceId.2=rdsia3u3yia****
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateScalingGroupResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <ScalingGroupId>dP8VqSd9ENXPc0ciVmbc****</ScalingGroupId>
</CreateScalingGroupResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"ScalingGroupId":"dP8VqSd9ENXPc0ciVmbc****",
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述

|
|----------|-----|------|----|
|400

|IncorrectDBInstanceStatus

|The current status of DB instance “XXX” does not support this action.

|指定RDS实例的状态必须是Running。

|
|400

|IncorrectLoadBalancerHealthCheck

|The current health check type of specified load balancer does not support this action.

|指定的负载均衡实例必须开启健康检查。

|
|400

|IncorrectLoadBalancerStatus

|The current status of the specified load balancer does not support this action.

|指定负载均衡实例的状态必须是active。

|
|400

|IncorrectVSwitchStatus

|The current status of virtual switch does not support this operation.

|虚拟交换机不可用，无法创建ECS实例。

|
|400

|InvalidDBInstanceId. RegionMismatch

|DB instance “XXX” and the specified scaling group are not in the same Region.

|指定的RDS实例与伸缩组必须在同一地域。

|
|400

|InvalidLoadBalancerId.IncorrectAddressType

|The current address type of specified load balancer does not support this action.

|指定虚拟交换机后，负载均衡实例为私网类型。

|
|400

|InvalidLoadBalancerId.IncorrectInstanceNetworkType

|The network type of the instance in specified Load Balancer does not support this action.

|指定的负载均衡实例内搭载的ECS实例的网络类型与伸缩组的网络类型必须一致。

|
|400

|InvalidLoadBalancerId.RegionMismatch

|The specified Load Balancer and the specified scaling group are not in the same Region.

|指定的负载均衡实例与伸缩组必须在同一地域。

|
|400

|InvalidLoadBalancerId.VPCMismatch

|The specified virtual switch and the instance in specified Load Balancer are not in the same VPC.

|伸缩组内的负载均衡实例搭载的ECS实例与虚拟交换机应该在同一个VPC中。

|
|400

|InvalidParameter

|The specified value of parameter "ScalingPolicy" is not valid.

|指定的回收模式参数不存在。

|
|400

|InvalidParameter.Conflict

|The value of parameter <parameter name\> and parameter <parameter name\> are conflict.

|指定的MinSize不能大于MaxSize。

|
|400

|InvalidScalingGroupName.Duplicate

|The specified value of parameter <parameter name\> is duplicated.

|伸缩组名已存在。

|
|400

|QuotaExceeded.DBInstanceSecurityIP

|Security IP quota exceeded in DB instance “XXX”.

|指定的RDS实例访问白名单的IP个数达到上限。

|
|400

|QuotaExceeded.PrivateIpAddress

|Private IP address quota exceeded in the specified virtual switch.

|虚拟交换机无法再分配多余的私有IP地址。

|
|400

|QuotaExceeded.ScalingGroup

|Scaling group quota exceeded.

|用户的伸缩组使用个数达到上限。

|
|400

|QuotaExceeded.VPCInstance

|Instance quota exceeded in the specified VPC.

|该VPC内的实例数超过数量限制。

|
|404

|InvalidDBInstanceId.NotFound

|DB instance “XXX” does not exist.

|指定的RDS实例不存在。

|
|404

|InvalidLoadBalancerId.NotFound

|The specified Load Balancer does not exist.

|指定的负载均衡实例不存在。

|
|404

|InvalidRegionId.NotFound

|The specified region does not exist.

|指定的地域不存在。

|
|404

|InvalidVSwitchId.NotFound

|The specified virtual switch does not exist.

|指定的虚拟交换机不存在。

|
|400

|LaunchTemplateVersionSet.NotFound

|The specific version of launch template is not exist.

|实例启动模板指定版本不存在。

|
|400

|LaunchTemplateSet.NotFound

|The specified launch template set is not found.

|指定实例启动模板不存在。

|
|400

|TemplateMissingParameter.ImageId

|The input parameter "ImageId" that is mandatory for processing this request is not supplied.

|实例启动模板指定版本缺少镜像信息。

|
|400

|TemplateMissingParameter.InstanceTypes

|The input parameter "InstanceTypes" that is mandatory for processing this request is not supplied.

|实例启动模板指定版本缺少实例规格信息。

|
|400

|TemplateMissingParameter.SecurityGroup

|The input parameter "SecurityGroup" that is mandatory for processing this request is not supplied.

|实例启动模板指定版本缺少安全组信息。

|
|400

|TemplateVersion.NotNumber

|The input parameter "LaunchTemplateVersion" is supposed to be a string representing the version number.

|指定实例启动模板固定版本号为非数字。

|

