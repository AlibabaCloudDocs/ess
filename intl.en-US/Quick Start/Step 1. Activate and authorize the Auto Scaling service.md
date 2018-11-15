# Step 1. Activate and authorize the Auto Scaling service {#concept_dnl_43m_qfb .concept}

This topic introduces the API information for activating and authorizing the Auto Scaling service.

## Authorization procedure {#section_dfv_r3m_qfb .section}

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  Click **Authorize** to go to the RAM console and grant authorization.
3.  Select **AliyunESSDefaultRole** and click **Agree to Authorize**.
4.  Return to the Auto Scaling console and refresh the page.

## Next step {#section_kkj_mkm_qfb .section}

After completing authorization, you can use the Auto Scaling service. Next, you can create your first scaling group in the desired region \(such as China \(Shanghai\)\). For more information, see [create a scaling group](reseller.en-US/Quick Start/Step 2. Create a scaling solution.md#).

## Permission list {#section_yqz_pkm_qfb .section}

By default, the role `AliyunESSDefaultRole` allows Auto Scaling to call the following Alibaba Cloud resources for you:

-   ECS permissions

    |Permission name|Description|
    |:--------------|:----------|
    |ecs:RunInstances|Create one or more ECS instances as needed.|
    |ecs:CreateInstance|Create ECS instances.|
    |ecs:StartInstance|Start ECS instances.|
    |ecs:AllocatePublicIpAddress|Allocate public IP addresses to ECS instances.|
    |ecs:StopInstance|Stop ECS instances.|
    |ecs:DeleteInstance|Delete ECS instances.|
    |ecs:DescribeInstances|Query ECS instance lists.|
    |ecs:DescribeInstanceAttribute|Query ECS instance attributes.|
    |ecs:ModifyInstanceAttribute|Modify ECS instance attributes.|
    |ecs:DescribeSecurityGroupAttribute|Query security group attributes.|
    |ecs:DescribeSnapshots|Query snapshot lists.|
    |ecs:DescribeKeyPairs|Query key pair lists.|

-   SLB permissions

    |Permission name|Description|
    |:--------------|:----------|
    |slb:DescribeLoadBalancerAttribute|Query SLB instance information.|
    |slb:RemoveBackendServers|Delete backend servers from a SLB instance.|
    |slb:DescribeHealthStatus|Check the health of the backend servers of a SLB instance.|
    |slb:AddBackendServers|Add backend servers to a SLB instance.|
    |slb:SetBackendServers|Configure backend server weights.|

-   RDS permissions

    |Permission name|Description|
    |:--------------|:----------|
    |rds:ModifySecurityIps|Modify the IP address whitelist of an RDS instance.|
    |rds:DescribeDBInstanceAttribute|View RDS instance details.|
    |rds:DescribeTaskInfo|Query RDS task information.|
    |rds:DescribeDBInstanceIPArrayList|View the IP address whitelist of an RDS instance.|

-   VPC permissions

    |Permission name|Description|
    |:--------------|:----------|
    |vpc:DescribeVpcs|Query VPC lists.|
    |vpc:DescribeVSwitches|Query VSwitch lists.|

-   MNS permissions

    |Permission name|Description|
    |:--------------|:----------|
    |mns:ListTopic|List topic lists under an account.|
    |mns:ListQueue|List queue lists under an account.|
    |mns:SendMessage|Send messages.|
    |mns:PublishMessage|Publish messages.|


The complete policy list for the role AliyunESSDefaultRole is as follows:

```
{
  "Version": "1",
  "Statement": [
    {
      "Action": [
        "ecs:CreateInstance",
        "ecs:RunInstances",
        "ecs:StartInstance",
        "ecs:AllocatePublicIpAddress",
        "ecs:StopInstance",
        "ecs:DeleteInstance",
        "ecs:DescribeInstances",
        "ecs:DescribeInstanceAttribute",
        "ecs:ModifyInstanceAttribute",
        "ecs:DescribeSecurityGroupAttribute",
        "ecs:DescribeImages",
        "ecs:DescribeSnapshots",
        "ecs:DescribeKeyPairs",
        "slb:DescribeLoadBalancerAttribute",
        "slb:RemoveBackendServers",
        "slb:DescribeHealthStatus",
        "slb:AddBackendServers",
        "slb:SetBackendServers",
        "rds:ModifySecurityIps",
        "rds:DescribeDBInstanceAttribute",
        "rds:DescribeTaskInfo",
        "rds:DescribeDBInstanceIPArrayList"
      ],
      "Resource": "*",
      "Effect": "Allow"
    },
    {
      "Action": [
        "vpc:DescribeVpcs",
        "vpc:DescribeVSwitches"
      ],
      "Resource": "*",
      "Effect": "Allow"
    },
    {
      "Action": [
        "mns:ListTopic",
        "mns:ListQueue",
        "mns:SendMessage",
        "mns:PublishMessage"
      ],
      "Resource": "*",
      "Effect": "Allow"
    },
    {
      "Action": "ram:PassRole",
      "Resource": "*",
      "Effect": "Allow",
      "Condition": {
        "StringEquals": {
          "acs:Service": "ecs.aliyuncs.com"
        }
      }
    }
  ]
}
```

