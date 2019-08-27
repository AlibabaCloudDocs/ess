# DescribeScalingGroups {#doc_api_Ess_DescribeScalingGroups .reference}

调用DescribeScalingGroups查询伸缩组。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DescribeScalingGroups&type=RPC&version=2014-08-28)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-qingdao|伸缩组所属地域的ID。

 |
|Action|String|否|DescribeScalingGroups|系统规定参数。取值：DescribeScalingGroups。

 |
|PageNumber|Integer|否|1|伸缩组列表的页码。起始值：1。

 默认值：1 。

 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。最大值：50。

 默认值：10。

 |
|ScalingGroupId.1|String|否|dyrSuvBOtO1dEdIlIbp\*\*\*\*|ScalingGroupId.N为待查询伸缩组的ID，N的取值范围：1～20。查询结果会忽略失效的伸缩组ID，并且不报错。

 |
|ScalingGroupName.1|String|否|dyrSuvBOtO1dEdIlIbp\*\*\*\*|ScalingGroupName.N为待查询伸缩组的名称，N的取值范围：1～20。查询结果会忽略失效的伸缩组名称，并且不报错。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|当前页码。

 |
|PageSize|Integer|50|每页行数。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |
|ScalingGroups| | |伸缩组信息的集合。

 |
|ActiveCapacity|Integer|1|已成功加入伸缩组,并正常运行的ECS实例数量。

 |
|ActiveScalingConfigurationId|String|dyo713cNYIB4ddEVlKbc\*\*\*\*|伸缩组内生效的伸缩配置的ID。

 |
|CreationTime|String|2014-08-14T10:58Z|伸缩组的创建时间。

 |
|DBInstanceIds| |rdszzzyyuny\*\*\*\*|伸缩组关联RDS实例的ID。

 |
|DefaultCooldown|Integer|60|伸缩组默认的冷却时间。冷却时间内，该伸缩组不执行其它的伸缩活动，仅针对[云监控](~~35170~~)报警任务触发的伸缩活动有效。

 |
|HealthCheckType|String|ECS|伸缩组的健康检查方式，取值范围：

 -   NONE：不做健康检查。
-   ECS：对伸缩组内的ECS实例做健康检查。

 |
|LaunchTemplateId|String|lt-m5e3ofjr1zn1aw7\*\*\*\*|伸缩组使用的实例启动模板的ID。

 |
|LaunchTemplateVersion|String|true|伸缩组使用的实例启动模板的版本。

 |
|LifecycleState|String|Active|伸缩组的状态信息，取值范围：

 -   Active：生效状态，处于生效状态的伸缩组才能接收执行伸缩规则的请求并触发伸缩活动。
-   Inacitve：失效状态，处于失效状态的伸缩组不接收任何执行伸缩规则的请求。
-   Deleting：伸缩组正在删除，处于删除中状态的伸缩组不接收任何执行伸缩规则的请求，并且不能修改伸缩组相关参数。

 |
|LoadBalancerIds| |147b46d767c-cn-qingdao-cm5\*\*\*\*|伸缩组关联的负载均衡实例的ID列表。

 |
|MaxSize|Integer|2|伸缩组内ECS实例台数的最大值。

 |
|MinSize|Integer|1|伸缩组内ECS实例台数的最小值。

 |
|ModificationTime|String|2014-08-14T10:58Z|修改时间。

 |
|MultiAZPolicy|String|PRIORITY|多可用区伸缩组ECS实例扩缩容策略。取值范围：

 -   PRIORITY：根据您定义的虚拟交换机（VSwitchIds.N）扩缩容。当优先级较高的虚拟交换机所在可用区无法创建ECS实例时，自动使用下一优先级的虚拟交换机创建ECS实例。
-   COST\_OPTIMIZED：按vCPU单价从低到高进行尝试创建。当伸缩配置设置了抢占式计费方式的多实例规格时，优先创建对应抢占式计费实例。当抢占式计费实例由于库存等原因无法创建时，自动尝试以按量付费的方式创建。

**说明：** COST\_OPTIMIZED仅在伸缩配置设置了多实例规格或者选用了抢占式实例的情况下生效。

-   BALANCE：在伸缩组指定的多可用区之间均匀分配ECS实例。如果由于库存不足等原因可用区之间变得不平衡，您可以通过API [RebalanceInstance](~~71516~~)平衡资源。

 |
|OnDemandBaseCapacity|Integer|30|伸缩组所需要按量实例个数的最小值，取值范围：0~1000。当按量实例个数少于该值时，将优先创建按量实例。

 |
|OnDemandPercentageAboveBaseCapacity|Integer|20|伸缩组满足最小按量实例数（OnDemandBaseCapacity）要求后，超出的实例中按量实例应占的比例，取值范围：0～100。

 |
|PendingCapacity|Integer|0|正在加入伸缩组，还未完成相关配置的ECS实例的数量。

 |
|PendingWaitCapacity|Integer|1|伸缩组中处于加入挂起状态的ECS实例的数量。

 |
|ProtectedCapacity|Integer|1|伸缩组中处于保护中状态的ECS实例的数量。

 |
|RegionId|String|cn-qingdao|伸缩组所属的地域的ID。

 |
|RemovalPolicies| |OldestScalingConfiguration|ECS实例移出伸缩组的策略的集合。

 |
|RemovingCapacity|Integer|0|正在移出伸缩组的ECS实例的数量。

 |
