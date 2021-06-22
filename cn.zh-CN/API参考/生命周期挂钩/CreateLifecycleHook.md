# CreateLifecycleHook

调用CreateLifecycleHook为伸缩组创建一个或多个生命周期挂钩。

## 接口说明

一个伸缩组最多可以创建6个生命周期挂钩。创建了生命周期挂钩的伸缩组，在发生伸缩活动时，生命周期挂钩会暂停伸缩活动一段时间，具体等待时长可以通过HeartbeatTimeout参数指定。您可以在等待期间进行初始化ECS实例配置、获取ECS实例数据等操作。

弹性扩张活动时，ECS实例添加至RDS实例白名单后进入等待状态，等待状态结束后再加入SLB实例后端服务器组。弹性收缩活动时，ECS实例从SLB实例后端服务器组移出后进入等待状态，等待状态结束后再从RDS实例白名单移出。

生命周期挂钩可以配置通知方式，支持MNS主题、MNS队列和OOS模板。如果配置OOS模板，您需要为OOS服务创建RAM角色。具体操作，请参见[为OOS服务设置RAM权限](~~120810~~)。

**说明：** 如果伸缩组有存量的ECS实例，且配置的OOS模板用于加入或移出除RDS外的其他云数据库白名单，则您必须手动将存量的ECS实例加入云数据库的白名单。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=CreateLifecycleHook&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateLifecycleHook|系统规定参数。取值：CreateLifecycleHook |
|LifecycleTransition|String|是|SCALE\_OUT|生命周期挂钩适用的伸缩活动类型，取值范围：

 -   SCALE\_OUT：伸缩组弹性扩张活动
-   SCALE\_IN：伸缩组弹性收缩活动 |
|ScalingGroupId|String|是|asg-bp1eyv4qn8ssgv43\*\*\*\*|伸缩组的ID。 |
|LifecycleHookName|String|否|lifecyclehook\*\*\*\*|生命周期挂钩的名称。不能与当前伸缩组其他生命周期挂钩重名，长度为2~64个英文或中文字符，以数字、大小写字母或中文开头，可包含数字、下划线（\_）、短划线（-）和英文句号（.）。

 默认值为LifecycleHookId的值。 |
|DefaultResult|String|否|CONTINUE|等待状态结束后的下一步动作，取值范围：

 -   CONTINUE：继续响应弹性扩张活动或者继续响应弹性收缩活动。
-   ABANDON：直接释放弹性扩张活动创建出来的ECS实例或者直接将弹性收缩活动中的ECS实例从伸缩组移除。

 当伸缩组发生弹性收缩活动（SCALE\_IN）并触发多个生命周期挂钩时，DefaultResult为ABANDON的生命周期挂钩触发的等待状态结束时，会提前将其它对应的等待状态提前结束。其他情况下，下一步动作均以最后一个结束等待状态的下一步动作为准。

 默认值：CONTINUE |
|HeartbeatTimeout|Integer|否|600|生命周期挂钩为伸缩组活动设置的等待时间，等待状态超时后会执行下一步动作。取值范围：30~21600，单位：秒。

 创建了生命周期挂钩后，您可以调用[RecordLifecycleActionHeartbeat](~~73846~~)延长ECS实例的等待时间，也可以调用[CompleteLifecycleAction](~~73847~~)提前结束伸缩活动的等待状态。

 默认值：600 |
|NotificationMetadata|String|否|Test lifecycle hook.|生命周期挂钩暂停伸缩活动时推送给NotificationArn（通知对象）的通知信息，便于管理和标记不同类别的通知信息。必须同时指定NotificationArn。参数长度不能超过4096个字符。

 如果NotificationArn指定为OOS模板，包括公共模板或者自定义模板，则NotificationMetadata必须指定为JSON字符串，且与OOS模板的参数相符。比如，`{"dbInstanceId": "dds-bp17661e0135****", "modifyMode": "Append"}`，`dbInstanceId`和`modifyMode`为OOS模板中已定义的参数。OOS模板的部分参数有默认值，NotificationMetadata必须指定无默认值的参数，指定有默认值的参数时会覆盖原默认值，但以下参数请保持默认值，用于在伸缩活动运行时获取相关信息：

 -   `regionId`：伸缩活动执行的地域，默认为$\{regionId\}
-   `instanceIds`：伸缩活动关联的实例列表，默认为$\{instanceIds\}
-   `lifecycleHookId`：生命周期挂钩ID，默认为$\{lifecycleHookId\}
-   `lifecycleActionToken`：伸缩活动的等待状态标识符，用于提前结束当前的挂起活动，默认为$\{lifecycleActionToken\}
-   `scalingGroupId`：伸缩活动所属的伸缩组ID，默认为$\{scalingGroupId\}

 **说明：** 您可以在[OOS控制台](https://oos.console.aliyun.com/)获取对应模板的参数信息。 |
|NotificationArn|String|否|acs:mns:cn-beijing:161456884340\*\*\*\*:queue/modifyLifecycleHo\*\*\*\*|生命周期挂钩通知对象标识符，不设置本参数表示不发送通知，设置本参数时支持以下通知方式：

 -   消息服务MNS队列，参数取值格式：acs:mns:\{region-id\}:\{account-id\}:queue/\{queuename\} 。
-   消息服务MNS主题，参数取值格式：acs:mns:\{region-id\}:\{account-id\}:topic/\{topicname\}。
-   运维编排OOS模板，参数取值格式：acs:oos:\{region-id\}:\{account-id\}:template/\{templatename\}。

 参数格式中的变量含义如下：

 -   region-id：伸缩组所在的地域的ID。
-   account-id：阿里云账号ID，不支持RAM用户的账号ID。
-   queuename：MNS队列的名称。
-   topicname：MNS主题的名称。
-   templatename：OOS模板的名称。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|LifecycleHookId|String|ash-bp1at9ufhmcf9cmy\*\*\*\*|生命周期挂钩的D。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=CreateLifecycleHook
&ScalingGroupId=asg-bp1eyv4qn8ssgv43****
&LifecycleHookName=lifecyclehook****
&LifecycleTransition=SCALE_OUT
&NotificationArn=acs:mns:cn-beijing:161456884340****:queue/modifyLifecycleHo****
&NotificationMetadata=Test lifecycle hook.
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateLifecycleHookResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <LifecycleHookId>ash-bp1at9ufhmcf9cmy****</LifecycleHookId>
</CreateLifecycleHookResponse>
```

`JSON`格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "LifecycleHookId": "ash-bp1at9ufhmcf9cmy****"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Ess)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|400

|InvalidParamter

|The specified value of parameter is not valid.

|参数值不合法。 |
|400

|InvalidNotificationArn

|The specified parameter notificationArn is invalid.

|指定的NotificationArn不合法。 |
|400

|UnsupportedNotificationType.CurrentRegion

|The notificationType is not supported in the special region which scalingGroup belongs to.

|当前地域不支持该通知方式。 |
|400

|QueueNotExist

|The specified queue does not exist.

|指定的MNS队列不存在。 |
|400

|TopicNotExist

|The specified topic does not exist.

|指定的MNS主题不存在。 |
|400

|InvalidLifecycleHookName.Duplicate

|The specified value of parameter lifecycleHookName is duplicated.

|生命周期挂钩已存在。 |
|400

|QuotaExceeded.LifecycleHook

|Lifecycle hook quota exceeded in the specified scaling group.

|一个伸缩组最多可以创建6个生命周期挂钩。 |

