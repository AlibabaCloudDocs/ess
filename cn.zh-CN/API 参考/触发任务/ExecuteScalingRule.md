# ExecuteScalingRule {#concept_25953_zh .concept}

执行一个指定的伸缩规则。

## 描述 {#section_e5k_vzk_sfb .section}

-   当伸缩组为active状态，才可以调用该接口。
-   当伸缩组没有伸缩活动正在执行，才可以调用该接口。
-   当伸缩组没有伸缩活动正在执行时，该接口可以绕过冷却时间（Cooldown）直接执行。
-   调用该接口返回成功，只是表示弹性伸缩服务接受了该接口的调用请求，伸缩活动可以执行，但不代表伸缩活动能够执行成功。用户需要通过返回的ScalingActivityId查看该伸缩活动的执行状态。
-   如果该伸缩规则需要增加的ECS实例数加上当前伸缩组的实例数（Total Capacity）大于MaxSize时，则按Total Capacity = MaxSize的规则进行执行。
-   如果当前伸缩组的实例数（Total Capacity）减去该伸缩规则需要减少的ECS实例数小于MinSize时，则按Total Capacity = MinSize的规则进行执行。
-   对于所有地域和所有伸缩组，一个用户最多能弹性伸缩1000台ECS实例。（此数量只包含自动创建的ECS实例，不包含手工添加的ECS实例。）

## 请求参数 {#section_xln_wzk_sfb .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：ExecuteScalingRule。|
|ScalingRuleAri|String|是|伸缩规则唯一标识符。|
|ClientToken|String|否|用于保证请求的幂等性。由客户端生成该参数值，要保证在不同请求间唯一，最大不超过64个ASCII字符。具体请参见附录 [如何保证幂等性](cn.zh-CN/API 参考/如何保证幂等性.md#)。|

## 返回参数 {#section_rbq_yzk_sfb .section}

|名称|类型|描述|
|:-|:-|:-|
|ScalingActivityId|String|伸缩活动的ID。|

## 示例 {#section_psp_11l_sfb .section}

请求示例

```
http://ess.aliyuncs.com/?Action=ExecuteScalingRule
&ScalingRuleAri=ari:acs:ess:cn-qingdao:1344371:scalingRule/cCBpdYdQuBe2cUxOdu6piOk
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ExecuteScalingRuleResponse>
    <ScalingActivityId>ebta5WbUzC8gcwUWvfchyT4U</ScalingActivityId>
    <RequestId>262216B9-F9D4-4D16-BE9B-BD1C39A4F42B</RequestId>
</ExecuteScalingRuleResponse>
```

`JSON` 格式

```
{
    "RequestId": "6469DCD0-13AC-487E-85A0-CE4922908FDE",
    "ScalingActivityId": "ebta5WbUzC8gcwUWvfchyT4U"
}
```

## 错误码 {#section_evn_d1l_sfb .section}

对于所有接口的通用性错误，请参考 [客户端错误](cn.zh-CN/API 参考/错误代码/客户端错误.md#) 或 [服务器端错误](cn.zh-CN/API 参考/错误代码/服务器端错误.md#)。

|HttpCode|错误码|错误信息|描述|
|--------|:--|:---|:-|
|404|InvalidScalingRuleAri.NotFound|The specified scaling rule Ari does not exist.|指定的伸缩规则在该用户账号下不存在。|
|403|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|用户并未向弹性伸缩完整授权Open API接口。|
|400|IncorrectScalingGroupStatus|The current status of the specified scaling group does not support this action.|指定伸缩规则所属的伸缩组为非active状态。|
|400|ScalingActivityInProgress|You cannot delete a scaling group or launch a new scaling activity while there is a scaling activity in progress for the specified scaling group.|指定伸缩规则所属的伸缩组有伸缩活动正在进行。|
|400|InsufficientBalance|Your account does not have enough balance.|用户账号余额不足。|
|400|QuotaExceed.Instance|Living instance quota exceeded.|用户的ECS实例个数使用达到上限。|
|400|IncorrectLoadBalancerStatus|The current status of the specified load balancer does not support this action.|指定伸缩规则所属的伸缩组的负载均衡实例为非active状态。|
|400|IncorrectLoadBalancerHealthCheck|The current health check type of specified load balancer does not support this action.|指定伸缩规则所属的伸缩组的负载均衡实例未开启健康检查。|
|400|InvalidLoadBalancerId.IncorrectInstanceNetworkType|The network type of the instance in specified load balancer does not support this action.|指定的负载均衡实例含有的ECS实例的网络类型与伸缩组的网络类型不匹配。|
|400|InvalidLoadBalancerId.VPCMismatch|The specified virtual switch and the instance in specified load balancer are not in the same VPC.|指定的伸缩组的负载均衡实例含有的ECS实例与VSwitchId不在同一个VPC当中。|
|400|IncorrectDBInstanceStatus|The current status of DB instance “XXX” does not support this action.|指定伸缩规则所属的伸缩组的RDS实例为非running状态。|
|400|QuotaExceeded.DBInstanceSecurityIP|Security IP quota exceeded in DB instance “XXX”.|指定伸缩规则所属的伸缩组的RDS实例访问白名单的IP个数达到上限。|
|400|QuotaExceeded.SecurityGroupInstance|Instance quota exceeded in the specified security group.|指定的安全组已添加的ECS实例个数达到上限。|
|400|IncorrectCapacity.NoChange|To execute the specified scaling rule, the total capacity will not change.|伸缩规则未造成伸缩组实例数的变化。|
|400|QuotaExceeded.ScalingInstance|Scaling instance quota exceeded.|弹性伸缩的ECS实例使用个数达到上限。|
|400|QuotaExceeded.AfterpayInstance|Living afterpay instance quota exceeded.|按量付费ECS实例的使用个数达到上限。|
|400|ResourceNotAvailable.ECS|The specified region or zone does not offer the specified disk or instance category.|指定的区域无法创建指定的ECS实例类型或磁盘类型。|

