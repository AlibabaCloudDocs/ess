# Create a scaling rule {#concept_25873_zh .concept}

This topic is an example of API request `CreateScalingRule`\(create a scaling rule\). You must specify the `ScalingGroupId`.

```
http://ess.aliyuncs.com/?Action=CreateScalingRule
&ScalingGroupId=dP8VqSd9ENXPc0ciVmbcrBT1
&AdjustmentType=QuantityChangeInCapacity
&AdjustmentValue=1
&<common request parameters>
```

## Response example { .section}

```
<CreateScalingRuleResponse>   
<ScalingRuleAri>
ari:acs:ess:cn-qingdao:1344371:scalingrule/eMKWG8SRNb9dBLAjweNI1Ik
</ScalingRuleAri>
    <ScalingRuleId>eMKWG8SRNb9dBLAjweNI1Ik</ScalingRuleId>
    <RequestId>570C84F4-A434-488A-AFA1-1E3213682B33</RequestId>
</CreateScalingRuleResponse>
```

