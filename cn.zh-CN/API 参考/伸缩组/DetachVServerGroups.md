# DetachVServerGroups {#concept_a1p_sgz_zfb .concept}

您可以通过DetachVServerGroups移除一个或者多个虚拟服务器组。

## 描述 {#section_rwv_mjz_zfb .section}

确定待移除虚拟服务器组的方式为：负载均衡实例ID（LoadBalancerId） + 虚拟服务器组ID（VServerGroupId） + 虚拟服务器组端口号（Port） 。如果请求参数中的虚拟服务器组与伸缩组中的虚拟服务器组相匹配，则移除该虚拟服务器组；如果未能匹配，则忽略移除请求，接口不报错。

## 请求参数 {#section_axg_pjz_zfb .section}

|名称|类型|是否必选|描述|
|--|--|----|--|
|Action|String|是|操作接口名，系统规定参数，取值： DetachVServerGroups。|
|RegionId|String|是|伸缩组所属的地域ID，如cn-hangzhou、cn-shanghai。更多详情，请参阅 [地域和可用区](../../../../../cn.zh-CN/通用参考/地域和可用区.md#)。|
|ScalingGroupId|String|是|伸缩组ID。|
|VServerGroup.N.LoadBalancerId|String|是|虚拟服务器组所属负载均衡实例的ID。N 为负载均衡实例编号，取值范围：1-5。|
|VServerGroup.N.VServerGroupAttribute.M.VServerGroupId|String|是|虚拟服务器组ID。N 为负载均衡实例编号，取值范围：1-5。M 为负载均衡实例下虚拟服务器组的编号，取值范围：1-5。|
|VServerGroup.N.VServerGroupAttribute.M.Port|Integer|是|弹性伸缩将ECS实例添加到虚拟服务器组时使用的端口号，取值范围：1-65535。N 为负载均衡实例编号，取值范围：1-5。M 为负载均衡实例下虚拟服务器组的编号，取值范围：1-5。

|
|ForceDetach|Boolean|否|是否从待移除虚拟服务器组中移除当前伸缩组内的ECS实例。-   true：移除
-   false：不移除

默认值：false。

|

## 返回参数 {#section_j1y_f3z_zfb .section}

|名称|类型|描述|
|--|--|--|
|RequestId|String|请求ID。|

## 示例 {#section_lm4_j3z_zfb .section}

请求示例

```
http://ess.aliyuncs.com/?Action=DetachVServerGroups
&ScalingGroupId=asg-xxxxxxxxxxx
&RegionId=cn-hangzhou
&VServerGroup.1.LoadBalancerId=lb-xxxxxxx
&VServerGroup.1.VServerGroupAttribute.1.VServerGroupId=rsp-xxxxx
&VServerGroup.1.VServerGroupAttribute.1.Port=22
&VServerGroup.1.VServerGroupAttribute.2.VServerGroupId=rsp-xxxxx
&VServerGroup.1.VServerGroupAttribute.2.Port=80
&<公共请求参数>
```

正常返回示例

 `XML` 格式

```
<DetachVServerGroupsResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</DetachVServerGroupsResponse>
```

 `JSON` 格式

```
{
    "requestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 {#section_jh2_v3z_zfb .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|您未授予弹性伸缩完整的Open API调用权限。|
|404|InvalidScalingGroupId.NotFound|The specified scaling group does not exist.|账号下不存在指定的伸缩组。|
|400|InvalidParameter|The specified value of parameter "%s" is not valid.|参数值不合法。|
|400|MissingParameter|The input parameter "%s" that is mandatory for processing this request is not supplied.|缺少必要的参数。|

