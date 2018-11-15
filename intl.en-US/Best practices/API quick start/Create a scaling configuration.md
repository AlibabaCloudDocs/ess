# Create a scaling configuration {#concept_25871_zh .concept}

You must specify the attributes of the ECS instances to be scaled, such as the ImageID and InstanceType. You must specify the ScalingGroupId returned in step 1.

```
http://ess.aliyuncs.com/?Action=CreateScalingConfiguration
&ScalingGroupId=dP8VqSd9ENXPc0ciVmbcrBT1
&SecurityGroupId=sg-280ih3w4b
&ImageId=centos6u5_64_20G_aliaegis_20140703.vhd
&InstanceType=ecs.t1.xsmall
&<common request parameters>
```

## Response example { .section}

```
<CreateScalingConfigurationResponse>
    <ScalingConfigurationId>eOs27Kb0oXvQcUYjEGelJqUy</ScalingConfigurationId>
    <RequestId>5CC0AD41-08ED-4559-A683-6F56355FE068</RequestId>
</CreateScalingConfigurationResponse>
```

