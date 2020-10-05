# 使用实例自定义数据自动配置ECS实例

为了提供更加高效灵活的伸缩服务，弹性伸缩配置中新增了实例自定义数据。您可以利用实例自定义数据自动完成ECS实例配置，从而安全快速地实现应用级别的扩容和缩容。

使用本教程进行操作前，请确保您已经注册了阿里云账号。如还未注册，请先完成[账号注册](https://account.alibabacloud.com/register/intl_register.htm)。

验证实例自定义数据效果时需要登录ECS实例，对Linux实例建议您使用密钥对，具体操作请参见[创建SSH密钥对](/intl.zh-CN/安全/SSH密钥对/使用SSH密钥对/创建SSH密钥对.md)和[使用SSH密钥对连接Linux实例](/intl.zh-CN/实例/连接实例/连接Linux实例/使用SSH密钥对连接Linux实例.md)。

本文结合具体场景向您展示实例自定义数据的使用方式，您可以根据自己的业务场景，灵活地定制实例自定义数据来满足您的业务需求。

实例自定义数据的介绍请参见[生成实例自定义数据](/intl.zh-CN/实例/管理实例/使用实例自定义数据/生成实例自定义数据.md)。Windows实例及Linux实例均支持实例自定义数据，主要有以下用途：

-   作为实例自定义脚本在启动实例时执行，您可以自定义实例的启动行为。
-   作为普通数据向实例传入信息，您可以在实例中引用这些数据。

相比Terraform等开源IT基础架构管理工具，使用弹性伸缩原生的实例自定义数据更加快速、安全。您只需要准备好实例自定义脚本，然后以Base64编码的方式传入伸缩配置即可，自动创建的ECS实例会在启动时自动执行实例自定义脚本，实现应用级别的扩容和缩容。但需要注意以下几点：

-   伸缩组的网络类型需要为专有网络（VPC）。
-   实例自定义数据需要为Base64编码方式。
-   实例自定义数据将以不加密的方式传入实例，请不要以明文方式传入机密的信息（例如密码、私钥数据等）。如果必须传入，建议先加密原始数据，以Base64方式编码加密后的数据并传入实例，然后在实例内部以同样的方式反解密。

通过API创建伸缩配置时，您可以使用UserData参数传入实例自定义数据，更多信息请参见[CreateScalingConfiguration](/intl.zh-CN/API参考/伸缩配置/CreateScalingConfiguration.md)。

除实例自定义数据外，SSH密钥对、RAM角色名称和标签也可以帮助您更加高效灵活地管理ECS实例，请参见[使用伸缩配置的特性实现自动部署](/intl.zh-CN/最佳实践/使用伸缩配置的特性实现自动部署.md)。

## 操作步骤

完成以下操作在伸缩配置中应用实例自定义数据：

1.  [步骤一：准备实例自定义数据](#section_kfp_0d6_w4t)
2.  [步骤二：创建并启用伸缩组](#section_7ls_gqc_gmp)
3.  [步骤三：验证实例自定义数据的效果](#section_zr5_zt2_4jd)

## 步骤一：准备实例自定义数据

您可以利用实例自定义数据实现在ECS实例启动时自动执行自定义shell脚本，在定义shell脚本时，需注意以下几点：

-   格式：首行固定为`#!`，例如`#!/bin/sh`。
-   限制：在Base64编码前脚本内容不能超过16 KB。
-   频率：仅在首次启动实例时执行一次。

1.  定义一个shell脚本，实现在ECS实例启动时配置DNS、yum和NTP服务。

    shell脚本内容如下：

    ```
    #!/bin/sh
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

2.  对shell脚本进行Base64编码。

    Base64编码后的shell脚本内容如下：

    ```
    IyEvYmluL3NoCiMgTW9kaWZ5IEROUwplY2hvICJuYW1lc2VydmVyIDguOC44LjgiIHwgdGVlIC9ldGMvcmVzb2x2LmNvbmYKIyBNb2RpZnkgeXVtIHJlcG8gYW5kIHVwZGF0ZQpybSAtcmYgL2V0Yy95dW0ucmVwb3MuZC8qCnRvdWNoIG15cmVwby5yZXBvCmVjaG8gIltiYXNlXSIgfCB0ZWUgL2V0Yy95dW0ucmVwb3MuZC9teXJlcG8ucmVwbwplY2hvICJuYW1lPW15cmVwbyIgfCB0ZWUgLWEgL2V0Yy95dW0ucmVwb3MuZC9teXJlcG8ucmVwbwplY2hvICJiYXNldXJsPWh0dHA6Ly9taXJyb3IuY2VudG9zLm9yZy9jZW50b3MiIHwgdGVlIC1hIC9ldGMveXVtLnJlcG9zLmQvbXlyZXBvLnJlcG8KZWNobyAiZ3BnY2hlY2s9MCIgfCB0ZWUgLWEgL2V0Yy95dW0ucmVwb3MuZC9teXJlcG8ucmVwbwplY2hvICJlbmFibGVkPTEiIHwgdGVlIC1hIC9ldGMveXVtLnJlcG9zLmQvbXlyZXBvLnJlcG8KeXVtIHVwZGF0ZSAteQojIE1vZGlmeSBOVFAgU2VydmVyCmVjaG8gInNlcnZlciBudHAxLmFsaXl1bi5jb20iIHwgdGVlIC9ldGMvbnRwLmNvbmYKc3lzdGVtY3RsIHJlc3RhcnQgbnRwZC5zZXJ2aWNl                      
    ```


## 步骤二：创建并启用伸缩组

1.  创建伸缩组，并在创建成功后查看伸缩组详情。

    具体操作请参见[创建伸缩组](/intl.zh-CN/伸缩组/伸缩组/创建伸缩组.md)，请注意：

    -   组内最小实例数：设为1，在启用伸缩组后即会自动创建一台实例。
    -   伸缩组内实例模板来源：选择**从零开始创建**。
    -   网络类型：选择**专有网络**，并指定专有网络的专有网络ID、虚拟交换机。
2.  创建伸缩配置，并在创建成功后启用配置。

    具体操作请参见[创建伸缩配置](/intl.zh-CN/伸缩组/组内实例配置信息来源/创建伸缩配置.md)，请注意：

    -   **基础配置**页面中，示例镜像选用Ubuntu 16.04 64位。
    -   **系统配置**页面中，应用步骤一中准备的实例自定义数据，登录凭证选择创建好的密钥对。
3.  启用伸缩组。

    具体操作请参见[启用伸缩组](/intl.zh-CN/伸缩组/伸缩组/启用伸缩组.md)。


## 步骤三：验证实例自定义数据的效果

由于创建伸缩组时指定伸缩最小实例数为1，在启用伸缩组后即会自动创建一台实例，保证伸缩组满足最小实例数的限制。

1.  查看伸缩活动。

    具体操作请参见[查看伸缩活动详情](/intl.zh-CN/监控/伸缩活动/查看伸缩活动详情.md)。

2.  登录ECS实例。

    具体操作请参见[使用SSH密钥对连接Linux实例](/intl.zh-CN/实例/连接实例/连接Linux实例/使用SSH密钥对连接Linux实例.md)。

3.  查看服务状态。

    服务状态如下图所示，DNS、yum和NTP服务已开启，可见伸缩配置中的实例自定义数据配置已生效。

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9956459951/p65781.png)


