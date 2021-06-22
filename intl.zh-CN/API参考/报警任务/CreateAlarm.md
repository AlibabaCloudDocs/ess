# CreateAlarm

调用CreateAlarm创建一个报警任务。

## 接口说明

报警任务支持的系统监控项的数据由云监控采集，您需要配合维度信息确定监控数据的聚合范围。例如，指定user\_id和scaling\_group即确定聚合该用户、该伸缩组下所有ECS实例的监控项数据。

监控项和维度信息的配合关系如下：

|监控项

|描述

|维度信息 |
|-----|----|------|
|CpuUtilization

|CPU使用率（%）

|user\_id、scaling\_group |
|ClassicInternetRx

|经典网络外网入流量（KB/min）

|user\_id、scaling\_group |
|ClassicInternetTx

|经典网络外网出流量（KB/min）

|user\_id、scaling\_group |
|VpcInternetRx

|VPC网络外网入流量（KB/min）

|user\_id、scaling\_group |
|VpcInternetTx

|VPC网络外网出流量（KB/min）

|user\_id、scaling\_group |
|IntranetRx

|内网入流量（KB/min）

|user\_id、scaling\_group |
|IntranetTx

|内网出流量（KB/min）

|user\_id、scaling\_group |
|LoadAverage

|系统平均负载

|user\_id、scaling\_group |
|MemoryUtilization

|内存使用率（%）

|user\_id、scaling\_group |
|SystemDiskReadBps

|系统盘读BPS（Byte/s）

|user\_id、scaling\_group |
|SystemDiskWriteBps

|系统盘写BPS（Byte/s）

|user\_id、scaling\_group |
|SystemDiskReadOps

|系统盘读IOPS（次/s）

|user\_id、scaling\_group |
|SystemDiskWriteOps

|系统盘写IOPS（次/s）

|user\_id、scaling\_group |
|PackagesNetIn

|网卡收包数（个/s）

|user\_id、scaling\_group、device |
|PackagesNetOut

|网卡发包数（个/s）

|user\_id、scaling\_group、device |
|TcpConnection

|TCP连接数（个）

|user\_id、scaling\_group、state |

其中，user\_id和scaling\_group由系统自动填充，device、state需要您手动指定。更多信息，请参见参数Dimension.N.DimensionKey和Dimension.N.DimensionValue。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=CreateAlarm&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateAlarm|系统规定参数。取值：CreateAlarm |
|MetricName|String|是|CpuUtilization|监控项名称。取值范围：

 -   CpuUtilization：CPU使用率（%）。
-   ClassicInternetRx：经典网络外网入流量（KB/min）。
-   ClassicInternetTx：经典网络外网出流量（KB/min）。
-   VpcInternetRx：VPC网络外网入流量（KB/min）。
-   VpcInternetTx：VPC网络外网出流量（KB/min）。
-   IntranetRx：内网入流量（KB/min）。
-   IntranetTx：内网出流量（KB/min）。
-   LoadAverage：系统平均负载。
-   MemoryUtilization：内存使用率（%）。
-   SystemDiskReadBps：系统盘读BPS（Byte/s）。
-   SystemDiskWriteBps：系统盘写BPS（Byte/s）。
-   SystemDiskReadOps：系统盘读IOPS（次/s）。
-   SystemDiskWriteOps：系统盘写IOPS（次/s）。
-   PackagesNetIn：网卡收包数（个/s）。
-   PackagesNetOut：网卡发包数（个/s）。
-   TcpConnection：TCP连接数（个）。

 更多信息，请参见接口说明。 |
|RegionId|String|是|cn-qingdao|地域ID。 |
|ScalingGroupId|String|是|asg-bp18p2yfxow2dloq\*\*\*\*|报警任务关联的伸缩组的ID。 |
|Threshold|Float|是|80|监控指标的阈值，满足阈值表达式达到指定次数即触发执行伸缩规则。 |
|Name|String|否|TestAlarmTask|报警任务的名称。 |
|Description|String|否|Test alarm task.|报警任务的描述。 |
|AlarmAction.N|RepeatList|否|ari:acs:ess:cn-hangzhou:1406926\*\*\*\*:scalingrule/asr-bp163l21e07uhn\*\*\*\*|报警任务关联伸缩规则的唯一标识符。 |
|MetricType|String|否|system|监控项类型。取值范围：

 -   system：使用云监控系统指标。
