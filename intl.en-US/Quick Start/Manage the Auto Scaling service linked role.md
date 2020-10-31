# Manage the Auto Scaling service linked role

This topic describes how to use the Auto Scaling service linked role to grant access permissions on Alibaba Cloud resources to Auto Scaling.

If you are a Resource Access Management \(RAM\) user, make sure that you are granted permissions on Auto Scaling. For more information, see [Grant permissions to a RAM user](/intl.en-US/RAM User Management/Grant permissions to a RAM user.md).

The following section shows the permissions to be added:

**Note:** Replace <account ID\> with the ID of your Alibaba Cloud account.

```
{
    "Statement": [
        {
            "Action": [
                "ram:CreateServiceLinkedRole"
            ],
            "Resource": "acs:ram:*:<account ID>:role/*",
            "Effect": "Allow",
            "Condition": {
                "StringEquals": {
                    "ram:ServiceName": [
                        "ess.aliyuncs.com"
                    ]
                }
            }
        }
    ],
    "Version": "1"
}
```

The Auto Scaling service linked role \(AliyunServiceRoleForAutoScaling\) is a RAM role that enables Auto Scaling to access other Alibaba Cloud resources. You can use AliyunServiceRoleForAutoScaling to enable Auto Scaling to access Elastic Compute Service \(ECS\), Virtual Private Cloud \(VPC\), ApsaraDB RDS \(RDS\), Server Load Balancer \(SLB\), Operation Orchestration Service \(OOS\), Message Service \(MNS\), and Cloud Monitor. For more information, see [Service linked roles](/intl.en-US/RAM Role Management/Service linked roles.md).

## Create AliyunServiceRoleForAutoScaling

When you use Auto Scaling, the system checks whether the AliyunServiceRoleForAutoScaling role is attached to your account. If the AliyunServiceRoleForAutoScaling role is not attached to your account, the system creates the role for your account.

The AliyunServiceRolePolicyForAutoScaling system policy is attached to AliyunServiceRoleForAutoScaling. System policies attached to service linked roles are defined and used by corresponding Alibaba Cloud services. You cannot add, modify, or delete the permissions of service linked roles. You can view policies attached to a RAM role in the RAM role details. For more information, see [View the basic information of a RAM role](/intl.en-US/RAM Role Management/View the basic information of a RAM role.md).

## Delete AliyunServiceRoleForAutoScaling

If you do not need the AliyunServiceRoleForAutoScaling service linked role for the moment and understand the impacts of not using the role, you can delete it. For example, when you do not need scaling groups to create and manage resources, you can delete the service linked role. For more information, see [Delete a RAM role](/intl.en-US/RAM Role Management/Delete a RAM role.md).

**Note:** Before you delete AliyunServiceRoleForAutoScaling, you must delete resources of Auto Scaling in all regions in your current account, including scaling groups, scheduled tasks, and event-triggered tasks. Otherwise, AliyunServiceRoleForAutoScaling cannot be deleted.

After you delete AliyunServiceRoleForAutoScaling, you cannot use Auto Scaling to create or manage resources.

