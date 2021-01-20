# DeleteAlarm

调用DeleteAlarm删除一个报警任务。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ess&api=DeleteAlarm&type=RPC&version=2014-08-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteAlarm|系统规定参数。取值：DeleteAlarm |
|AlarmTaskId|String|是|asg-bp1hvbnmkl10vll5\*\*\*\*\_f95ce797-dc2e-4bad-9618-14fee7d1\*\*\*\*|报警任务ID。 |
|RegionId|String|是|cn-qingdao|地域ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AlarmTaskId|String|asg-bp1hvbnmkl10vll5\*\*\*\*\_f95ce797-dc2e-4bad-9618-14fee7d1\*\*\*\*|报警任务ID。 |
|RequestId|String|6EF9BFEE-FE07-4627-B8FB-14326FB9\*\*\*\*|请求ID。 |

## 示例

请求示例

```
https://ess.aliyuncs.com/?Action=DeleteAlarm
&RegionId=cn-qingdao
&AlarmTaskId=asg-bp1hvbnmkl10vll5****_f95ce797-dc2e-4bad-9618-14fee7d1****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeleteAlarmResponse>
    <AlarmTaskId>asg-bp1hvbnmkl10vll5****_f95ce797-dc2e-4bad-9618-14fee7d1****</AlarmTaskId>
    <RequestId>6EF9BFEE-FE07-4627-B8FB-14326FB9****</RequestId>
</DeleteAlarmResponse>
```

`JSON` 格式

```
{
	"AlarmTaskId": "asg-bp1hvbnmkl10vll5****_f95ce797-dc2e-4bad-9618-14fee7d1****",
	"RequestId": "6EF9BFEE-FE07-4627-B8FB-14326FB9****"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ess)查看更多错误码。

