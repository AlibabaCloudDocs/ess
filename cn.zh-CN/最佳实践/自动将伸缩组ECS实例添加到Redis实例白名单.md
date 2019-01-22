# 自动将伸缩组ECS实例添加到Redis实例白名单 {#concept_nlg_pzb_kgb .concept}

本文介绍如何使用弹性伸缩、消息服务和函数计算，将弹性扩张时创建的ECS实例自动添加到Redis实例的白名单。您可以作为参考，实现更多自动化操作。

## 背景信息 {#section_wcf_szb_kgb .section}

目前，弹性伸缩已经接入负载均衡、云数据库RDS等产品，但是暂未接入云数据库Redis。如果您将业务数据存储在Redis实例上，可能需要配置伸缩组内的ECS实例访问Redis实例。等待ECS实例创建完成后再逐个手动添加不仅费时费力，也容易出现失误，在维护大量实例时成本较高。

针对这种情况，您可以在伸缩组中创建生命周期挂钩，生命周期挂钩在弹性扩张时会自动向指定的MNS主题发送消息，然后通过函数计算中的MNS主题触发器，触发执行上传的代码，自动将ECS实例添加到Redis实例的白名单。

![自动化管理实践-添加ECS实例到Redis白名单流程](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/92948/154816736037006_zh-CN.png)

## 准备工作 {#section_uxw_szb_kgb .section}

