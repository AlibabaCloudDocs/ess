# 让ESS更灵活的新特性 {#concept_63444_zh .concept}

弹性伸缩（Elastic Scaling Service, ESS）是一种根据业务需求和策略，自动调整其弹性计算资源的管理服务。在满足业务需求高峰增长时无缝地增加 ECS 实例，并在业务需求下降时自动减少ECS实例以节约成本。

为了提供更加弹性、灵活的伸缩服务，ESS弹性伸缩配置中新增了 UserData、KeyPair、RamRole、Tags 4个特性。使用 UserData，您可以快速安全的完成自动化的配置过程，在 ECS 实例数量随着业务需求弹性变化的同时，您还能够安全、快速地完成应用级别的扩容和缩容。您还可以通过配置 KeyPair、Tags 等参数，实现更加高效、智能的 ECS 实例管理服务。

本文将详细介绍ESS新增的 4 个特性，并结合具体场景，向您阐述这些特性在 ESS 中的使用方式。您可以根据自己的业务场景，灵活地使用这些特性来满足您的业务需求。

## 实例自定义数据 {#section_mh4_52n_qfb .section}

[实例自定义数据](../../../../cn.zh-CN/用户指南/实例/实例自定义数据和元数据/实例自定义数据.md#)（UserData），是阿里云 ECS 为您提供的一种自定义实例启动行为及传入数据的功能，该功能兼容 Windows 实例及 Linux 实例，主要有 2 种用途：

-   作为实例自定义脚本，在启动实例时执行。
-   作为普通数据，将一定的信息传入实例中，您可以在实例中引用这些数据。

使用ESS来满足您 ECS 实例数随着业务需求弹性伸缩的要求时，如果您还要自动化地实现应用级别的扩容和缩容，常用的方法可能是通过自定义镜像的方式来实现，也可能是通过使用 Terraform 等开源的IT基础架构管理工具来实现。

ESS 伸缩配置中添加了 UserData 参数以后，您只需要准备好您的 UserData 自定义脚本数据，然后以 Base64 编码的方式传入伸缩配置中即可。当ESS弹性扩容 ECS 实例数时，UserData 实例自定义脚本会在实例启动的时候自动地执行，从而帮您实现应用级别的扩容和缩容。相比借助于自定义镜像或其它开源工具来实现应用自动扩展的方法，使用 ESS 原生的 UserData 特性显得更加快捷、安全。

在创建伸缩配置，并使用了UserData参数时，需要注意以下几点：

-   专有网络（VPC）的伸缩配置才能使用UserData参数。
-   UserData 要以 Base64 编码的方式传入。
-   UserData 将以不加密的方式传入，所以请不要以明文方式传入机密的信息（比如密码、私钥数据等），如果必须传入，建议加密后，然后以 Base64 的方式编码后再传入，在实例内部以同样的方式反解密。

## SSH 秘钥对 { .section}

在使用 SSH 登录远程 Linux 服务器时，您可以选择使用密码的方式来登录，也可以选择使用 [SSH 秘钥对](../../../../cn.zh-CN/产品简介/网络和安全性/SSH 密钥对.md#) 的方式来登录。当您要管理的服务器集群较多时，频繁地输入密码不仅浪费时间，而且容易发生密码输入错误，无法登陆服务器的情况。

此时，如果您通过SSH 秘钥对的方式来登陆服务器，您只需要配置好您的公钥和私钥，即可登录到服务器。一次配置，长期有效。阿里云创建的SSH 秘钥对只支持RSA 2048位的密钥对。在生成秘钥的时候，阿里云会保存密钥的公钥部分，并返回给您秘钥的私钥部分。

ESS 弹性伸缩配置中的 KeyPairName 参数，为您提供了 SSH 秘钥对的方式来登录服务器的能力。在创建伸缩配置时，选择您想要使用的秘钥对名称作为 KeyPairName 参数配置到伸缩配置中。当 ECS 实例被弹性伸缩服务创建出来时，实例会存储此秘钥对的公钥部分，您只需要在本机配置一下秘钥对的私钥部分，便可以使用 SSH 秘钥对的方式快速地登录到您的服务器上去。

在创建伸缩配置，并使用了 KeyPairName 参数时，需要注意以下几点：

-   Windows ECS 实例，忽略该参数。即使传入了 KeyPairName，也不会生效。
-   当传入了 KeyPairName 参数后，Linux ECS 实例的密码登录方式会被初始化成禁止。
-   关于秘钥对的创建，您可以参考 [CreateKeyPair](../../../../cn.zh-CN/API 参考/SSH 密钥对/CreateKeyPair.md#) 接口 。

## RAM 角色名称 { .section}

RAM \(Resource Access Management\) 是阿里云为客户提供的用户身份管理与访问控制服务。使用 RAM，您可以创建、管理用户账号（比如员工、系统或应用程序），并可以控制这些用户账号对您名下资源具有的操作权限。当您的企业存在多用户协同操作资源时，使用 RAM 可以让您避免与其他用户共享云账号密钥，按需为用户分配最小权限，从而降低您的企业信息安全风险。

RAM 支持创建不同的角色，不同的角色具有对不同的云产品的不同的操作权限。ESS 弹性伸缩配置新增了 RamRoleName 参数，您可以通过设置该参数，让您的 ECS 实例来扮演不同的角色，这些实例便拥有了这些角色不同的云产品的操作权限。在给伸缩配置指定RamRoleName 参数时，您需要确保当前的 RamRole 策略中允许您的ECS实例来扮演该角色，否则伸缩配置无法有效地弹出 ECS 实例。

关于 RamRole 的策略信息和创建方法，您可以参考 [CreateRole](../../../../cn.zh-CN/API参考/API 参考（RAM）/角色管理接口/CreateRole.md#) 接口。

## 标签 { .section}

阿里云 ECS 提供标签（Tags）服务，您可以通过给 ECS 实例绑定不同的标签的方式，实现对 ECS 实例的分类管理。

您可以通过查询不同的标签方式，获取符合条件的 ECS 实例列表。同样，您也可以通过查询 ECS 实例的方式，查询出匹配到的标签。ESS 弹性伸缩配置新增了 Tags 参数，您可以通过设置不同的标签对，来对您ESS伸缩服务弹出的机器进行分类管理。每个伸缩配置暂时最多只能支持5对标签，当指定的标签数超过5对，伸缩配置将创建失败。

## 最佳实践 { .section}

为了让您能够更加清晰地理解并准确地使用 ESS 伸缩服务，本章节将结合这些新特性，向您详细地介绍伸缩组和伸缩配置的创建过程，并为这些新参数中的每个参数都设置一个简单的使用场景，来加强您的理解。

## 创建伸缩组 { .section}

1.  创建一个伸缩组。登录ESS控制台，单击控制台右侧 **创建伸缩组**，弹出伸缩组创建对话框。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40616/154227366021296_zh-CN.png)

2.  伸缩组分为经典网络伸缩组、专有网络伸缩组。由于专有网络（VPC）环境下的伸缩配置才能使用实例自定义数据（UserData）参数，因此本文将基于专有网络伸缩组展开介绍。您需要指定伸缩组所在的虚拟交换机，然后点击确定，创建一个专有网络伸缩组。

## 创建伸缩配置 { .section}

1.  创建完伸缩组以后，弹出 创建伸缩配置 对话框。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40616/154227366021297_zh-CN.png)

2.  单击 **创建伸缩配置** 按钮，弹出伸缩配置参数配置界面。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40616/154227366021298_zh-CN.png)


基本的伸缩配置参数这里不作过多介绍，您可以参考 [创建伸缩配置](../../../../cn.zh-CN/API 参考/伸缩配置/创建伸缩配置.md#) 接口来了解每个参数的作用和设置方式。这里将重点介绍 UserData、KeyPairName、RamRoleName、Tags 4个参数的设置。

## UserData 参数设置 { .section}

UserData 支持 Windows 系统和 Linux 操作系统，这里将介绍 UserData 在 Linux 操作系统下，如何通过自定义shell脚本的方式，来实现在ECS实例启动时自动地运行已定义好的脚本。

1.  定义一个shell脚本，来实现在实例首次启动后向 /root/output10.txt 文件写入字符串 `Hello World. The time is now{当前时间}`。在定义shell脚本时，需注意以下3点：

    -   格式：首行必须是 `#!`，如 `#!/bin/sh`。
    -   限制：在 Base64 编码前，脚本内容（包括首行在内）不能超过16 KB。
    -   频率：仅在首次启动实例时执行一次。
    脚本的内容如下：

    ```language-bash
    #!/bin/sh
    echo "Hello World.  The time is now $(date -R)!" | tee /root/output10.txt
    
    ```

    脚本经过 Base64 编码后内容如下：

    ```language-bash
    IyEvYmluL3NoDQplY2hvICJIZWxsbyBXb3JsZC4gIFRoZSB0aW1lIGlzIG5vdyAkKGRhdGUgLVIpISIgfCB0ZWUgL3Jvb3Qvb3V0cHV0MTAudHh0
    
    ```

2.  shell脚本准备好以后，伸缩配置中 **镜像类型** 选择 **公共镜像**，**镜像** 选择Linux类型的系统镜像如 **Ubuntu**，伸缩配置中用户自定义数据填写 Base64 编码以后的脚本数据，并勾选 **输入已采用base64编码** 选项，上述参数设置结果如下图所示：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40616/154227366021299_zh-CN.png)


## KeyPairName参数设置 { .section}

1.  在设置 KeyPairName 参数前，您需要确保伸缩配置所在区域已经存在创建好的秘钥对，如果没有创建好的秘钥对，需访问 秘钥对 列表页新建秘钥对。秘钥对创建界面如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40616/154227366121300_zh-CN.png)

