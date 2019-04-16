# DescribeScalingGroups {#concept_25938_zh .concept}

本文主要介绍查询伸缩组API操作。

## 描述 {#section_wdv_5zj_sfb .section}

查询伸缩组的信息。伸缩组具有以下几种状态（LifecycleState）：

-   Active：生效状态，在该状态下才能接收执行伸缩规则的请求并触发伸缩活动。
-   Inacitve：失效状态，在该状态下不接收任何执行伸缩规则的请求。
-   Deleting：伸缩组正在删除，在该状态下不接收任何执行伸缩规则的请求。

## 请求参数 { .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：DescribeScalingGroups。|
|RegionId|String|是|伸缩组所属的地域 ID。|
|ScalingGroupId.N|String|否|伸缩组的 ID，最多可以输入 20 个。查询结果会忽略失效的伸缩组 ID，并且不报错。|
|ScalingGroupName.N|String|否|伸缩组的名称，最多可以输入 20 个。查询结果会忽略失效的伸缩组名称，并且不报错。|
|PageNumber|Integer|否|伸缩组列表的页码，起始值为 1，默认值为 1。|
|PageSize|Integer|否|分页查询时设置的每页行数，最大值 50 行，默认值为10。|

## 返回参数 { .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|伸缩组的总数。|
|PageNumber|Integer|当前页码。|
|PageSize|Integer|每页行数。|
|ScalingGroups|ScalingGroupSetType|伸缩组信息的集合。|

ScalingGroupSetType 是由 ScalingGroupItemType 类型组成的集合。

|名称|类型|描述|
|:-|:-|:-|
|ScalingGroup|ScalingGroupItemType|伸缩组信息。|

ScalingGroupItemType 类型的属性如下表所示。

|名称|类型|描述|
|:-|:-|:-|
|ScalingGroupId|String|伸缩组的 ID。|
|ScalingGroupName|String|伸缩组的显示名称。|
|ActiveScalingConfigurationId|String|伸缩组内生效的伸缩配置 ID。|
|LaunchTemplateId|String|当前伸缩组使用的实例启动模板 ID|
|LaunchTemplateVersion|String|当前伸缩组使用的实例启动模板版本|
|RegionId|String|伸缩组所属的地域 ID。|
|MinSize|Integer|伸缩组内 ECS 实例个数的最小值。|
|MaxSize|Integer|伸缩组内 ECS 实例个数的最大值。|
|DefaultCooldown|Integer|伸缩组默认的冷却时间。|
|RemovalPolicies|RemovalPolicySetType|ECS 实例移出伸缩组的策略的集合。|
|LoadBalancerIds|List of LoadBalancerId|负载均衡实例的 ID列表。|
|DBInstanceIds|DBInstanceIdSetType|RDS 实例 ID 的集合。|
|VSwitchId|String|伸缩组对应虚拟交换机的 ID。|
|LifecycleState|String|伸缩组的状态信息。|
|TotalCapacity|Integer|伸缩组内所有 ECS 实例的数量。|
|ActiveCapacity|Integer|已成功加入伸缩组,并正常运行的 ECS 实例数量。|
|PendingCapacity|Integer|正在加入伸缩组，还未完成相关配置的 ECS 实例数量。|
|RemovingCapacity|Integer|正在移出伸缩组的 ECS 实例数。量。|
|CreationTime|String|伸缩组的创建时间。|

RemovalPolicySetType 是由 String 类型组成的集合。

|名称|类型|描述|
|:-|:-|:-|
|RemovalPolicy|String|ECS 实例移出伸缩组的策略。|

DBInstanceIdSetType 是由 String 类型组成的集合。

|名称|类型|描述|
|:-|:-|:-|
|DBInstanceId|String|RDS 实例的 ID。|

## 示例 { .section}

请求示例

```
http://ess.aliyuncs.com/?Action=DescribeScalingGroups
&RegionId=cn-qingdao
&PageSize=50
&<公共请求参数>
```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码 {#section_q3h_r1k_sfb .section}

关于所有接口的通用性错误，请参考 [客户端错误](intl.zh-CN/API参考/错误代码/客户端错误.md#) 或 [服务器端错误](intl.zh-CN/API参考/错误代码/服务器端错误.md#)。