-   custom：使用上报到云监控的自定义指标。 |
|Period|Integer|否|300|统计监控项数据的周期，单位：秒。取值范围：

 -   60
-   120
-   300
-   900

 默认值：300 |
|Statistics|String|否|Average|统计监控项数据的方法。取值范围：

 -   Average：平均值。
-   Minimum：最小值。
-   Maximum：最大值。

 默认值：Average |
|ComparisonOperator|String|否|\>=|监控项统计值与阈值的比较符，用于指定监控项统计值与阈值在什么关系下满足条件。取值范围：

 -   监控项统计值大于等于阈值。取值：\>=
-   监控项统计值小于等于阈值。取值：<=
-   监控项统计值大于阈值。取值：\>
-   监控项统计值小于阈值。取值：<

 默认值：\>= |
|EvaluationCount|Integer|否|3|触发执行伸缩规则需要满足阈值表达式的次数，例如，CPU使用率平均值3次的统计结果均大于等于80%。

 默认值：3 |
|Dimension.N.DimensionKey|String|否|device|监控项关联的维度信息键。取值范围：

 -   user\_id：您的账号ID。
-   scaling\_group：被监控的伸缩组。
-   device：网卡设备的类型。
-   state：TCP连接的状态。 |
|Dimension.N.DimensionValue|String|否|eth0|监控项关联的维度信息值，取值范围由维度信息键决定。

 user\_id：由系统自动填充。

 scaling\_group：由系统自动填充。

 device取值范围：

 -   eth0：对于经典网络实例，eth0表示内网网卡。对于VPC实例，只存在eth0一张网卡。
-   eth1：对于经典网络实例，eth1代表外网网卡。

 state取值范围：

 -   TCP\_TOTAL：表示总的TCP连接数。
-   ESTABLISHED：表示已建立的TCP连接数。 |
|GroupId|Integer|否|4055401|自定义监控项所属云监控应用分组的ID，仅在监控项类型为custom时需要指定该参数。 |
|Effective|String|否|TZ=+00 \* \* 1-2 \* \* ?|指定报警任务的生效时间段，默认所有时间都生效。

 该参数遵循Cron表达式，默认格式为`X X X X X ?`，含义如下：

 -   X：一个域的占位符，依次表示秒、分钟、小时、日期和月。X可以是确定的取值，也可以是具有逻辑意义的特殊字符。X的取值范围，请参见[Cron表达式](~~25907~~)。
-   ？：表示不指定值。

 **说明：** 该参数指定值**默认为UTC+8时区**，支持在Cron表达式之前添加时区信息`TZ=+yy`来指定时区，其中y表示时区的数值。例如，`TZ=+00 * * 1-2 * * ?`表示报警任务在UTC+0时区每天01:00~02:59之间生效。

 取值示例及含义如下：

 -   `* * * * * ?`：所有时间都生效
-   `* * 17-18 * * ?`：在UTC+8时区每天17:00~18:59之间生效
-   `TZ=+00 * * 1-2 * * ?`：在UTC+0时区每天01:00~02:59之间生效 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AlarmTaskId|String|asg-bp1hvbnmkl10vll5\*\*\*\*\_f95ce797-dc2e-4bad-9618-14fee7d1\*\*\*\*|报警任务ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3\*\*\*\*|请求ID。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=CreateAlarm
&RegionId=cn-qingdao
&ScalingGroupId=asg-bp18p2yfxow2dloq****
&MetricName=CpuUtilization
&Threshold=80
&AlarmAction.1=ari:acs:ess:cn-hangzhou:1406926****:scalingrule/asr-bp163l21e07uhn****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateAlarmResponse>
    <AlarmTaskId>asg-bp1hvbnmkl10vll5****_f95ce797-dc2e-4bad-9618-14fee7d1****</AlarmTaskId>
    <RequestId>ADD82C07-7A7C-4DD4-907F-1D114742****</RequestId>
</CreateAlarmResponse>
```

`JSON`格式

```
{
	"AlarmTaskId":"asg-bp1hvbnmkl10vll5****_f95ce797-dc2e-4bad-9618-14fee7d1****",
	"RequestId":"ADD82C07-7A7C-4DD4-907F-1D114742****"
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

|InvalidParameter

|The specified value of parameter "%s" is not valid.

|指定参数“%s”不合法。 |

