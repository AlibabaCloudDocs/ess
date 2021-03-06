# 查询ECS实例列表

本章节介绍如何查询已添加至伸缩组的ECS实例。

1.  登录[弹性伸缩控制台](https://essnew.console.aliyun.com/)。

2.  在顶部菜单栏处，选择地域。

3.  找到待操作的伸缩组，选择一种方式打开伸缩组详情页面。

    -   在**伸缩组名称/ID**区域，单击伸缩组ID。
    -   在**操作**区域，单击**查看详情**。
4.  在页面上方，单击**实例列表**。

5.  查看ECS实例。

    -   **自动创建**页中列出了伸缩组自动创建的ECS实例，您可以设置ECS实例的状态、将ECS实例移出伸缩组或者释放ECS实例。如果自动创建的实例被判定为不健康，会被移出伸缩组并释放。
    -   **手动创建**页中列出了您手动添加的ECS实例，您可以设置ECS实例的状态或者将ECS实例手动移出伸缩组。如果手动添加的实例没有处于**运行中**状态，即被判定为不健康而自动移出伸缩组。ECS实例移出伸缩组时是否被释放由托管状态决定：
        -   实例生命周期未托管给伸缩组：手动添加的ECS实例仅移出伸缩组，不会被释放。
        -   实例生命周期托管给伸缩组：手动添加的ECS实例会被移出伸缩组并释放。

**相关文档**  


[实例转为备用状态](/cn.zh-CN/实例管理/ECS实例/实例转为备用状态.md)

[实例转为保护状态](/cn.zh-CN/实例管理/ECS实例/实例转为保护状态.md)

[实例移出保护状态](/cn.zh-CN/实例管理/ECS实例/实例移出保护状态.md)

[手动添加ECS实例](/cn.zh-CN/实例管理/ECS实例/手动添加ECS实例.md)

[手动移出ECS实例](/cn.zh-CN/实例管理/ECS实例/手动移出ECS实例.md)

