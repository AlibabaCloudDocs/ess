# Create a scaling group {#concept_25870_zh .concept}

This topic gives you an example of how to make the CreateScalingGroup API request, and specifying MinSize and MaxSize.

```
http://ess.aliyuncs.com/?Action=CreateScalingGroup
&RegionId=cn-qingdao
&MaxSize=20
&MinSize=2
&LoadBalancerId=147b46d767c-cn-qingdao-cm5-a01
&DBInstanceId. 1=rdszzzyyunybaeu
&DBInstanceId. 2=rdsia3u3yia3u3y
&<Public Request Parameters>
```

## Response example { .section}

```
<CreateScalingGroupResponse>
    <ScalingGroupId>dP8VqSd9ENXPc0ciVmbcrBT1</ScalingGroupId>
    <RequestId>536E9CAD-DB30-4647-AC87-AA5CC38C5382</RequestId>
</CreateScalingGroupResponse>
```

