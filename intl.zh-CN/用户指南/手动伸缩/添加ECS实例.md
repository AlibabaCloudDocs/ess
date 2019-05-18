# 添加ECS实例 {#task_zn2_2nx_rfb .task}

本文介绍如何手动向伸缩组添加一个ECS实例。

手动添加ECS实例前，请确保待添加的ECS实例满足以下条件：

-   实例必须与伸缩组处于同一个地域。
-   实例不能已加入到其它伸缩组中。
-   实例的状态必须是**运行中**。
-   实例的网络类型可以为经典网络或专有网络，但有以下限制：
    -   当伸缩组的网络类型为经典网络时，只能添加网络类型为经典网络的ECS实例。
    -   当伸缩组的网络类型为专有网络时，只能添加同一专有网络下的ECS实例。

同时，请确保伸缩组满足以下条件：

-   伸缩组的状态必须是**启用**。
-   伸缩组内不能存在执行中的伸缩活动。

手动添加ECS实例的配置与当前伸缩配置没有关联，并且手动添加ECS实例时可以绕过[冷却时间](intl.zh-CN/用户指南/使用须知/冷却时间.md#)

弹性伸缩服务尽力保证足额弹出待添加的ECS实例，但是，如果出现云服务器库存不足、待添加的ECS实例数超过伸缩组上限等问题，ECS实例会无法足额弹出。这种情况下，请您检查伸缩组相关配置定位问题。如果无法解决问题，请[提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex)。

1.  登录[弹性伸缩控制台](https://essnew.console.aliyun.com/)。 
2.  在伸缩组管理页面，单击指定伸缩组**操作**列下的**管理**。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40594/155815435821748_zh-CN.png)

3.  前往ECS实例列表页面，单击**添加已有实例**。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40594/155815435821749_zh-CN.png)

4.  从左侧列表中选择可用的ECS实例，单击**\>**添加到伸缩组，然后单击**确定**。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40594/155815435821750_zh-CN.png)

5.  前往手动添加页面查看结果。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40594/155815435821751_zh-CN.png)

    **说明：** 如果页面没有自动刷新，请单击页面右上角的**刷新**手动刷新。


