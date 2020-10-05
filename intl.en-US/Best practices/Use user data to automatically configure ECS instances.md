# Use user data to automatically configure ECS instances

To provide more efficient and flexible scaling services, Auto Scaling allows you to configure user data in scaling configurations to customize ECS instances. You can pass in user data to perform automated configuration tasks on ECS instances, such as installing applications on ECS instances. This allows you to scale applications in a more secure and efficient manner.

Before you perform the operations provided in the tutorial, you must have registered an Alibaba Cloud account. To create an Alibaba Cloud account, click [Create a new Alibaba Cloud account](https://account.alibabacloud.com/register/intl_register.htm).

To verify the effect of user data, you must log on to ECS instances. We recommend that you use Secure Shell \(SSH\) key pairs to log on to Linux instances. For more information, see [Create an SSH key pair](/intl.en-US/Security/Key pairs/Use an SSH key pair/Create an SSH key pair.md) and [Connect to a Linux instance by using an SSH key pair](/intl.en-US/Instance/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using an SSH key pair.md).

An example is used in this topic to describe how to use user data in Auto Scaling. You can customize user data based on your business requirements.

For more information about user data, see [Prepare user data](/intl.en-US/Instance/Manage instances/User data/Prepare user data.md). Both Windows and Linux instances support user data. You can use user data for the following scenarios:

-   Configure a script that is run when an ECS instance starts. In this way, you can customize the startup behavior of the ECS instance.
-   Pass data to an ECS instance. You can reference the data on the ECS instance.

Compared with using open source IT infrastructure management tools such as Terraform, the method of using user data that is natively supported by Auto Scaling to manage the infrastructure is more efficient and secure. You only need to configure a Base64-encoded custom script and pass the script to a scaling configuration as user data. ECS instances created based on the scaling configuration can run the script upon startup to automatically deploy applications. In this way, you can scale applications. When you use user data, take note of the following items:

-   The network type of the scaling group must be Virtual Private Cloud \(VPC\).
-   The user data must be Base64-encoded.
-   We recommend that you do not configure confidential information such as passwords and private keys in user data because user data is passed to instances in plaintext. If you must pass confidential information, we recommend that you encrypt the confidential information based on Base64 and decrypt the information on the instance.

If you call an API operation to create a scaling configuration, you can use the UserData parameter to configure user data. For more information, see [CreateScalingConfiguration](/intl.en-US/API Reference/Scaling configuration/CreateScalingConfiguration.md).

In addition to user data, you can use SSH key pairs, Resource Access Management \(RAM\) roles, and tags to customize ECS instances efficiently and flexibly. For more information, see [t40616.md\#](/intl.en-US/Best practices/Set parameters of scaling configurations to customize ECS instances.md).

## Procedure

Perform the following steps to configure user data in a scaling configuration:

1.  [Step 1: Prepare user data](#section_kfp_0d6_w4t)
2.  [Step 2: Create and enable a scaling group](#section_7ls_gqc_gmp)
3.  [Step 3: Verify the user data](#section_zr5_zt2_4jd)

## Step 1: Prepare user data

You can configure a custom shell script in user data and enable the script to run when ECS instances start. When you customize a shell script, take note of the following items:

-   Format: The first line must start with `#!`, such as `#! /bin/sh`.
-   Limit: The script size cannot exceed 16 KB before the script is encoded in Base64.
-   Frequency: The script is run only when instances are started for the first time.

1.  Customize a shell script to configure the Domain Name System \(DNS\), Yellowdog Updater, Modified \(YUM\), and Network Time Protocol \(NTP\) services when an ECS instance starts.

    The following section shows the shell script:

    ```
    #! /bin/sh
    # Modify DNS
    echo "nameserver 8.8.8.8" | tee /etc/resolv.conf
    # Modify yum repo and update
    rm -rf /etc/yum.repos.d/*
    touch myrepo.repo
    echo "[base]" | tee /etc/yum.repos.d/myrepo.repo
    echo "name=myrepo" | tee -a /etc/yum.repos.d/myrepo.repo
    echo "baseurl=http://mirror.centos.org/centos" | tee -a /etc/yum.repos.d/myrepo.repo
    echo "gpgcheck=0" | tee -a /etc/yum.repos.d/myrepo.repo
    echo "enabled=1" | tee -a /etc/yum.repos.d/myrepo.repo
    yum update -y
    # Modify NTP Server
    echo "server ntp1.aliyun.com" | tee /etc/ntp.conf
    systemctl restart ntpd.service
    ```

2.  Encode the shell script in Base64.

    The following section shows the Base64-encoded shell script:

    ```
    IyEvYmluL3NoCiMgTW9kaWZ5IEROUwplY2hvICJuYW1lc2VydmVyIDguOC44LjgiIHwgdGVlIC9ldGMvcmVzb2x2LmNvbmYKIyBNb2RpZnkgeXVtIHJlcG8gYW5kIHVwZGF0ZQpybSAtcmYgL2V0Yy95dW0ucmVwb3MuZC8qCnRvdWNoIG15cmVwby5yZXBvCmVjaG8gIltiYXNlXSIgfCB0ZWUgL2V0Yy95dW0ucmVwb3MuZC9teXJlcG8ucmVwbwplY2hvICJuYW1lPW15cmVwbyIgfCB0ZWUgLWEgL2V0Yy95dW0ucmVwb3MuZC9teXJlcG8ucmVwbwplY2hvICJiYXNldXJsPWh0dHA6Ly9taXJyb3IuY2VudG9zLm9yZy9jZW50b3MiIHwgdGVlIC1hIC9ldGMveXVtLnJlcG9zLmQvbXlyZXBvLnJlcG8KZWNobyAiZ3BnY2hlY2s9MCIgfCB0ZWUgLWEgL2V0Yy95dW0ucmVwb3MuZC9teXJlcG8ucmVwbwplY2hvICJlbmFibGVkPTEiIHwgdGVlIC1hIC9ldGMveXVtLnJlcG9zLmQvbXlyZXBvLnJlcG8KeXVtIHVwZGF0ZSAteQojIE1vZGlmeSBOVFAgU2VydmVyCmVjaG8gInNlcnZlciBudHAxLmFsaXl1bi5jb20iIHwgdGVlIC9ldGMvbnRwLmNvbmYKc3lzdGVtY3RsIHJlc3RhcnQgbnRwZC5zZXJ2aWNl                      
    ```


## Step 2: Create and enable a scaling group

1.  Create a scaling group and view details of the scaling group after it is created.

    For more information, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md). Take note of the following items:

    -   Minimum Number of Instances: Set this parameter to 1. An ECS instance is automatically created after the scaling group is enabled.
    -   Instance Template Source: Set this parameter to **Create from Scratch**.
    -   Network Type: Set this parameter to **VPC** and specify a VPC and a VSwitch.
2.  Create and enable a scaling configuration after it is created.

    For more information, see [Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md). Take note of the following items:

    -   In the **Basic Configurations** step, set Image to Ubuntu 16.04 64-bit.
    -   In the **System Configurations \(Optional\)** step, pass in the user data that were created in Step 1 and select an existing SSH key pair.
3.  Enable the scaling group.

    For more information, see [Enable a scaling group](/intl.en-US/Scaling Group/Scaling group/Enable a scaling group.md).


## Step 3: Verify the user data

The minimum number of instances in the scaling group is set to 1. Therefore, an ECS instance is automatically created after the scaling group is enabled.

1.  View the scaling activity.

    For more information, see [View the details of a scaling activity](/intl.en-US/Monitoring/Scaling events/View the details of a scaling activity.md).

2.  Log on to the ECS instance.

    For more information, see [Connect to a Linux instance by using an SSH key pair](/intl.en-US/Instance/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using an SSH key pair.md).

3.  Check the status of services on the instance.

    The following figure shows that the DNS, YUM, and NTP services are enabled on the ECS instance. This indicates that the user data configured in the scaling configuration is in effect.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5281438951/p65781.png)


