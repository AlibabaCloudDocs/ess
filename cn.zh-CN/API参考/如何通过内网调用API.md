# 如何通过内网调用API {#task_2054849 .task}

本文通过配置云解析PrivateZone，为伸缩组中无公网访问能力的专有网络VPC类型ECS实例提供了通过阿里云内网调用API的方案。

由于弹性伸缩提供的接入地址（Endpoint）为公网服务地址，当伸缩组ECS实例没有分配公网带宽或者不存在公网IP地址时，无法使用阿里云CLI或者SDK等工具发起API请求。此时，您可以为伸缩组ECS实例所在地域下的专有网络VPC关联云解析PrivateZone，即可实现在阿里云内网调用API。

-   此方案仅适用于伸缩组中专有网络VPC类型ECS实例所在的地域，不支持跨地域配置云解析PrivateZone。
-   建议您在伸缩配置中使用已部署了阿里云CLI或者SDK的自定义镜像，避免伸缩组实例在无公网访问的条件下无法加载相关依赖。
-   目前，支持云解析PrivateZone的弹性伸缩接入地址（Endpoint）如下表所示，请确保您使用的Endpoint在列举范围内。

    |阿里云地域|地域ID|CNAME记录值|公网接入地址（Endpoint）|
    |-----|----|--------|----------------|
    |华北2（北京）|cn-beijing|popunify-vpc.cn-beijing.aliyuncs.com|ess.cn-beijing.aliyuncs.com|
    |华东1（杭州）|cn-hangzhou|popunify-vpc.cn-hangzhou.aliyuncs.com|ess.cn-hangzhou.aliyuncs.com|
    |华东2（上海）|cn-shanghai|popunify-vpc.cn-shanghai.aliyuncs.com|ess.cn-shanghai.aliyuncs.com|
    |华南 1（深圳）|cn-shenzhen|popunify-vpc.cn-shenzhen.aliyuncs.com|ess.cn-shenzhen.aliyuncs.com|
    |中国（香港）|cn-hongkong|popunify-vpc.cn-hongkong.aliyuncs.com|ess.cn-hongkong.aliyuncs.com|
    |新加坡|ap-southeast-1|popunify-vpc.ap-southeast-1.aliyuncs.com|ess.ap-southeast-1.aliyuncs.com|


1.  登录[云解析控制台](https://dns.console.aliyun.com/#/dns/domainList)。
2.  前往**PrivateZone**，然后单击**添加Zone**。
3.  完成以下设置后，单击**确定**。 

    -   **Zone名称**：设置一个已支持云解析PrivateZone的云服务器ECS接入地址，如ess.cn-hangzhou.aliyuncs.com。
    -   **子域名递归解析代理**：勾选后，当DNS查询的域名以Zone名称为后缀，但是在Zone文件里未配置时，会以公网的权威解析为准。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1630494/156766946759246_zh-CN.png)

4.  找到已创建的PrivateZone，在**操作**列，单击**解析设置**。
5.  在**解析设置**页面，单击**添加记录**。
6.  在添加记录弹窗中，完成以下设置后，单击**确定**。 

    -   **记录类型**：选择CNAME。
    -   **主机记录**：填写@可以解析@.exmaple.com域名。
    -   **记录值**：设置为对应地域下的CNAME记录值。
    -   **TTL值**：生存时间，本文选择了**1 分钟**。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1630494/156766946759247_zh-CN.png)

7.  返回PrivateZone列表页面，找到已创建的PrivateZone，在**操作**列，单击**关联VPC**。
8.  选择与PrivateZone相同的地域，勾选需要关联的专有网络VPC，然后单击**确定**。 

    **说明：** 请选择伸缩组ECS实例所在的专有网络VPC。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1630494/156766946759249_zh-CN.png)


为专有网络VPC关联了云解析PrivateZone后，您可以通过远程登录伸缩组ECS实例，在ECS实例内部测试是否能访问对应地域的接入地址，具体登录操作请参见[使用管理终端连接Linux实例](../../../../cn.zh-CN/实例/连接实例/连接Linux实例/使用管理终端连接Linux实例.md#)。

下面以ess.cn-hangzhou.aliyuncs.com为例演示测试效果：

-   使用ping功能测试数据包收发状况。

    ``` {#codeblock_zd0_jwo_mst}
    ping ess.cn-hangzhou.aliyuncs.com
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1630494/156766946759255_zh-CN.png)

-   使用阿里云CLI调用[DescribeRegions](cn.zh-CN/API参考/地域/DescribeRegions.md#)，并通过--endpoint字段修改接入地址。

    ``` {#codeblock_fzg_s7t_v51}
    aliyun ecs DescribeRegions --endpoint ess.cn-hangzhou.aliyuncs.com
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1630494/156766946759256_zh-CN.png)


