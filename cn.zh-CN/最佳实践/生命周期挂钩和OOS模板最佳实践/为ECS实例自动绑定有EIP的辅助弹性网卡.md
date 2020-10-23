---
keyword: [生命周期挂钩, OOS模板, 弹性网卡, 弹性公网IP]
---

# 为ECS实例自动绑定有EIP的辅助弹性网卡

本教程介绍如何使用弹性伸缩生命周期挂钩挂起ECS实例，并结合运维编排服务OOS的模板，实现为ECS实例自动绑定有弹性公网IP（EIP）的辅助弹性网卡。

-   使用本教程进行操作前，请确保您已经注册了阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。
-   已创建伸缩组，且伸缩组处于启用状态。
-   已为OOS服务创建RAM角色，具体操作请参见[为OOS服务设置RAM权限](https://help.aliyun.com/document_detail/120810.html)。

    **说明：** 本教程中使用默认的RAM角色OOSServiceRole，您也可以使用其他自定义的RAM角色，但需要保证RAM角色拥有执行OOS模板所需的权限。


弹性网卡是一种可以绑定到专有网络VPC类型ECS实例上的虚拟网卡，用于实现高可用集群搭建、低成本故障转移和精细化的网络管理。弹性网卡分为主网卡和辅助网卡：主网卡随ECS实例一起创建，不支持从ECS实例上解绑；辅助网卡可以单独创建，支持自由绑定到ECS实例上或从ECS实例上解绑。更多说明，请参见[弹性网卡概述](/cn.zh-CN/网络/弹性网卡/弹性网卡概述.md)。

EIP是可以独立购买和持有的公网IP地址资源，用于长期持有某个公网IP地址。您可以根据业务需要将EIP绑定到ECS实例、弹性网卡等资源，或者从这些资源解绑。更多说明，请参见[弹性公网IP](/cn.zh-CN/网络/实例IP地址介绍/弹性公网IP.md)。

目前创建伸缩配置时暂不支持指定辅助弹性网卡和EIP，但您可以通过生命周期挂钩和OOS模板为ECS实例自动绑定有EIP的辅助弹性网卡，相比创建ECS实例后再手动绑定，效率更高。

**说明：** 如果ECS实例使用的镜像为Window Server 2008 R2及更高版本、CentOS 7.3 64位、CentOS6.8 64位，绑定弹性网卡后无需再手动配置。使用其它镜像时则需要手动配置，使弹性网卡能被ECS实例识别，具体操作请参见[配置弹性网卡](/cn.zh-CN/网络/弹性网卡/配置弹性网卡.md)。

## 操作步骤

本教程以OOS公共模板ACS-ESS-LifeCycleCreateNetworkInterfaceAndEipAndAttachToInstance为例，实现在扩容时为ECS实例绑定一张辅助弹性网卡，并为辅助弹性网卡分配一个EIP。步骤如下：

-   [步骤一：对RAM角色授予OOS服务权限](#section_onb_kyb_1xg)
-   [步骤二：为扩容活动创建生命周期挂钩并触发扩容](#section_ixt_52h_nq5)
-   [（可选）步骤三：查看OOS执行情况](#section_dvu_jn8_f76)

## 步骤一：对RAM角色授予OOS服务权限

您需要拥有OOS的执行权限才能执行OOS的模板。执行ACS-ESS-LifeCycleCreateNetworkInterfaceAndEipAndAttachToInstance中定义的运维操作时涉及ECS、弹性伸缩、EIP的资源。

1.  登录[RAM控制台](https://ram.console.aliyun.com/)。

2.  在左侧导航栏，单击**RAM角色管理**。

3.  找到OOSServiceRole，在**操作**区域，单击**添加权限**。

    为OOS服务扮演的RAM角色OOSServiceRole添加权限即可完成授权。

4.  指定权限配置，然后单击**确定**。

    本教程中使用的配置如下表所示，未提及的配置保持默认即可。

    |配置项|说明|
    |---|--|
    |**授权范围**|选择**云帐号全部资源**。|
    |**选择权限**|添加系统策略AliyunECSFullAccess、AliyunESSFullAccess和AliyunEIPFullAccess。|


## 步骤二：为扩容活动创建生命周期挂钩并触发扩容

1.  登录[弹性伸缩控制台](https://essnew.console.aliyun.com/)。

2.  在左侧导航栏中，单击**伸缩组管理**。

3.  在顶部菜单栏处，选择地域。

4.  找到待操作的伸缩组，选择一种方式打开伸缩组详情页面。

    -   在**伸缩组名称/ID**区域，单击伸缩组ID。
    -   在**操作**区域，单击**查看详情**。
5.  为扩容活动创建生命周期挂钩。

    1.  在页面上方，单击**生命周期挂钩**页签。

    2.  单击**创建生命周期挂钩**。

    3.  指定生命周期挂钩配置，然后单击**确认**。

        本教程中使用的配置如下表所示，未提及的配置保持默认即可。

        |配置项|说明|
        |---|--|
        |**名称**|输入ESSHookForAttachNicWithEip。|
        |**适用的伸缩活动类型**|选择**弹性扩张活动**。|
        |**超时时间**|输入适当的超时时间，例如300秒。**说明：** 超时时间即用于执行自定义操作的时间，若超时时间过短，可能导致自定义操作失败，请评估自定义操作耗时并设置适当的超时时间。 |
        |**执行策略**|选择**继续**。|
        |**通知方式**|模板配置如下：        -   通知方式：选择**OOS模板**。
        -   OOS模板类型：选择**公共模板**。
        -   公共模板：选择ACS-ESS-LifeCycleCreateNetworkInterfaceAndEipAndAttachToInstance。
ACS-ESS-LifeCycleCreateNetworkInterfaceAndEipAndAttachToInstance的执行参数配置示例如下：

        -   **internetChargeType**：PayByBandwidth为按带宽，PayByTraffic为按流量。本教程中以PayByBandwidth为例。
        -   **bandwidth**：本教程中以5为例，代表使用EIP时带宽峰值为5 Mbit/s。
        -   **执行使用到的权限的来源**：选择OOSServiceRole即可。步骤一中已为RAM角色OOSServiceRole添加操作ECS、弹性伸缩、EIP资源的权限，OOS服务扮演该RAM角色即可拥有相关权限。 |

6.  触发扩容。

    本教程中以手动执行伸缩规则为例，您也可以通过定时任务、报警任务等方式触发扩容。

    **说明：** 手动执行伸缩规则触发扩缩容时，生命周期挂钩会生效，但手动添加或移出已有ECS实例时，生命周期挂钩不会生效。

    1.  在页面上方，单击**伸缩规则**页签。

    2.  单击**创建伸缩规则**。

    3.  设置伸缩规则的属性，然后单击**确认**。

        本教程中使用的配置如下表所示，未提及的配置保持默认即可。

        |配置项|说明|
        |---|--|
        |**规则名称**|输入Add1。|
        |**伸缩规则类型**|选择**简单规则**。|
        |**执行的操作**|设置为增加1台。|

    4.  找到新建的伸缩规则Add1，在**操作**区域，单击**执行**。

    5.  单击**确定**。

    执行伸缩规则后自动创建1台ECS实例，由于伸缩组内已创建生命周期挂钩ESSHookForAttachNicWithEip，ECS实例会被挂起，同时自动通知OOS服务执行ACS-ESS-LifeCycleCreateNetworkInterfaceAndEipAndAttachToInstance中定义的运维操作。

    如果伸缩活动的状态为失败，且出现以下报错，请前往OOS控制台查看运维任务执行情况，具体步骤请参见[（可选）步骤三：查看OOS执行情况](#section_dvu_jn8_f76)。

    ![instance-rollback](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2272372061/p172157.png)

7.  查看自动创建的ECS实例是否符合预期。

    1.  在页面上方，单击**实例列表**页签。

    2.  找到自动创建的ECS实例，在**云服务器ID/名称**区域，单击实例ID。

    3.  在左侧导航栏，单击**本实例弹性网卡**。

        如下图所示，ECS实例自动绑定了一张辅助弹性网卡，并且为辅助弹性网卡分配了EIP，符合使用公共模板ACS-ESS-LifeCycleCreateNetworkInterfaceAndEipAndAttachToInstance的预期。

        ![自动绑定的辅助ENI](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9394129951/p133063.png)

        如果成功创建了ECS实例，但ECS实例并没有自动绑定辅助弹性网卡和EIP，请前往OOS控制台查看运维任务执行情况，具体步骤请参见[（可选）步骤三：查看OOS执行情况](#section_dvu_jn8_f76)。


## （可选）步骤三：查看OOS执行情况

1.  登录[OOS管理控制台](https://oos.console.aliyun.com/)。

2.  在左侧导航栏，单击**执行管理**。

3.  按开始时间找到执行，然后在**操作**区域，单击**详情**。

4.  在页面上方，单击**高级视图**，然后在**执行结果**页签中查看执行状态。

    -   如果执行成功，显示相关的结果输出等信息。

        ![查看执行情况](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0163562061/p132765.png)

    -   如果执行失败，显示相关的报错等信息。

        ![OOS执行结果](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0163562061/p133032.png)


## 常见问题

如果运维任务执行失败，请根据执行结果中的报错信息排查原因。常见的报错信息及解决方案如下：

-   报错信息：Forbidden.Unauthorized message: A required authorization for the specified action is not supplied.

    解决方案：请检查是否为RAM角色OOSServiceRole添加了相应的权限，例如步骤一中的示例权限。您需要为RAM角色添加操作权限，确保OOS服务能够操作OOS模版中涉及的资源。

-   报错信息：Forbidden.RAM message: User not authorized to operate on the specified resource, or this API doesn't support RAM.

    解决方案：请检查是否为RAM角色OOSServiceRole添加了相应的权限，例如步骤一中的示例权限。您需要为RAM角色添加操作权限，确保OOS服务能够操作OOS模版中涉及的资源。

-   报错信息：LifecycleHookIdAndLifecycleActionToken.Invalid message: The specified lifecycleActionToken and lifecycleActionId you provided does not match any in process lifecycle action.

    解决方案：请评估生命周期挂钩的超时时间，确保在超时时间内可以执行完OOS模板中定义的运维任务。


