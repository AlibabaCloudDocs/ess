# Create a scheduled task {#concept_25874_zh .concept}

This topic is an example of API request `CreateScheduledTask` \(create a scheduled task\). You must specify the `ScalingRuleAri`.

```
http://ess.aliyuncs.com/?Action=CreateScheduledTask
&RegionId=cn-qingdao
&LaunchTime=2014-08-17T12:00Z
&RecurrenceType=Daily
&RecurrenceValue=1
&RecurrenceEndTime=2014-09-17T16:55Z
&ScheduledAction=ari:acs:ess:cn-qingdao:1344371:scalingrule/eMKWG8SRNb9dBLAjweNI1Ik
&<common request parameters>
```

## Response example { .section}

```
<CreateScheduledTaskResponse>
    <ScheduledTaskId>edRtShc57WGXdt8TlPbrjsnV</ScheduledTaskId>
    <RequestId>0F02D931-2B12-44D7-A0E9-39925C13D15E</RequestId>
</CreateScheduledTaskResponse>
```