2.  秘钥对创建好以后，系统会返回秘钥的私钥部分，请妥善保管。秘钥的公钥部分由阿里云统一管理。伸缩配置参数中，请选择您想要用来登录实例的秘钥对名称，如下图所示：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40616/154227366121301_zh-CN.png)


## Tags参数设置 { .section}

在配置伸缩配置中实例标签参数时，您可以选用已有的标签，也可以新建标签。

**说明：** 实例标签参数目前只支持 key、value 都不为空的场景。在设置实例标签参数时，最多设置5对标签，超过5对标签伸缩配置将无法创建。伸缩配置中，配置好标签参数以后的效果，如下图所示：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40616/154227366121302_zh-CN.png)

## RamRoleName参数设置 { .section}

1.  RamRoleName 参数目前在 ESS 控制台暂未开放，您可以通过调用 [创建伸缩配置](../../../../cn.zh-CN/API 参考/伸缩配置/创建伸缩配置.md#) API 的方式来使用此参数。因为弹性伸缩服务创建出来的 ECS 实例参数会扮演 RamRoleName 对应的角色.

    **说明：** ESS 伸缩配置中配置该参数时，您需要确保当前的 RamRole策略中允许您的 ECS 实例来扮演该角色。如 AliyunECSImageExportDefaultRole 镜像的导出角色，该角色允许当前用户的所有 ECS 实例来扮演这个角色，角色信息如下：

    ```language-bash
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

    其中 ecs.aliyuncs.com 表示该角色当前用户的所有 ECS 实例来扮演。

2.  配置好伸缩配置以后，单击 **确定** 创建伸缩配置。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40616/154227366121303_zh-CN.png)

3.  单击 **确定** 按钮，启动伸缩配置。

## 验证伸缩活动 { .section}

由于伸缩组创建的时候指定了最小实例数为1，弹性伸缩服务会启动一个伸缩任务，生产1台实例到当前伸缩组，使得当前伸缩组满足最小实例数的限制。

1.  您可以进入伸缩活动列表页，查看当前伸缩组对应的伸缩活动执行详情，如下图所示：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40616/154227366121304_zh-CN.png)

2.  实例通过当前伸缩配置生产出来以后，您需要在本机配置伸缩配中指定的秘钥对的私钥，然后以 SSH Key 的方式来登录实例。不同的操作中，SSH 私钥的配置方式不同，这里以 Mac 系统为例，来介绍如何配置私钥。步骤如下：

    1.  找到 /Users/\{username\}/.ssh/ 目录，如果找不到，需要新建。
    2.  在 /Users/\{username\}/.ssh/ 目录下新建 id\_rsa 文件，将私钥信息拷贝进文件并保存。
    3.  执行 ssh-add 命令将私钥信息配置到系统。
    4.  使用命令 ssh root@\{publicIp\} 登录实例。其中 `publicIp` 代表实例的公网IP，可以通过查看本伸缩组的 ECS 实例列表获取。单击 **实例ID** 进去详情页查看，可以获取到实例的公网Ip，实例的标签等信息。
    SSH登录成功的效果，如下图所示：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40616/154227366121305_zh-CN.png)

3.  查看 /root/output10.txt 文件，校验 UserData 参数的执行结果，如下图所示：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40616/154227366121306_zh-CN.png)

    从上图可以看出伸缩配置中设置的 KeyPairName、UserData 等参数都已生效。

    **说明：** 上述只展示了 UserData 的使用方式，使用的shell脚本比较简单。您可以根据自己的需求，定制您自己的脚本，然后将脚本内容经过 Base64 编码以后配置到伸缩配置中，实例在被弹出来并启动的时候，会执行您的自定义脚本。您可以通过这种方式，来实现应用的自动化扩容、缩容，应用的生命周期管理等功能。


ESS 不仅提供了在业务需求高峰或低谷时自动调节 ECS 实例数量的能力，而且提供了在 ECS 实例上快速安全地部署服务的能力。同时，ESS 还提供了一些管理 ECS 实例的新特性，帮助您更加高效灵活地管理您的 ECS 实例。

合理地使用 ESS 弹性伸缩服务，不仅能够有效地降低您的服务器成本，而且能够有效地降低您的服务管理和运维成本。您可以登录 [弹性伸缩控制台](https://essnew.console.aliyun.com/) 体验ESS的特性，同时也可以参考 [创建伸缩配置](../../../../cn.zh-CN/API 参考/伸缩配置/创建伸缩配置.md#) 接口来使用这些新特性。