在操作前，请确保您已经开通[云数据库Redis](https://www.aliyun.com/product/kvstore)、[消息服务](https://www.aliyun.com/product/mns)、[弹性伸缩](https://www.aliyun.com/product/ess)和[函数计算](https://www.aliyun.com/product/fc)。

## 注意事项 {#section_tnv_m1j_kgb .section}

-   建议在相同地域创建消息服务主题、消息服务队列、函数计算服务、函数计算函数和Redis实例。
-   本文以Java语言的形式给出示例代码，您可以根据业务需求，将此类最佳实践扩展到其它语言。

## 一、云数据库Redis操作步骤 {#section_bbr_n1j_kgb .section}

1.  登录[云数据库Redis控制台](https://kvstorenext.console.aliyun.com/)。
2.  [创建一台Redis实例](../../../../../cn.zh-CN/快速入门/创建实例.md#)，用于为自动创建的ECS实例提供数据库服务。
3.  查看Redis实例的白名单，确定执行代码前的白名单状态。

    ![自动化管理实践-查看Redis实例白名单](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/92948/154816736036915_zh-CN.png)


## 二、消息服务操作步骤 {#section_vsx_p1j_kgb .section}

1.  登录[消息服务控制台](https://mns.console.aliyun.com/)。
2.  [创建一个MNS主题](https://help.aliyun.com/document_detail/34424.html)，用作执行函数的触发器。示例主题的名称为`fc-trigger`。

    ![自动化管理实践-创建MNS主题消息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/92948/154816736036961_zh-CN.png)

3.  [创建一个MNS队列](https://help.aliyun.com/document_detail/34417.html)，用作函数执行结果的接收器。示例队列的名称为`fc-callback`，[示例代码](#section_pzf_ymj_kgb)中通过QUEUE\_NAME指定该队列，发送包含函数执行结果的消息。

    ![自动化管理实践-创建MNS队列消息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/92948/154816736137004_zh-CN.png)


## 三、弹性伸缩操作步骤 {#section_zhc_r1j_kgb .section}

1.  登录[弹性伸缩控制台](https://essnew.console.aliyun.com/)。
2.  创建一个伸缩组，详细步骤请参阅[使用自定义伸缩配置创建伸缩组](../../../../../cn.zh-CN/用户指南/管理伸缩组的伸缩活动/使用自定义伸缩配置创建伸缩组.md#)或者[使用实例启动模板创建伸缩组](../../../../../cn.zh-CN/用户指南/管理伸缩组的伸缩活动/使用实例启动模板创建伸缩组.md#)。
3.  [创建一个生命周期挂钩](../../../../../cn.zh-CN/用户指南/管理伸缩组的伸缩活动/实现自动伸缩/创建生命周期挂钩.md#)。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/92948/154816736136960_zh-CN.png)

    1.  **适用的伸缩活动类型**配置为**弹性扩张活动**，用于通知弹性扩张事件。
    2.  **通知方式**配置为**MNS主题**，与**MNS队列**相比，主题可以通知多个订阅者，执行多种操作。
    3.  **MNS主题**配置为`fc-trigger`，用于在自动创建的ECS实例进入**加入挂起中**状态时执行代码，将ECS实例添加到云数据库Redis的白名单。
    4.  根据需要配置其它选项。

## 四、函数计算操作步骤 {#section_qdb_s1j_kgb .section}

1.  登录[函数计算控制台](https://fc.console.aliyun.com/)。
2.  [新建一个服务](https://help.aliyun.com/document_detail/73337.html)，用于承载需要执行的函数。示例服务的名称为`as-hook-mns-fc-redis`。

    ![自动化管理实践-创建函数计算服务](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/92948/154816736136962_zh-CN.png)

3.  在服务下[新建函数](https://help.aliyun.com/document_detail/73338.html)，订阅MNS主题并上传代码。
    1.  在函数模板页面中，选择**空白函数**。
    2.  在触发器配置页面中，选择**MNS 主题触发器**，然后根据需要配置其它选项。

        ![自动化管理实践-配置函数触发器](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/92948/154816736136966_zh-CN.png)

    3.  在基础管理配置页面中，**所在服务**配置为`as-hook-mns-fc-redis`，**函数入口**配置为`fc.Example::handleRequest`，然后根据需要配置其它选项。

        **说明：** 

        -   **函数入口**由代码决定，请根据实际情况配置。
        -   本文示例采用上传jar包，实现将自动创建的ECS实例添加到云数据库Redis的白名单。有关编程语言说明，请参考[函数计算Java编程说明](https://help.aliyun.com/document_detail/58887.html)。
        ![自动化管理实践-配置函数基础信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/92948/154816736136969_zh-CN.png)

        ![自动化管理实践-配置函数基础信息-函数入口](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/92948/154816736136975_zh-CN.png)

    4.  在权限配置页面中，根据需要授予函数访问其它资源的权限，并授予消息服务调用函数的权限。

        **说明：** 建议遵循权限最小化原则，仅授予必需的权限，防范潜在风险。

        ![自动化管理实践-配置权限-函数计算操作其它资源](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/92948/154816736136976_zh-CN.png)

        ![自动化管理实践-配置权限-调用函数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/92948/154816736136977_zh-CN.png)

    5.  在信息核对页面中，核对**函数信息**和**触发器信息**，然后单击**创建**。

## 执行效果 {#section_ccj_tzb_kgb .section}

配置完成后，执行效果如下：

1.  在满足弹性扩张的条件时，伸缩组触发伸缩活动，自动创建ECS实例。
2.  生命周期挂钩挂起伸缩活动，同时发送消息到MNS主题。
3.  函数计算中，MNS主题触发器触发函数执行过程，并将消息内容作为输入信息（包括ECS实例的ID等信息），执行Java代码。
4.  代码执行时，会通过接口获取ECS实例的私网IP，然后将私网IP添加到Redis实例的白名单（default 分组）。
5.  代码执行结果会发送到MNS队列`fc-callback`，您可以在[消息服务控制台](https://mns.console.aliyun.com/)查看结果详情。下图消息中success为true，表明ECS实例成功添加到了Redis实例的白名单。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/92948/154816736136983_zh-CN.png)

    ![自动化管理实践-查看执行效果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/92948/154816736137014_zh-CN.png)


您还可以继续消费MNS队列中的消息，比如获取success、LifecycleHookId和LifecycleActionToken，编程提前结束生命周期挂钩。

上述最佳实践供您参考，您也在其它场景下通过多款产品实现自动化管理，从而更加灵活地管理伸缩组内的资源。

## 示例代码 {#section_pzf_ymj_kgb .section}

示例代码仅供参考，请结合具体业务进行测试改造。主要功能涉及四个java文件，通过Maven管理，目录结构如下：

![自动化管理实践-Jar包结构](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/92948/154816736137010_zh-CN.png)

Maven依赖如下：

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.aliyun.fc.wujin</groupId>
    <artifactId>demo</artifactId>
    <version>1.0-SNAPSHOT</version>

    <dependencies>
        <dependency>
            <groupId>com.aliyun</groupId>
            <artifactId>aliyun-java-sdk-ecs</artifactId>
            <version>4.10.1</version>
        </dependency>
        <dependency>
            <groupId>com.aliyun.fc.runtime</groupId>
            <artifactId>fc-java-core</artifactId>
            <version>1.0.0</version>
        </dependency>
        <dependency>
            <groupId>com.aliyun</groupId>
            <artifactId>aliyun-java-sdk-core</artifactId>
            <version>3.2.6</version>
        </dependency>
        <dependency>
            <groupId>com.aliyun</groupId>
            <artifactId>aliyun-java-sdk-r-kvstore</artifactId>
            <version>2.0.3</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.25</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>4.2.5.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.apache.httpcomponents</groupId>
            <artifactId>httpclient</artifactId>
            <version>4.5.2</version>
        </dependency>
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>com.springsource.org.apache.commons.lang</artifactId>
            <version>2.6.0</version>
        </dependency>
        <dependency>
            <groupId>com.aliyun.mns</groupId>
            <artifactId>aliyun-sdk-mns</artifactId>
            <version>1.1.8.4</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <artifactId>maven-assembly-plugin</artifactId>
                <version>3.1.0</version>
                <configuration>
                    <descriptorRefs>
                        <descriptorRef>jar-with-dependencies</descriptorRef>
                    </descriptorRefs>
                    <appendAssemblyId>false</appendAssemblyId> <!-- this is used for not append id to the jar name -->
                </configuration>
                <executions>
                    <execution>
                        <id>make-assembly</id> <!-- this is used for inheritance merges -->
                        <phase>package</phase> <!-- bind to the packaging phase -->
                        <goals>
                            <goal>single</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
        </plugins>
    </build>

</project>
```

Example.java代码如下：

```
package fc;

import com.alibaba.fastjson.JSON;
import com.alibaba.fastjson.TypeReference;
import com.aliyun.fc.runtime.Context;
import com.aliyun.fc.runtime.StreamRequestHandler;
import com.aliyun.mns.client.CloudAccount;
import com.aliyun.mns.client.CloudQueue;
import com.aliyun.mns.client.MNSClient;
import com.aliyun.mns.model.Message;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.ecs.model.v20140526.DescribeInstancesRequest;
import com.aliyuncs.ecs.model.v20140526.DescribeInstancesResponse;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.profile.DefaultProfile;
import com.aliyuncs.profile.IClientProfile;
import com.aliyuncs.r_kvstore.model.v20150101.DescribeSecurityIpsRequest;
import com.aliyuncs.r_kvstore.model.v20150101.DescribeSecurityIpsResponse;
import com.aliyuncs.r_kvstore.model.v20150101.ModifySecurityIpsRequest;
import model.FCResult;
import model.HookModel;
import model.MnsMessageModel;
import org.apache.commons.codec.binary.Base64;
import org.apache.commons.lang.StringUtils;
import org.springframework.util.CollectionUtils;

import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
public class Example implements StreamRequestHandler {

    /**
     * 专有网络类型，此参数不用变
     */
    private static final String  VPC_NETWORK                 = "vpc";

    private static final String  CHAR_SET                    = "UTF-8";

    /**
     * 接收input数组大小，4096通常够用
     */
    private static final Integer MAX_BYTE_LENGTH             = 4096;

    /**
     * REDIS 白名单默认分组
     */
    private static final String  DEFAULT_SECURITY_GROUP_NAME = "default";

    /**
     * REDIS 修改白名单的模式
     */
    private static final String  MODIFY_MODE_APPEND          = "Append";

    /**
     * MNS 客户端发送消息地址
     */
    private static final String  MNS_END_POINT               = "http://%s.mns.%s.aliyuncs.com/";

    /**
     * 待添加的REDIS实例ID，根据个人情况替换
     */
    private static final String  REDIS_ID                    = "";

    /**
     * 接收本次函数计算执行结果的队列名称，根据个人情况替换
     */
    private static final String  QUEUE_NAME                  = "wujin-fc-callback";

    /**
     * 阿里云账号UID，根据跟人情况替换
     */
    private static final Long    USER_ID                     = 1111111111111111111L;

    /**
     * 伸缩组 MNS FC 所属的region，根据个人情况替换
     */
    private static final String  REGION_ID                   = "cn-hangzhou";

    @Override
    public void handleRequest(InputStream inputStream, OutputStream outputStream, Context context) {
        FCResult result = new FCResult();
        String akId = context.getExecutionCredentials().getAccessKeyId();
        String akSecret = context.getExecutionCredentials().getAccessKeySecret();
        String securityToken = context.getExecutionCredentials().getSecurityToken();
        try {
            //获取MNS触发函数计算时输入的内容
            String input = readInput(inputStream);
            MnsMessageModel mnsMessageModel = JSON.parseObject(input,
                    new TypeReference<MnsMessageModel>() {
                    });
            if (mnsMessageModel == null) {
                result.setSuccess(false);
                result.setMessage("mnsMessageModel is null");
                sendMns(akId, akSecret, securityToken, result.toString());
                return;
            }
            HookModel contentModel = mnsMessageModel.getContent();
            if (contentModel == null) {
                result.setSuccess(false);
                result.setMessage("contentModel is null");
                sendMns(akId, akSecret, securityToken, result.toString());
                return;
            }
            IAcsClient client = buildClient(akId, akSecret, securityToken);
            //获取本次伸缩活动对应实例的私网IP
            List<String> privateIps = getInstancesPrivateIps(contentModel.getInstanceIds(), client);
            if (CollectionUtils.isEmpty(privateIps)) {
                result.setSuccess(false);
                result.setMessage("privateIps is empty");
                sendMns(akId, akSecret, securityToken, result.toString());
                return;
            }
            List<String> needAppendIps = filterPrivateIpsForAppend(privateIps, client);
            if (!CollectionUtils.isEmpty(needAppendIps)) {
                modifySecurityIps(client, needAppendIps);
                result.setLifecycleHookId(contentModel.getLifecycleHookId());
                result.setLifecycleActionToken(contentModel.getLifecycleActionToken());
                sendMns(akId, akSecret, securityToken, result.toString());
            }
        } catch (Exception ex) {
            result.setSuccess(false);
            result.setMessage(ex.getMessage());
            sendMns(akId, akSecret, securityToken, result.toString());
        }
    }

    /**
     * 构建请求 ECS Redis 接口客户端
     *
     * @param akId
     * @param akSecret
     * @param securityToken
     * @return
     */
    private IAcsClient buildClient(String akId, String akSecret, String securityToken) {
        IClientProfile clientProfile = DefaultProfile.getProfile(REGION_ID, akId, akSecret,
                securityToken);
        return new DefaultAcsClient(clientProfile);
    }

    /**
     * 将执行结果发送消息到MNS
     *
     * @param ak
     * @param aks
     * @param securityToken
     * @param msg
     */
    private void sendMns(String ak, String aks, String securityToken, String msg) {
        MNSClient client = null;
        try {
            CloudAccount account = new CloudAccount(ak, aks,
                    String.format(MNS_END_POINT, USER_ID, REGION_ID), securityToken);
            client = account.getMNSClient();
            CloudQueue queue = client.getQueueRef(QUEUE_NAME);
            Message message = new Message();
            message.setMessageBody(msg);
            queue.putMessage(message);
        } finally {
            if (client != null) {
                client.close();
            }
        }
    }

    /**
     * 过滤出需要添加到redis的私网IP
     *
     * @param privateIps 过滤以前的私网IP
     * @param client
     * @return
     * @throws ClientException
     */
    private List<String> filterPrivateIpsForAppend(List<String> privateIps, IAcsClient client)
            throws ClientException {
        List<String> needAppendIps = new ArrayList<>();
        if (CollectionUtils.isEmpty(privateIps)) {
            return needAppendIps;
        }
        DescribeSecurityIpsRequest request = new DescribeSecurityIpsRequest();
        request.setInstanceId(REDIS_ID);
        DescribeSecurityIpsResponse response = client.getAcsResponse(request);
        List<DescribeSecurityIpsResponse.SecurityIpGroup> securityIpGroups = response
                .getSecurityIpGroups();
        if (CollectionUtils.isEmpty(securityIpGroups)) {
            return privateIps;
        }
        for (DescribeSecurityIpsResponse.SecurityIpGroup securityIpGroup : securityIpGroups) {
            if (!securityIpGroup.getSecurityIpGroupName().equals(DEFAULT_SECURITY_GROUP_NAME)) {
                continue;
            }
            String securityIps = securityIpGroup.getSecurityIpList();
            if (securityIps == null) {
                continue;
            }
            String[] securityIpList = securityIps.split(",");
            List<String> existIps = Arrays.asList(securityIpList);
            if (CollectionUtils.isEmpty(existIps)) {
                continue;
            }
            for (String ip : privateIps) {
                if (!existIps.contains(ip)) {
                    needAppendIps.add(ip);
                }
            }
        }
        return privateIps;
    }

    /**
     * 修改REDIS实例DEFAULT分组私网IP白名单
     *
     * @param client
     * @param needAppendIps
     * @throws ClientException
     */
    private void modifySecurityIps(IAcsClient client, List<String> needAppendIps)
            throws ClientException {
        if (CollectionUtils.isEmpty(needAppendIps)) {
            return;
        }
        ModifySecurityIpsRequest request = new ModifySecurityIpsRequest();
        request.setInstanceId(REDIS_ID);
        String ip = StringUtils.join(needAppendIps.toArray(), ",");
        request.setSecurityIps(ip);
        request.setSecurityIpGroupName(DEFAULT_SECURITY_GROUP_NAME);
        request.setModifyMode(MODIFY_MODE_APPEND);
        client.getAcsResponse(request);
    }

    /**
     * 获取输入，并base64解码
     *
     * @param inputStream
     * @return
     * @throws IOException
     */
    private String readInput(InputStream inputStream) throws IOException {
        try {
            byte[] bytes = new byte[MAX_BYTE_LENGTH];
            int tmp;
            int len = 0;
            //循环读取所有内容
            while ((tmp = inputStream.read()) != -1 && len < MAX_BYTE_LENGTH) {
                bytes[len] = (byte) tmp;
                len++;
            }
            inputStream.close();
            byte[] act = new byte[len];
            System.arraycopy(bytes, 0, act, 0, len);
            return new String(Base64.decodeBase64(act), CHAR_SET);
        } finally {
            inputStream.close();
        }
    }

    /**
     * 获取实例列表对应的私网IP，并限制每次请求实例数量不超过100
     *
     * @param instanceIds 实例列表
     * @param client 请求客户端
     * @return
     * @throws Exception
     */
    public List<String> getInstancesPrivateIps(List<String> instanceIds, IAcsClient client)
            throws Exception {
        List<String> privateIps = new ArrayList<>();
        if (CollectionUtils.isEmpty(instanceIds)) {
            return privateIps;
        }
        int size = instanceIds.size();
        int queryNumberPerTime = 100;
        int batchCount = (int) Math.ceil((float) size / (float) queryNumberPerTime);
        //support 100 instance
        for (int i = 1; i <= batchCount; i++) {
            int fromIndex = queryNumberPerTime * (i - 1);
            int toIndex = Math.min(queryNumberPerTime * i, size);
            List<String> subList = instanceIds.subList(fromIndex, toIndex);
            DescribeInstancesRequest request = new DescribeInstancesRequest();
            request.setInstanceIds(JSON.toJSONString(subList));
            DescribeInstancesResponse response = client.getAcsResponse(request);
            List<DescribeInstancesResponse.Instance> instances = response.getInstances();
            if (CollectionUtils.isEmpty(instances)) {
                continue;
            }
            for (DescribeInstancesResponse.Instance instance : instances) {
                String privateIp = getPrivateIp(instance);
                if (privateIp != null) {
                    privateIps.add(privateIp);
                }
            }
        }
        return privateIps;
    }

    /**
     * 从 DescribeInstancesResponse.Instance 中解析出私网 IP
     *
     * @param instance DescribeInstancesResponse.Instance
     */
    private String getPrivateIp(DescribeInstancesResponse.Instance instance) {
        String privateIp = null;
        if (VPC_NETWORK.equalsIgnoreCase(instance.getInstanceNetworkType())) {
            DescribeInstancesResponse.Instance.VpcAttributes vpcAttributes = instance
                    .getVpcAttributes();
            if (vpcAttributes != null) {
                List<String> privateIpAddress = vpcAttributes.getPrivateIpAddress();
                if (!CollectionUtils.isEmpty(privateIpAddress)) {
                    privateIp = privateIpAddress.get(0);
                }
            }
        } else {
            List<String> innerIpAddress = instance.getInnerIpAddress();
            if (!CollectionUtils.isEmpty(innerIpAddress)) {
                privateIp = innerIpAddress.get(0);
            }
        }
        return privateIp;
    }
}
```

FCResult.java代码如下：

```
package model;

import com.alibaba.fastjson.JSON;

public class FCResult {

  private boolean success = true;

  private String  lifecycleHookId;

  private String  lifecycleActionToken;

  private String  message;

  public boolean isSuccess() {
      return success;
  }

  public void setSuccess(boolean success) {
      this.success = success;
  }

  public String getLifecycleHookId() {
      return lifecycleHookId;
  }

  public void setLifecycleHookId(String lifecycleHookId) {
      this.lifecycleHookId = lifecycleHookId;
  }

  public String getLifecycleActionToken() {
      return lifecycleActionToken;
  }

  public void setLifecycleActionToken(String lifecycleActionToken) {
      this.lifecycleActionToken = lifecycleActionToken;
  }

  public String getMessage() {
      return message;
  }

  public void setMessage(String message) {
      this.message = message;
  }

  @Override
  public String toString() {
      return JSON.toJSONString(this);
  }
}
```

HookModel.java代码如下：

```
package model;

import java.util.List;

public class HookModel {

    private String            lifecycleHookId;

    private String            lifecycleActionToken;

    private String            lifecycleHookName;

    private String            scalingGroupId;

    private String            scalingGroupName;

    private String            lifecycleTransition;

    private String            defaultResult;

    private String            requestId;

    private String            scalingActivityId;

    private List<String>      instanceIds;

    public String getLifecycleHookId() {
        return lifecycleHookId;
    }

    public void setLifecycleHookId(String lifecycleHookId) {
        this.lifecycleHookId = lifecycleHookId;
    }

    public String getLifecycleActionToken() {
        return lifecycleActionToken;
    }

    public void setLifecycleActionToken(String lifecycleActionToken) {
        this.lifecycleActionToken = lifecycleActionToken;
    }

    public String getLifecycleHookName() {
        return lifecycleHookName;
    }

    public void setLifecycleHookName(String lifecycleHookName) {
        this.lifecycleHookName = lifecycleHookName;
    }

    public String getScalingGroupId() {
        return scalingGroupId;
    }

    public void setScalingGroupId(String scalingGroupId) {
        this.scalingGroupId = scalingGroupId;
    }

    public String getScalingGroupName() {
        return scalingGroupName;
    }

    public void setScalingGroupName(String scalingGroupName) {
        this.scalingGroupName = scalingGroupName;
    }

    public String getLifecycleTransition() {
        return lifecycleTransition;
    }

    public void setLifecycleTransition(String lifecycleTransition) {
        this.lifecycleTransition = lifecycleTransition;
    }

    public String getDefaultResult() {
        return defaultResult;
    }

    public void setDefaultResult(String defaultResult) {
        this.defaultResult = defaultResult;
    }

    public String getRequestId() {
        return requestId;
    }

    public void setRequestId(String requestId) {
        this.requestId = requestId;
    }

    public String getScalingActivityId() {
        return scalingActivityId;
    }

    public void setScalingActivityId(String scalingActivityId) {
        this.scalingActivityId = scalingActivityId;
    }

    public List<String> getInstanceIds() {
        return instanceIds;
    }

    public void setInstanceIds(List<String> instanceIds) {
        this.instanceIds = instanceIds;
    }
}
```

MnsMessageModel.java代码如下：

```
package model;

public class MnsMessageModel {

    private String    userId;

    private String    regionId;

    private String    resourceArn;

    private HookModel content;

    public String getUserId() {
        return userId;
    }

    public void setUserId(String userId) {
        this.userId = userId;
    }

    public String getRegionId() {
        return regionId;
    }

    public void setRegionId(String regionId) {
        this.regionId = regionId;
    }

    public String getResourceArn() {
        return resourceArn;
    }

    public void setResourceArn(String resourceArn) {
        this.resourceArn = resourceArn;
    }

    public HookModel getContent() {
        return content;
    }

    public void setContent(HookModel content) {
        this.content = content;
    }
}
```

