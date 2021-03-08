# 使用阿里云CLI执行滚动升级任务

阿里云CLI是基于阿里云OpenAPI建立的管理工具，您可以通过阿里云CLI调用OpenAPI来管理阿里云产品，灵活性高且易于扩展。本教程介绍如何使用阿里云CLI执行滚动升级任务。

-   已安装阿里云CLI，安装说明请参见[阿里云CLI文档]()中的安装指南部分。
-   已创建伸缩组并添加ECS实例。
-   如果为伸缩组内ECS实例更新镜像，伸缩组的组内实例配置来源必须是伸缩配置。
-   如果为伸缩组内ECS实例安装OOS软件包，必须提前在OOS中创建软件包，具体操作请参见[批量管理我的软件](https://help.aliyun.com/document_detail/169939.html)。

滚动升级是指通过任务形式批量更新ECS实例配置，更多说明请参见[滚动升级](/cn.zh-CN/伸缩组/滚动升级.md)。

## 操作步骤

本教程介绍如何使用阿里云CLI更新伸缩组内ECS实例的镜像、在ECS实例中执行脚本以及为ECS实例安装OOS软件包。步骤如下：

-   [步骤一：创建RAM用户并添加权限](#section_d0w_yd2_kov)
-   [步骤二：配置并验证阿里云CLI](#section_par_u1c_nco)
-   [步骤三：通过阿里云CLI执行滚动升级任务](#section_cxb_gj6_plx)
-   [执行回滚任务：滚动升级异常时的处理](#section_od2_7q0_tlh)

## 步骤一：创建RAM用户并添加权限

1.  登录[RAM控制台](https://ram.console.aliyun.com/)。

2.  创建RAM用户。

    本步骤中以创建名为clitest的RAM用户为例，更多操作说明请参见[创建RAM用户](/cn.zh-CN/用户管理/创建RAM用户.md)。

    1.  在左侧导航栏，单击**人员管理** \> **用户**。

    2.  单击**创建用户**。

    3.  在**创建用户**页面，指定用户配置，然后单击**确定**。

        示例配置如下表所示。

        |配置项|示例配置|
        |---|----|
        |**登录名称**|clitest@sample.com|
        |**显示名称**|clitest|
        |**访问方式**|选中**编程访问**。自动为RAM用户生成访问密钥（AccessKey），支持通过API或其他开发工具访问阿里云。 |

    4.  在**用户信息**页面，单击**下载CSV文件**。

        **说明：** AccessKeySecret只在创建时显示，不提供查询，请妥善保管。如果AccessKey泄露或丢失，则需要创建新的AccessKey。

3.  为RAM用户添加操作资源的权限。

    1.  在左侧导航栏，单击**人员管理** \> **用户**。

    2.  找到已创建的RAM用户clitest，在**操作**列，单击**添加权限**。

    3.  在添加权限页面，选择执行滚动升级任务所需的权限，然后单击**确定**。

        示例配置如下表所示。

        |配置项|示例配置|
        |---|----|
        |**授权范围**|保持默认**云账号全部资源**。|
        |**被授权主体**|保持默认clitest@sample.com。|
        |**选择权限**|选择以下系统权限：        -   AliyunECSFullAccess：操作ECS资源的权限，包括ECS实例等资源。
        -   AliyunESSFullAccess：操作弹性伸缩资源的权限，包括伸缩组等资源。
        -   AliyunOOSFullAccess：操作运维编排资源的权限，包括执行等资源。
        -   AliyunOSSFullAccess：操作对象存储资源的权限，包括bucket等资源。 |


## 步骤二：配置并验证阿里云CLI

更多配置项的说明请参见[阿里云CLI文档]()中的配置阿里云CLI部分。

1.  在您的本地电脑中打开命令行工具。

2.  配置阿里云CLI。

    1.  运行以下命令打开配置文件。

        ```
        aliyun configure
        ```

    2.  按提示输入AccessKeyID、AccessKeySecret等信息。

        ![cli-config](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3192839951/p160873.png)

3.  运行以下命令验证阿里云CLI是否可用。

    ```
    aliyun ecs DescribeRegions
    ```

    该命令用于查询支持的地域信息，返回地域信息表示命令执行成功，示例如下图所示。

    ![cli-example](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3192839951/p160879.png)


## 步骤三：通过阿里云CLI执行滚动升级任务

本步骤提供示例命令，演示更新伸缩组内ECS实例的镜像、在ECS实例中执行脚本以及为ECS实例安装OOS软件包。

1.  输入阿里云CLI命令执行滚动升级任务。

    示例代码中涉及的OOS模板参数说明，请参见[模板参数说明](#section_gju_4ho_zbw)。

    -   镜像更新示例命令如下，实现将伸缩组内ECS实例的镜像更新为Alibaba Cloud Linux 2.1903 LTS 64位。

        ```
        aliyun oos StartExecution --TemplateName ACS-ESS-RollingUpdateByReplaceSystemDiskInScalingGroup --Parameters "{
                \"invokeType\": \"invoke\",
                \"scalingGroupId\": \"asg-bp18p2yfxow2dloq****\",
                \"scalingConfigurationId\": \"asc-bp1bx8mzur534edp****\",
                \"imageId\": \"aliyun_2_1903_x64_20G_alibase_20200529.vhd\",
                \"sourceImageId\": \"centos_7_8_x64_20G_alibase_20200717.vhd\",
                \"OOSAssumeRole\": \"\",
                \"enterProcess\": [
                  \"ScaleIn\",
                  \"ScaleOut\",
                  \"HealthCheck\",
                  \"AlarmNotification\",
                  \"ScheduledAction\"
                ],
                \"exitProcess\":  [
                  \"ScaleIn\",
                  \"ScaleOut\",
                  \"HealthCheck\",
                  \"AlarmNotification\",
                  \"ScheduledAction\"
                ],
                \"batchNumber\": 2,
                \"batchPauseOption\": \"Automatic\"
              }"
        ```

    -   脚本执行示例命令如下，实现在伸缩组内ECS实例中执行Shell命令df -h和ifconfig查看实例的磁盘和网络配置信息。

        ```
        aliyun oos StartExecution --TemplateName ACS-ESS-RollingUpdateByRunCommandInScalingGroup --Parameters "{
                \"invokeType\": \"invoke\",
                \"scalingGroupId\": \"asg-bp18p2yfxow2dloq****\",
                \"commandType\": \"RunShellScript\",
                \"invokeScript\": \"df -h\nifconfig\",
                \"rollbackScript\": \"df -h\nifconfig\",
                \"OOSAssumeRole\": \"\",
                \"exitProcess\": [
                  \"ScaleIn\",
                  \"ScaleOut\",
                  \"HealthCheck\",
                  \"AlarmNotification\",
                  \"ScheduledAction\"
                ],
                \"enterProcess\": [
                  \"ScaleIn\",
                  \"ScaleOut\",
                  \"HealthCheck\",
                  \"AlarmNotification\",
                  \"ScheduledAction\"
                ],
                \"batchNumber\": 2,
                \"batchPauseOption\": \"Automatic\"
              }"
        ```

    -   安装OOS软件包示例命令如下，实现为伸缩组内的ECS实例统一安装OOS中已创建的wordpress软件包。

        ```
        aliyun oos StartExecution --TemplateName ACS-ESS-RollingUpdateByConfigureOOSPackage --Parameters "{
                \"invokeType\": \"invoke\",
                \"scalingGroupId\": \"asg-bp18p2yfxow2dloq****\",
                \"packageName\": \"wordpress\",
                \"packageVersion\": \"v4\",
                \"action\": \"install\",
                \"OOSAssumeRole\": \"\",
                \"enterProcess\": [
                  \"ScaleIn\",
                  \"ScaleOut\",
                  \"HealthCheck\",
                  \"AlarmNotification\",
                  \"ScheduledAction\"
                ],
                \"exitProcess\": [
                  \"ScaleIn\",
                  \"ScaleOut\",
                  \"HealthCheck\",
                  \"AlarmNotification\",
                  \"ScheduledAction\"
                ],
                \"batchNumber\": 2,
                \"batchPauseOption\": \"Automatic\"
              }"
        ```

2.  查看执行详情。

    执行滚动升级任务的CLI命令时，会自动在OOS中创建执行。您可以通过返回的执行ID查看执行的详情，包括执行结果、输出等信息。下面以查看脚本执行的输出为例，介绍如何获取执行ID并查看执行详情。

    1.  在命令的返回信息中找到滚动升级任务的执行ID。

        执行ID示例如下图所示。

        ![exec-id](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3192839951/p161172.png)

    2.  运行以下阿里云CLI命令查看执行详情。

        ```
        aliyun oos ListExecutions --ExecutionId exec-40e2e17ef7e04****
        ```

        执行详情示例如下图所示。

        ![exec-outputs](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3192839951/p161174.png)


## 执行回滚任务：滚动升级异常时的处理

如果滚动升级过程中出现异常，或者滚动升级后又需要使用历史配置，您可以执行回滚任务为伸缩组内ECS实例恢复配置。本步骤提供示例命令，演示如何回滚已经执行的滚动升级任务。

1.  在命令的返回信息中找到滚动升级任务的执行ID。

    执行ID示例如下图所示。

    ![exec-id](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3192839951/p161172.png)

2.  输入阿里云CLI命令执行回滚任务。

    示例代码中涉及的OOS模板参数说明，请参见[模板参数说明](#section_gju_4ho_zbw)。

    **说明：** 执行回滚任务时，OOS会根据滚动升级任务自动进行过滤待回滚的ECS实例、暂停和恢复伸缩组流程等操作，因此您可以跳过指定部分参数。

    -   回滚镜像更新示例命令如下，实现将ECS实例的镜像回滚为CentOS 7.8 64位。

        ```
        aliyun oos StartExecution --TemplateName ACS-ESS-RollingUpdateByReplaceSystemDiskInScalingGroup --Parameters "{
                \"invokeType\": \"rollback\",
                \"scalingGroupId\": \"asg-bp18p2yfxow2dloq****\",
                \"scalingConfigurationId\": \"asc-bp1bx8mzur534edp****\",
                \"sourceImageId\": \"centos_7_8_x64_20G_alibase_20200717.vhd\",
                \"sourceExecutionId\": \"exec-83dba59be77d430****\",
                \"OOSAssumeRole\": \"\",
                \"batchNumber\": 2,
                \"batchPauseOption\": \"Automatic\"
              }"
        ```

    -   回滚脚本执行示例命令如下，实现在ECS实例中执行回滚用的脚本。此处仍然以Shell命令df -h和ifconfig为例，您可以按需要更换脚本。

        ```
        aliyun oos StartExecution --TemplateName ACS-ESS-RollingUpdateByRunCommandInScalingGroup --Parameters "{
                \"invokeType\": \"rollback\",
                \"commandType\": \"RunShellScript\",
                \"rollbackScript\": \"df -h\nifconfig\",
                \"scalingGroupId\": \"asg-bp18p2yfxow2dloq****\",
                \"sourceExecutionId\": \"exec-40e2e17ef7e046****\",
                \"OOSAssumeRole\": \"\",
                \"batchNumber\": 2,
                \"batchPauseOption\": \"Automatic\"
              }"
        ```

    -   回滚安装OOS软件包示例命令如下，实现为ECS实例统一安装OOS中已创建的wordpress软件包历史版本。

        ```
        aliyun oos StartExecution --TemplateName ACS-ESS-RollingUpdateByConfigureOOSPackage --Parameters "{
                \"invokeType\": \"rollback\",
                \"scalingGroupId\": \"asg-bp18p2yfxow2dloq****\",
                \"packageVersion\": \"v3\",
                \"packageName\": \"wordpress\",
                \"sourceExecutionId\": \"exec-f4e61f2f21fe490****\",
                \"OOSAssumeRole\": \"\",
                \"batchNumber\": 2,
                \"batchPauseOption\": \"Automatic\"
              }"
        ```

3.  查看执行详情。

    执行回滚任务的CLI命令时，同样会自动在OOS中创建执行。您同样可以通过步骤三中的方法查看执行的详情，包括执行结果、输出等信息。


## 模板参数说明

本节列出示例中使用的公共模板的参数。

|参数|说明|
|--|--|
|invokeType|任务类型。取值范围：-   invoke：滚动升级任务。
-   rollback：回滚任务。 |
|scalingGroupId|待执行任务的伸缩组的ID。|
|scalingConfigurationId|伸缩组生效中的伸缩配置的ID。|
|imageId|替换当前镜像时使用的镜像的ID。|
|sourceImageId|回滚操作时使用的镜像的ID。|
|OOSAssumeRole|执行任务时使用的RAM角色，默认为OOSServiceRole。|
|enterProcess|开始执行任务时暂停的伸缩组流程。|
|exitProcess|结束任务时需要恢复的伸缩组流程。|
|batchNumber|执行任务时，将伸缩组内ECS实例分成几个批次，每批次至少包括一台ECS实例。|
|batchPauseOption|执行任务时的暂停设置。取值范围：-   Automatic：不暂停，一次性执行完成。
-   FirstBatchPause：第一批次执行完成后，暂停执行任务。
-   EveryBatchPause：每批次执行完成后，都暂停执行任务。 |
|sourceExecutionId|执行回滚任务时，源滚动升级任务的执行ID。|

**说明：** 您也可以在OOS控制台查看更多参数说明，以华东1（杭州）地域为例，请参见[ACS-ESS-RollingUpdateByReplaceSystemDiskInScalingGroup](https://oos.console.aliyun.com/cn-hangzhou/template/public/detail/ACS-ESS-RollingUpdateByReplaceSystemDiskInScalingGroup)。

|参数|说明|
|--|--|
|invokeType|任务类型。取值范围：-   invoke：滚动升级任务。
-   rollback：回滚任务。 |
|scalingGroupId|待执行任务的伸缩组的ID。|
|commandType|待执行的脚本类型，取值RunShellScript代表Shell脚本。|
|invokeScript|执行滚动升级任务时，在ECS实例中执行的脚本。|
|rollbackScript|执行回滚任务时，在ECS实例中执行的脚本。|
|OOSAssumeRole|执行任务时使用的RAM角色，默认为OOSServiceRole。|
|enterProcess|开始执行任务时暂停的伸缩组流程。|
|exitProcess|结束任务时需要恢复的伸缩组流程。|
|batchNumber|执行任务时，将伸缩组内ECS实例分成几个批次，每批次至少包括一台ECS实例。|
|batchPauseOption|执行任务时的暂停设置。取值范围：-   Automatic：不暂停，一次性执行完成。
-   FirstBatchPause：第一批次执行完成后，暂停执行任务。
-   EveryBatchPause：每批次执行完成后，都暂停执行任务。 |
|sourceExecutionId|执行回滚任务时，源滚动升级任务的执行ID。|

**说明：** 您也可以在OOS控制台查看更多参数说明，以华东1（杭州）地域为例，请参见[ACS-ESS-RollingUpdateByRunCommandInScalingGroup](https://oos.console.aliyun.com/cn-hangzhou/template/public/detail/ACS-ESS-RollingUpdateByRunCommandInScalingGroup)。

|参数|说明|
|--|--|
|invokeType|任务类型。取值范围：-   invoke：滚动升级任务。
-   rollback：回滚任务。 |
|scalingGroupId|待执行任务的伸缩组的ID。|
|packageName|软件包的名称。|
|packageVersion|软件包的版本。|
|action|配置软件包的方式。取值范围：-   install：安装软件包。
-   uninstall：卸载软件包。 |
|OOSAssumeRole|执行任务时使用的RAM角色，默认为OOSServiceRole。|
|enterProcess|开始执行任务时暂停的伸缩组流程。|
|exitProcess|结束任务时需要恢复的伸缩组流程。|
|batchNumber|执行任务时，将伸缩组内ECS实例分成几个批次，每批次至少包括一台ECS实例。|
|batchPauseOption|执行任务时的暂停设置。取值范围：-   Automatic：不暂停，一次性执行完成。
-   FirstBatchPause：第一批次执行完成后，暂停执行任务。
-   EveryBatchPause：每批次执行完成后，都暂停执行任务。 |
|sourceExecutionId|执行回滚任务时，源滚动升级任务的执行ID。|

**说明：** 您也可以在OOS控制台查看更多参数说明，以华东1（杭州）地域为例，请参见[ACS-ESS-RollingUpdateByConfigureOOSPackage](https://oos.console.aliyun.com/cn-hangzhou/template/public/detail/ACS-ESS-RollingUpdateByConfigureOOSPackage)。

