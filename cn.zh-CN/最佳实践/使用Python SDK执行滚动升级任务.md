# 使用Python SDK执行滚动升级任务

通过阿里云Python SDK，您不用复杂编程即可访问阿里云服务。本教程以运行Linux系统的电脑为例，介绍如何使用阿里云Python SDK调用运维编排服务OOS的API执行滚动升级任务。

-   已创建伸缩组并添加ECS实例。
-   已在本地电脑中安装Python。
-   已创建RAM用户并获取AccessKey。

滚动升级是指通过任务形式批量更新ECS实例配置。通过滚动升级，您可以为伸缩组内处于服务中状态的ECS实例批量更新镜像、执行脚本或者安装OOS软件包。

## 操作步骤

在本地电脑中使用Python SDK为ECS实例执行脚本的步骤如下：

-   [步骤一：安装阿里云Python SDK](#section_2s7_41j_w30)
-   [步骤二：执行滚动升级任务](#section_ogk_ybh_2p7)
-   [执行回滚任务：滚动升级异常时的处理](#section_3n9_swu_j8p)

## 步骤一：安装阿里云Python SDK

1.  查看Python版本。

    ```
    python --version
    ```

    返回Python版本表明已安装Python，示例如下图所示。

    ![python-version](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3202479951/p165119.png)

2.  安装SDK核心库。

    ```
    pip install aliyun-python-sdk-core
    ```

3.  安装运维编排服务OOS的SDK。

    ```
    pip install aliyun-python-sdk-oos
    ```


## 步骤二：执行滚动升级任务

本步骤提供示例代码，演示在ECS实例中执行脚本。

1.  创建Python脚本并输入执行滚动升级任务的代码。

    示例代码中涉及的OOS模板参数说明，请参见[模板参数说明](#section_j3p_cao_xwp)。示例代码如下：

    ```
    # -*- coding: UTF-8 -*-
    
    from aliyunsdkcore.client import AcsClient
    from aliyunsdkcore.acs_exception.exceptions import ClientException
    from aliyunsdkcore.acs_exception.exceptions import ServerException
    from aliyunsdkoos.request.v20190601 import StartExecutionRequest
    import json
    
    # 创建AcsClient实例
    client = AcsClient('<accessKeyId>', '<accessSecret>', 'cn-hangzhou')
    
    # 创建request，并设置JSON数据格式
    request = StartExecutionRequest.StartExecutionRequest()
    request.set_accept_format('json')
    
    # 模板名称根据所选升级方式替换
    request.set_TemplateName("ACS-ESS-RollingUpdateByRunCommandInScalingGroup")
    
    # 参数根据所选模板替换
    parameters = {"invokeType": "invoke",
                  "scalingGroupId": "asg-bp18p2yfxow2dloq****",
                  "commandType": "RunShellScript",
                  "invokeScript": "df -h\nifconfig",
                  "rollbackScript": "df -h\nifconfig",
                  "OOSAssumeRole": "",
                  "exitProcess": [
                      "ScaleIn",
                      "ScaleOut",
                      "HealthCheck",
                      "AlarmNotification",
                      "ScheduledAction"
                    ],
                  "enterProcess": [
                      "ScaleIn",
                      "ScaleOut",
                      "HealthCheck",
                      "AlarmNotification",
                      "ScheduledAction"
                    ],
                  "batchNumber": 2,
                  "batchPauseOption": "Automatic"}
    
    request.set_Parameters(json.dumps(parameters))
    
    # 发起API请求并显示返回值
    response = client.do_action_with_exception(request)
    print(response)
    ```

2.  运行Python脚本并查看返回信息。

    您可以在命令的返回信息中找到滚动升级任务的执行ID等信息，示例如下图所示。

    **说明：** 执行回滚任务时需要填入源滚动升级任务的执行ID。

    ![rollingupdate-py](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/4202479951/p165127.png)


## 执行回滚任务：滚动升级异常时的处理

如果滚动升级过程中出现异常，或者滚动升级后又需要使用历史配置，您可以执行回滚任务为伸缩组内ECS实例恢复配置。本步骤提供示例代码，演示如何回滚已经执行的滚动升级任务。

1.  创建Python脚本并输入执行回滚任务的代码。

    示例代码中涉及的OOS模板参数说明，请参见[模板参数说明](#section_j3p_cao_xwp)。示例代码如下：

    ```
    # -*- coding: UTF-8 -*-
    
    from aliyunsdkcore.client import AcsClient
    from aliyunsdkcore.acs_exception.exceptions import ClientException
    from aliyunsdkcore.acs_exception.exceptions import ServerException
    from aliyunsdkoos.request.v20190601 import StartExecutionRequest
    import json
    
    # 创建AcsClient实例
    client = AcsClient('<accessKeyId>', '<accessSecret>', 'cn-hangzhou')
    
    # 创建request，并设置JSON数据格式
    request = StartExecutionRequest.StartExecutionRequest()
    request.set_accept_format('json')
    
    # 模板名称根据所选升级方式替换
    request.set_TemplateName("ACS-ESS-RollingUpdateByRunCommandInScalingGroup")
    
    # 回滚操作对应的参数
    parameters = {"invokeType": "rollback",
                  "scalingGroupId": "asg-bp18p2yfxow2dlo****",
                  "commandType": "RunShellScript",
                  "rollbackScript": "df -h\nifconfig",
                  "OOSAssumeRole": "",
                  "sourceExecutionId": "exec-8fe4a73e9ffd423****",
                  "batchNumber": 2,
                  "batchPauseOption": "Automatic"}
    
    request.set_Parameters(json.dumps(parameters))
    
    # 发起API请求并显示返回值
    response = client.do_action_with_exception(request)
    print(response)
    ```

2.  运行Python脚本并查看返回信息。

    示例如下图所示。

    ![rollingupdate-rollback-py](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3202479951/p165129.png)


## 模板参数说明

本教程中使用了公共模板ACS-ESS-RollingUpdateByRunCommandInScalingGroup，参数说明如下表所示。

|参数|说明|
|--|--|
|invokeType|任务类型。取值范围：-   invoke：滚动升级任务。
-   rollback：回滚任务。 |
|scalingGroupId|待执行任务的伸缩组。|
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

**相关文档**  


[使用阿里云CLI执行滚动升级任务](/cn.zh-CN/最佳实践/使用阿里云CLI执行滚动升级任务.md)

