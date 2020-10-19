# ModifyScheduledTask

调用ModifyScheduledTask修改一个定时任务的信息。

## 接口说明

定时任务支持两种伸缩方式：

-   通过ScheduledAction参数设置需要执行的伸缩规则。
-   通过ScalingGroupId参数设置伸缩组内实例数量。

**说明：** 不支持同时设置ScheduledAction和ScalingGroupId。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=ModifyScheduledTask&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyScheduledTask|系统规定参数。取值：ModifyScheduledTask |
|ScheduledTaskId|String|是|edRtShc57WGXdt8TlPbr\*\*\*\*|定时任务的ID。 |
|ScheduledTaskName|String|否|scheduled\*\*\*\*|定时任务的名称。2~64个英文或中文字符，以数字、大小字母或中文开头，可包含数字、下划线（\_）、连字符（-）或点号（.）。同一账号同一地域内唯一。 |
|Description|String|否|Test scheduled task.|定时任务的描述信息。2~200个英文或中文字符。 |
|ScheduledAction|String|否|ari:acs:ess:cn-hangzhou:14069264\*\*\*\*:scalingrule/asr-bp12tcnol686y1ik\*\*\*\*|定时任务触发时需要执行的伸缩规则，填写伸缩规则的唯一标识符。指定ScheduledAction后，定时任务的伸缩方式为选择已有伸缩规则。

 **说明：** 不支持同时设置ScheduledAction和ScalingGroupId。 |
|RecurrenceEndTime|String|否|2014-08-20T16:55Z|重复执行定时任务的结束时间。按照ISO8601标准表示，并需要使用UTC时间。格式为：YYYY-MM-DDThh:mmZ。不能填写自修改当天起365日后的时间。 |
|LaunchTime|String|否|2014-08-18T10:52Z|定时任务触发的时间点。按照ISO8601标准表示，并需要使用UTC时间。格式为：YYYY-MM-DDThh:mmZ。不能填写自修改当天起90日后的时间。

 如果指定了RecurrenceType，则此属性指定的时间点，默认为循环执行的时间点。

 如果未指定RecurrenceType，则按指定的日期和时间执行一次。 |
|RecurrenceType|String|否|Daily|重复执行定时任务的类型，取值范围：

 -   Daily：每多少天重复执行一次定时任务。
-   Weekly：每周指定几天重复执行一次定时任务。
-   Monthly：每月内指定几天重复执行一次定时任务。
-   Cron：按照指定的Cron表达式执行定时任务。

 修改后，RecurrenceType和RecurrenceValue需要同时有效。 |
|RecurrenceValue|String|否|2|重复执行定时任务的数值。

 -   RecurrenceType取Daily时，只能填一个值，取值范围：1~31。
-   RecurrenceType取Weekly时，可以填入多个值，填多个值时使用英文逗号（,）分隔。比如，周日、周一、周二、周三、周四、周五、周六的值依次为：0,1,2,3,4,5,6。
-   RecurrenceType取Monthly时，格式为A-B。A、B的取值范围为1~31，并且B必须大于等于A。
-   RecurrenceType取Cron时，表示UTC时间，支持分、时、日、月、星期的5域表达式，支持通配符英文逗号（,）、英文问号（?）、连字符（-）、星号（\*）、井号（\#）、斜线（/）、L和W。

 修改后，RecurrenceType和RecurrenceValue需要同时有效。 |
|TaskEnabled|Boolean|否|true|是否启动定时任务。

 -   true：启动定时任务。
-   false：停止定时任务。 |
|LaunchExpirationTime|Integer|否|600|定时任务触发操作失败后，在此时间内重试。单位为秒，取值范围：0~21600。 |
|MinValue|Integer|否|0|定时任务的伸缩方式为设置伸缩组内实例数量时，指定伸缩组内实例的最小数量。 |
|MaxValue|Integer|否|10|定时任务的伸缩方式为设置伸缩组内实例数量时，指定伸缩组内实例的最大数量。 |
|DesiredCapacity|Integer|否|10|定时任务的伸缩方式为设置伸缩组内实例数量时，指定伸缩组内实例的期望实例数。

 **说明：** 伸缩组必须支持设置期望实例数，即在创建该伸缩组时指定了DesiredCapacity。 |
|ScalingGroupId|String|否|asg-bp18p2yfxow2dloq\*\*\*\*|定时任务触发时需要修改实例数量的伸缩组，填写伸缩组ID。指定ScalingGroupId后，定时任务的伸缩方式为设置伸缩组内实例数量，您需要为MinValue、MaxValue和DesiredCapacity中至少一个参数指定数量。

 **说明：** 不支持同时设置ScheduledAction和ScalingGroupId。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3\*\*\*\*|请求ID。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=ModifyScheduledTask
&ScheduledTaskId=edRtShc57WGXdt8TlPbr****
&LaunchTime=2014-08-18T10:52Z
&RecurrenceEndTime=2014-08-20T16:55Z
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ModifyScheduledTaskResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3****</RequestId>
</ModifyScheduledTaskResponse>
```

`JSON` 格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3****"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ess)查看更多错误码。

|HttpCode

|错误码

|错误信息

|描述 |
|----------|-----|------|----|
|404

|InvalidScheduledTaskId.NotFound

|The specified scheduled task does not exist.

|指定的定时任务在该用户账号下不存在。 |
|400

|InvalidScheduledTaskName.Duplicate

|The specified value of parameter

`ScheduledTaskName`is duplicated.

|定时任务名已存在。 |
|400

|ScheduledAction.RegionMismatch

|The specified scheduled task and the specified scheduled action are not in the same Region.

|指定的ScheduledAction与定时任务所在的地域不匹配。 |

