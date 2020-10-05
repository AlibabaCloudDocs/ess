# Configure parameters in a scaling configuration to implement automatic deployment

Auto Scaling automatically adds and removes ECS instances based on your business requirements. To provide more flexible scaling services, Auto Scaling allows you to configure the following settings in a scaling configuration to customize ECS instances: tags, Secure Shell \(SSH\) key pairs, Resource Access Management \(RAM\) roles, and user data. This topic describes tags, SSH key pairs, RAM roles, and user data, and how to configure them in a scaling configuration.

Before you perform the operations provided in the tutorial, you must have registered an Alibaba Cloud account. To create an Alibaba Cloud account, click [Create a new Alibaba Cloud account](https://account.alibabacloud.com/register/intl_register.htm).

Auto Scaling can automatically scale ECS instances during peak or off-peak traffic hours, and can also automatically deploy applications on ECS instances. Auto Scaling allows you to configure various parameters in a scaling configuration to customize ECS instances efficiently and flexibly based on your business requirements.

-   Tags

    For more information about tags, see [Overview](/intl.en-US/Tag & Resource/Tags/Overview.md). Tags can be used to identify resources and user groups. Enterprises and individuals can use tags to categorize their ECS resources to simplify search and aggregation of resources. When you create a scaling configuration, you can select tags to be bound to the ECS instances that are created based on the scaling configuration.

    If you call an API operation to create a scaling configuration, you can use the Tags parameter to specify tags. For more information, see [CreateScalingConfiguration](/intl.en-US/API Reference/Scaling configuration/CreateScalingConfiguration.md).

-   SSH key pairs

    For more information, see [Overview](/intl.en-US/Security/Key pairs/Overview.md). Alibaba Cloud supports only 2048-bit RSA key pairs. SSH key pairs apply only to Linux instances. After an SSH key pair is created, Alibaba Cloud stores the public key and offers you the private key.

    Compared with logons to ECS instances by using passwords, logons to ECS instances by using SSH key pairs are more efficient and secure. You can specify an SSH key pair when you create a scaling configuration. After Auto Scaling creates an ECS instance based on the scaling configuration, the instance stores the public key of the specified SSH key pair. You can use the private key to log on to the ECS instance from your local device. Note that:

    If you call an API operation to create a scaling configuration, you can use the KeyPairName parameter to specify an SSH key pair. For more information, see [CreateScalingConfiguration](/intl.en-US/API Reference/Scaling configuration/CreateScalingConfiguration.md).

-   RAM roles

    RAM is a service provided by Alibaba Cloud to manage user identities and resource access permissions. RAM allows you to create different roles and grant different permissions on Alibaba Cloud services to each role.

    For more information about RAM roles, see [Overview](/intl.en-US/Security/Instance RAM roles/Overview.md). An ECS instance can assume a RAM role to obtain the permissions granted to the RAM role. When you specify a RAM role in a scaling configuration, make sure that ECS has been selected as the trusted entity of the RAM role. Otherwise, Auto Scaling cannot create ECS instances based on the scaling configuration.

    If you call an API operation to create a scaling configuration, you can use the RamRoleName parameter to specify a RAM role. For more information, see [CreateScalingConfiguration](/intl.en-US/API Reference/Scaling configuration/CreateScalingConfiguration.md).

-   User data

    For more information about user data of ECS instances, see [Prepare user data](/intl.en-US/Instance/Manage instances/User data/Prepare user data.md). Both Windows and Linux instances support user data. You can use user data for the following scenarios:

    -   Configure a script that is run when an ECS instance starts. In this way, you can customize the startup behavior of the ECS instance.
    -   Pass data to an ECS instance. You can reference the data on the ECS instance.
    Compared with using open source IT infrastructure management tools such as Terraform, the method of using user data that is natively supported by Auto Scaling to manage the infrastructure is more efficient and secure. You only need to configure a Base64-encoded custom script and pass the script to a scaling configuration as user data. ECS instances created based on the scaling configuration can run the script upon startup to automatically deploy applications. In this way, you can scale applications. Take note of the following items:

    -   The network type of the scaling group must be Virtual Private Cloud \(VPC\).
    -   The user data must be Base64-encoded.
    -   We recommend that you do not configure confidential information, such as passwords and private keys in user data because user data is passed to instances in plaintext. If you must pass confidential information, we recommend that you encrypt the confidential information based on Base64 and decrypt the information on the instance.
    If you call an API operation to create a scaling configuration, you can use the UserData parameter to configure user data. For more information, see [CreateScalingConfiguration](/intl.en-US/API Reference/Scaling configuration/CreateScalingConfiguration.md).


Proper use of Auto Scaling can reduce your costs on servers, service management, and operations and maintenance \(O&M\). To help you understand and properly use Auto Scaling, this topic demonstrates how to configure the preceding parameters in a scaling configuration for Auto Scaling to automatically scale and customize ECS instances. Specifically, this topic demonstrates how to configure tags, an SSH key pair, a RAM role, and user data containing a custom script in a scaling configuration. When an ECS instance is created based on the scaling configuration, the tags are bound to the ECS instance, and the ECS instance assumes the RAM role. You can use the SSH key pair to log on to the ECS instance. The custom script is automatically run when the ECS instance starts.

## Procedure

Perform the following steps to configure custom settings, including tags, an SSH key pair, a RAM role, and user data, in a scaling configuration:

1.  [Step 1: Prepare custom settings](#section_t39_o4v_qs9)
2.  [Step 2: Apply the preceding settings](#section_vhc_c1q_x9k)
3.  [Step 3: Verify the preceding settings](#section_l2v_k5s_gnr)

## Step 1: Prepare custom settings

Perform the following operations to create tags, an SSH key pair, a RAM role, and user data:

1.  Create tags.

    For more information, see [Create or bind a tag](/intl.en-US/Tag & Resource/Tags/Create or bind a tag.md).

2.  Create an SSH key pair.

    For more information, see [Create an SSH key pair](/intl.en-US/Security/Key pairs/Use an SSH key pair/Create an SSH key pair.md).

3.  Create a RAM role.

    For more information, see [Create a RAM role for a trusted Alibaba Cloud service](/intl.en-US/RAM Role Management/Create a RAM role/Create a RAM role for a trusted Alibaba Cloud service.md). You can also use an existing RAM role. When you specify a RAM role in a scaling configuration, make sure that ECS has been selected as the trusted entity of the RAM role. Otherwise, Auto Scaling cannot create ECS instances based on the scaling configuration. For example, the RAM role `AliyunECSImageExportDefaultRole` grants the permission of exporting images. The trust policy of the RAM role allows all ECS instances in the current account to assume this RAM role. The following section shows the policy content:

    ```
    {
        "Statement": [
            {
                "Action": "sts:AssumeRole",
                "Effect": "Allow",
                "Principal": {
                    "Service": [
                        "ecs.aliyuncs.com"
                    ]
                }
            }
        ],
        "Version": "1"
    }
    ```

    **Note:** `ecs.aliyuncs.com` in the preceding policy indicates that all ECS instances in the current account can assume this RAM role.

4.  Prepare user data.

    For more information, see [Prepare user data](/intl.en-US/Instance/Manage instances/User data/Prepare user data.md). In this example, a shell script is provided in user data to write the following string to the /root/output10.txt file when an ECS instance starts for the first time: `Hello World. The time is now {Current time}`. The following section shows the script:

    ```
    #! /bin/sh
    echo "Hello World.  The time is now $(date -R)!" | tee /root/output10.txt
    ```

    The following section shows the Base64-encoded string of the script:

    ```
    IyEvYmluL3NoDQplY2hvICJIZWxsbyBXb3JsZC4gIFRoZSB0aW1lIGlzIG5vdyAkKGRhdGUgLVIpISIgfCB0ZWUgL3Jvb3Qvb3V0cHV0MTAudHh0 
    ```


## Step 2: Apply the preceding settings

Perform the following operations to create a scaling group and a scaling configuration and apply the preceding settings in the scaling configuration:

1.  Create a scaling group and view details of the scaling group after it is created.

    For more information, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md). Take note of the following items:

    -   Minimum Number of Instances: Set this parameter to 1. An ECS instance is automatically created after the scaling group is enabled.
    -   Instance Template Source: Set this parameter to **Create from Scratch**.
    -   Network Type: Set this parameter to **VPC** and specify a VPC and a VSwitch.
2.  Create and enable a scaling configuration after it is created.

    For more information, see [Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md). Take note of the following items:

    -   In the **Basic Configurations** step, set Image to Ubuntu 16.04 64-bit.
    -   In the **System Configurations \(Optional\)** step, select the tags, SSH key pair, RAM role, and user data that were created in Step 1.
3.  Enable the scaling group.

    For more information, see [Enable a scaling group](/intl.en-US/Scaling Group/Scaling group/Enable a scaling group.md).


## Step 3: Verify the preceding settings

In Step 2, the minimum number of instances in the scaling group is set to 1. Therefore, an ECS instance is automatically created after the scaling group is enabled.

1.  View the automatically created ECS instance.

    For more information, see [View ECS instances](/intl.en-US/Instance Management/ECS instance/View ECS instances.md).

2.  Click the instance ID to view details of the instance in the **ECS Instance ID/Name** column.

    The following figure shows details of the instance. You can find that the instance has assumed the RAM role and the tags have been bound to the instance.

    ![View instance details](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7281438951/p60674.png)

3.  Use the SSH key pair to log on to the instance.

    For more information, see [Connect to a Linux instance by using an SSH key pair](/intl.en-US/Instance/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using an SSH key pair.md). The following figure shows a successful logon. This indicates that the SSH key pair is in effect.

    ![Use the SSH key pair to log on to the instance](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7281438951/p60668.png)

4.  Run the following command to view the content of the /root/output10.txt file:

    ```
    cat /root/output10.txt
    ```

    The following figure shows the file content. This indicates that the user data configured in the scaling configuration is in effect.

    ![User data that takes effect](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7281438951/p60667.png)

    **Note:** A simple shell script is used in this example. You can create a script based on your requirements to customize more startup behaviors.


