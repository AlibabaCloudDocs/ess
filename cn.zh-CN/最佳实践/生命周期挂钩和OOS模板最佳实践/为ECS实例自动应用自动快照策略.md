---
keyword: [弹性伸缩, 生命周期挂钩, 自动快照策略, OOS]
---

# 为ECS实例自动应用自动快照策略

本教程介绍如何使用弹性伸缩生命周期挂钩挂起ECS实例，并结合运维编排服务OOS的模板，实现为ECS实例自动应用自动快照策略。

-   使用本教程进行操作前，请确保您已经注册了阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。
-   已创建伸缩组，且伸缩组处于启用状态。
-   已创建自动快照策略。
-   已为OOS服务创建RAM角色，具体操作请参见[为OOS服务设置RAM权限](https://help.aliyun.com/document_detail/120810.html)。

    **说明：** 本教程中使用默认的RAM角色OOSServiceRole，您也可以使用其他自定义的RAM角色，但需要保证RAM角色拥有执行OOS模板所需的权限。


自动快照策略可以为ECS实例定期创建快照，提高数据安全和操作容错率。目前创建伸缩配置时暂时不支持关联自动快照策略，但您可以通过生命周期挂钩和OOS模板为ECS实例自动应用自动快照策略，相比创建ECS实例后再手动应用自动快照策略，效率更高。

## 操作步骤

本教程以OOS公共模板ACS-ESS-LifeCycleApplyAutoSnapshotPolicy为例，实现在扩容时自动为ECS实例应用自动快照策略。步骤如下：

-   [步骤一：对RAM角色授予OOS服务权限](#section_r5u_0u7_sg7)
-   [步骤二：为扩容活动创建生命周期挂钩并触发扩容](#section_r15_be6_7lv)
-   [（可选）步骤三：查看OOS执行情况](#section_p8q_obi_gcr)

## 步骤一：对RAM角色授予OOS服务权限

您需要拥有OOS的执行权限才能执行OOS的模板。执行ACS-ESS-LifeCycleApplyAutoSnapshotPolicy中定义的运维操作时涉及云服务器ECS、弹性伸缩的资源。

1.  登录[RAM控制台](https://ram.console.aliyun.com/)。

2.  创建权限策略。

    1.  在左侧导航栏，单击**权限管理** \> **权限策略管理**。

    2.  在页面左上角，单击**创建权限策略**。

    3.  在**新建自定义权限策略**页面，指定权限配置，然后单击**确定**。

        本教程中使用的配置如下表所示，未提及的配置保持默认即可。

        |配置项|说明|
        |---|--|
        |**策略名称**|填写ESSHookPolicyForApplyAutoSnapshotPolicy。|
        |**配置模式**|选择**脚本配置**。|
        |**策略内容**|输入以下内容：        ```
{
    "Version": "1",
    "Statement": [
        {
            "Action": [
                "ecs:DescribeDisks",
                "ecs:ApplyAutoSnapshotPolicy",
                "ecs:DescribeInstances"
            ],
            "Resource": "*",
            "Effect": "Allow"
        },
        {
            "Action": [
                "ess:CompleteLifecycleAction"
            ],
            "Resource": "*",
            "Effect": "Allow"
        }
    ]
}
        ``` |

3.  为OOSServiceRole授予权限策略。

    1.  在左侧导航栏，单击**RAM角色管理**。

    2.  找到OOSServiceRole，在**操作**区域，单击**添加权限**。

        为OOS服务扮演的RAM角色OOSServiceRole添加权限即可完成授权。

    3.  在**添加权限**页面，指定权限配置，然后单击**确定**。

        本教程中使用的配置如下表所示，未提及的配置保持默认即可。

        |配置项|说明|
        |---|--|
        |**授权范围**|选择**云帐号全部资源**。|
        |**选择权限**|添加自定义策略ESSHookPolicyForApplyAutoSnapshotPolicy。|


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
        |**名称**|输入ESSHookForApplyAutoSnapshotPolicy。|
        |**适用的伸缩活动类型**|选择**弹性扩张活动**。|
        |**超时时间**|输入适当的超时时间，例如300秒。**说明：** 超时时间即用于执行自定义操作的时间，若超时时间过短，可能导致自定义操作失败，请评估自定义操作耗时并设置适当的超时时间。 |
        |**执行策略**|选择**继续**。|
        |**通知方式**|模板配置如下：        -   通知方式：选择**OOS模板**。
        -   OOS模板类型：选择**公共模板**。
        -   公共模板：选择ACS-ESS-LifeCycleApplyAutoSnapshotPolicy。
ACS-ESS-LifeCycleApplyAutoSnapshotPolicy的执行参数配置如下：

        -   **自动快照策略ID**：输入自动快照策略的ID。
        -   **执行使用到的权限的来源**：选择OOSServiceRole，步骤一中已为RAM角色OOSServiceRole添加操作ECS、弹性伸缩资源的权限，OOS服务扮演该RAM角色即可拥有相关权限。 |

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

    4.  在**伸缩规则**页面，找到新建的伸缩规则Add1，在**操作**区域，单击**执行**。

    5.  单击**确定**。

    执行伸缩规则后自动创建1台ECS实例，由于伸缩组内已创建生命周期挂钩ESSHookForApplyAutoSnapshotPolicy，ECS实例会被挂起，同时自动通知OOS服务执行ACS-ESS-LifeCycleApplyAutoSnapshotPolicy中定义的运维操作。

7.  查看自动创建的ECS实例是否符合预期。

    1.  在页面上方，单击**实例列表**页签。

    2.  找到自动创建的ECS实例，在**云服务器ID/名称**区域，单击实例ID。

    3.  在左侧导航栏中，单击**本实例云盘**。

    4.  找到云盘，在**操作**区域，单击**设置自动快照策略**。

        如下图所示，云盘已打开自动快照策略开关，并应用了步骤二中创建生命周期挂钩时设置的自动快照策略，符合使用公共模板ACS-ESS-LifeCycleApplyAutoSnapshotPolicy的预期。

        ![view-autosnapshotpolicy](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7261659951/p142246.png)

        如果成功创建了ECS实例，但ECS实例并没有自动应用自动快照策略，请前往OOS控制台查看运维任务执行情况，具体步骤请参见[（可选）步骤三：查看OOS执行情况](#section_p8q_obi_gcr)。


## （可选）步骤三：查看OOS执行情况

1.  登录[OOS管理控制台](https://oos.console.aliyun.com/)。

2.  在左侧导航栏，单击**执行管理**。

3.  按开始时间找到执行，然后在**操作**区域，单击**详情**。

4.  单击**高级视图**。

    **执行结果**页签中显示执行状态。

    ![success](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7261659951/p142247.png)

    如果执行失败，**执行结果**页签中也会显示相关的报错信息。

    ![failed](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7261659951/p142249.png)


## 常见问题

如果运维任务执行失败，请根据执行结果中的报错信息排查原因。常见的报错信息及解决方案如下：

-   报错信息：Forbidden.Unauthorized message: A required authorization for the specified action is not supplied.

    解决方案：请检查是否为RAM角色OOSServiceRole添加了相应的权限，例如步骤一中的示例权限。您需要为RAM角色添加操作权限，确保OOS服务能够操作OOS模版中涉及的资源。

-   报错信息：Forbidden.RAM message: User not authorized to operate on the specified resource, or this API doesn't support RAM.

    解决方案：请检查是否为RAM角色OOSServiceRole添加了相应的权限，例如步骤一中的示例权限。您需要为RAM角色添加操作权限，确保OOS服务能够操作OOS模版中涉及的资源。

-   报错信息：LifecycleHookIdAndLifecycleActionToken.Invalid message: The specified lifecycleActionToken and lifecycleActionId you provided does not match any in process lifecycle action.

    解决方案：请评估生命周期挂钩的超时时间，确保在超时时间内可以执行完OOS模板中定义的运维任务。