|RemovingWaitCapacity|Integer|1|伸缩组中处于移除挂起状态的ECS实例的数量。

 |
|ScalingGroupId|String|dyrSuvBOtO1dEdIlIbp\*\*\*\*|伸缩组的ID。

 |
|ScalingGroupName|String|dyrSuvBOtO1dEdIlIbp\*\*\*\*|伸缩组的名称。

 |
|ScalingPolicy|String|recycle|指定伸缩组的回收模式，取值范围：

 -   recycle：伸缩组的回收模式为停机回收模式
-   release：伸缩组的回收模式为释放模式

 关于被移出实例的动作，请参见[RemoveInstances](~~25955~~)。

 |
|SpotInstancePools|Integer|5|指定可用实例规格的个数，伸缩组将按成本最低的多个规格均衡创建抢占式实例。取值范围：0~10。

 |
|SpotInstanceRemedy|Boolean|true|是否开启补齐抢占式实例。开启后，当收到抢占式实例将被回收的系统消息时，伸缩组将尝试创建新的实例，替换掉将被回收的抢占式实例。

 |
|StandbyCapacity|Integer|1|伸缩组中处于备用状态的实例数量。

 |
|StoppedCapacity|Integer|1|伸缩组中处于停机不收费状态的实例数量。

 |
|TotalCapacity|Integer|1|伸缩组内所有ECS实例的数量。

 |
|VServerGroups| | |后端服务器组列表。

 |
|LoadBalancerId|String|147b46d767c-cn-qingdao-cm5\*\*\*\*|后端服务器组所属的负载均衡实例的ID。

 |
|VServerGroupAttributes| | |后端服务器组属性。

 |
|Port|Integer|22|负载均衡实例对外提供服务的端口号。

 |
|VServerGroupId|String|rsp-bp12bjrny\*\*\*\*|后端服务器组的ID。

 |
|Weight|Integer|1|后端服务器组的权重。

 |
|VSwitchId|String|vpc-25j4g\*\*\*\*|伸缩组关联虚拟交换机的ID。

 |
|VSwitchIds| |vpc-25j4g\*\*\*\*|伸缩组关联虚拟交换机的ID集合。如果您使用了VSwitchIds参数，VSwitchId参数将被忽略。

 |
|VpcId|String|vpc-\*\*\*\*|伸缩组所属VPC的ID。

 |
|TotalCount|Integer|1|伸缩组的总数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ess.aliyuncs.com/?Action=DescribeScalingGroups
&RegionId=cn-qingdao
&PageSize=50
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeScalingGroupsResponse>
      <RequestId>6393C3A8-B611-42F2-AFA6-F080FC45D5D0</RequestId>
      <TotalCount>1</TotalCount>
      <PageNumber>1</PageNumber>
      <PageSize>10</PageSize>
      <ScalingGroups> 
            <ScalingGroup>
                  <ActiveCapacity>1</ActiveCapacity>
                  <ActiveScalingConfigurationId>dyo713cNYIB4ddEVlKbc****</ActiveScalingConfigurationId>
                  <DBInstanceIds>
                        <DBInstanceId>rdszzzyyuny****</DBInstanceId>
                  </DBInstanceIds>
                  <VSwitchId>vpc-25j4g****</VSwitchId>
                  <DefaultCooldown>20</DefaultCooldown>
                  <LifecycleState>Active</LifecycleState>
                  <LoadBalancerIds>
                        <LoadBalancerId>147b46d767c-cn-qingdao-cm5****</LoadBalancerId>
                  </LoadBalancerIds>
                  <MaxSize>1</MaxSize>
                  <MinSize>0</MinSize>
                  <PendingCapacity>0</PendingCapacity>
                  <RegionId>cn-qingdao</RegionId>
                  <RemovingCapacity>0</RemovingCapacity>
                  <ScalingGroupId>dyrSuvBOtO1dEdIlIbp****</ScalingGroupId>
                  <ScalingGroupName>dyrSuvBOtO1dEdIlIbp****</ScalingGroupName>
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

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":10,
	"RequestId":"68386699-8B9E-4D5B-BC4C-75A28F6C2A00",
	"ScalingGroups":{
		"ScalingGroup":[
			{
				"DefaultCooldown":300,
				"MaxSize":2,
				"RemovalPolicies":{
					"RemovalPolicy":[
						"OldestScalingConfiguration",
						"OldestInstance"
					]
				},
				"PendingCapacity":0,
				"RemovingCapacity":0,
				"VSwitchId":"vpc-25j4g****",
				"ScalingGroupName":"b8pYCVbIV5k9cz4PWpbe****",
				"CreationTime":"2014-08-14T10:58Z",
				"ActiveCapacity":0,
				"ActiveScalingConfigurationId":" dyo713cNYIB4ddEVlKbc****",
				"ScalingGroupId":"b8pYCVbIV5k9cz4PWpbe****",
				"RegionId":"cn-qingdao",
				"TotalCapacity":0,
				"DBInstanceIds":{
					"DBInstanceId":[
						"rdsia3u3yia****",
						"rdszzzyyuny****"
					]
				},
				"LoadBalancerIds":{
					"LoadBalancerId":[
						"147b46d767c-cn-qingdao-cm5****"
					]
				},
				"MinSize":1,
				"LifecycleState":"Inactive"
			}
		]
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

