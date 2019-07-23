# Automatically add ECS instances of a scaling group to a Redis instance whitelist {#concept_nlg_pzb_kgb .concept}

This topic describes how to add scaled-out ECS instances to the whitelist of an ApsaraDB for Redis \(Redis\) instance by using Auto Scaling, Message Service \(MNS\), and Function Compute. You can refer to this topic to learn how to perform more automated operations.

## Background information {#section_wcf_szb_kgb .section}

Auto Scaling is integrated with Server Load Balancer \(SLB\) and Relational Database Service \(RDS\), but is not integrated with ApsaraDB for Redis. If your business data is stored in a Redis instance, you need to perform certain operations to allow ECS instances of a scaling group to access the Redis instance. Manually adding every created ECS instance to the Redis instance whitelist is time-consuming and prone to mistakes. When there are a large number of instances, manually adding these instances incurs large costs.

In this case, you can create a lifecycle hook in a scaling group. During a scale-out process, the lifecycle hook automatically sends messages to a specific MNS topic. Then, an MNS topic trigger in Function Compute executes the uploaded code to add the scaled-out ECS instances to the whitelist of the Redis instance.

## Preparations {#section_uxw_szb_kgb .section}

Before you start, ensure that you have activated [ApsaraDB for Redis](https://partners-intl.aliyun.com/vodafone/product/apsaradb-for-redis), [Message Service](https://partners-intl.aliyun.com/vodafone/product/message-service), [Auto Scaling](https://partners-intl.aliyun.com/vodafone/product/auto-scaling), and [Function Compute](https://partners-intl.aliyun.com/vodafone/product/function-compute).

## Notes {#section_tnv_m1j_kgb .section}

-   We recommend that you create MNS topics, MNS queues, Function Compute services, Function Compute functions, and Redis instances in the same region.
-   This topic provides sample code written in Java. You can follow these best practices with other programming languages.

## 1. Procedure in ApsaraDB for Redis {#section_bbr_n1j_kgb .section}

1.  Log on to the [ApsaraDB for Redis console](https://partners-intl.console.aliyun.com/#/kvstore).
2.  [Create a Redis instance](../../../../reseller.en-US/.md#) that serves as the database for automatically created ECS instances.
3.  View the Redis instance whitelist to check the whitelist status before code execution.

## 2. Procedure in Message Service {#section_vsx_p1j_kgb .section}

1.  Log on to the [Message Service console](https://partners-intl.console.aliyun.com/#/mns).
2.  Create an MNS topic that will be used as a function trigger. Set the topic name to `fc-trigger`.
3.  Create an MNS queue that will be used to receive function execution results. Set the queue name to `fc-callback`. In the [sample code](#section_pzf_ymj_kgb), QUEUE\_NAME is set to this queue name to send function execution results.

## 3. Procedure in Auto Scaling {#section_zhc_r1j_kgb .section}

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  Create a scaling group. For more information, see [Use custom scaling configurations to create scaling groups](../../../../reseller.en-US/User Guide/Realize Auto Scaling/Use custom scaling configurations to create scaling groups.md#) or [Use launch templates to create scaling groups](../../../../reseller.en-US/User Guide/Realize Auto Scaling/Use launch templates to create scaling groups.md#).
3.  [Create a lifecycle hook](../../../../reseller.en-US/User Guide/Realize Auto Scaling/Create a lifecycle hook.md#).
    1.  Set **Scaling Activity Type** to **Scale-Out** to notify of scale-out activities.
    2.  Set **Notification Method** to **MNS Topic**. Compared with the **MNS Queue** method, the MNS Topic method can be used to notify multiple subscribers and execute various operations.
    3.  Set **MNS Topic** to `fc-trigger`. When automatically created ECS instances enter the **Adding: Wait** state, this topic is used to execute code to add the instances to the whitelist of a Redis instance.
    4.  Configure other parameters as required.

## 4. Procedure in Function Compute {#section_qdb_s1j_kgb .section}

1.  Log on to the [Function Compute](https://partners-intl.console.aliyun.com/#/fc) console.
2.  [Create a service](https://partners-intl.aliyun.com/help/doc-detail/73337.htm) for functions to be executed. Set the service name to `as-hook-mns-fc-redis`.
3.  Under the created service, create a function to subscribe to the MNS topic, and upload the code. For more information, see [Create a function](https://partners-intl.aliyun.com/help/doc-detail/52077.htm).
    1.  On the Function Template page, select **Empty Function**.
    2.  On the Trigger Configuration page, select **MNS Topic Trigger** from the Trigger Type drop-down list and configure other parameters as required.
    3.  On the Configure Function Settings page, set **Service Name** to `as-hook-mns-fc-redis` and **Function Handler** to `fc.Example::handleRequest`, and configure other parameters as required.

        **Note:** 

        -   **Function Handler** varies with code. Set this parameter based on the actual conditions.
        -   In the examples provided in this topic, a JAR package is uploaded to add automatically created ECS instances to the whitelist of a Redis instance. For more information about Java programming descriptions, see [Java programming in Function Compute](https://partners-intl.aliyun.com/help/doc-detail/58887.htm).
    4.  On the Permission Configuration page, grant permissions on necessary resources to the function and allow Message Service to call functions.

        **Note:** We recommend that you follow the principle of least privilege and only grant necessary permissions to prevent potential risks.

    5.  On the Preview page, confirm **Function Information** and **Trigger Information**, and click **Create**.

## Expected results {#section_ccj_tzb_kgb .section}

After the configurations are completed, the expected results are as follows:

1.  When the scaling conditions are met, the scaling group triggers the scaling activity and automatically creates ECS instances.
2.  The lifecycle hook suspends the scaling activity and sends a message to the MNS topic.
3.  In Function Compute, the MNS topic trigger triggers the function, fills in the Java code with the message content \(such as ECS IDs\), and executes the code.
4.  When the code is being executed, the private IP addresses of the ECS instances are obtained and then added to the default group of the Redis instance whitelist.
5.  The result of the executed code is sent to MNS queue `fc-callback`. You can view the result details in the [Message Service console](https://partners-intl.console.aliyun.com/#/mns). If success in the message content is true as shown in the following figure, the ECS instances have been added to the whitelist of the Redis instance.

You can also continue to consume messages in the MNS queue, such as obtaining the success, LifecycleHookId, and LifecycleActionToken parameters. With these parameters, you can stop a lifecycle hook in advance.

The preceding best practices are for your reference. You can also use other necessary services to manage resources in your scaling groups with more flexibility.

## Sample code {#section_pzf_ymj_kgb .section}

The sample code is for reference only. Use and test the code based on your actual conditions. Maven is used to manage the Java files that are used to add the instances to the whitelist. The directory structure is as follows:

Maven dependencies:

``` {#codeblock_4fz_ehh_5vt}
<? xml version="1.0" encoding="UTF-8"? > 
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
            <version>4.2.5. RELEASE</version>
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
                    <appendAssemblyId>false</appendAssemblyId> <! -- this is used for not append id to the jar name -->
                </configuration>
                <executions>
                    <execution>
                        <id>make-assembly</id> <! -- this is used for inheritance merges -->
                        <phase>package</phase> <! -- bind to the packaging phase -->
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

Example of Example. java:

``` {#codeblock_961_y1g_v90}
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
import com.aliyuncs.ecs.model.v20140526. DescribeInstancesRequest;
import com.aliyuncs.ecs.model.v20140526. DescribeInstancesResponse;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.profile.DefaultProfile;
import com.aliyuncs.profile.IClientProfile;
import com.aliyuncs.r_kvstore.model.v20150101. DescribeSecurityIpsRequest;
import com.aliyuncs.r_kvstore.model.v20150101. DescribeSecurityIpsResponse;
import com.aliyuncs.r_kvstore.model.v20150101. ModifySecurityIpsRequest;
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
     * The VPC network. Do not change the value.
     */
    private static final String  VPC_NETWORK                 = "vpc";

    private static final String  CHAR_SET                    = "UTF-8";

    /**
     * The size of the array receiving input information. A value of 4096 is sufficient in most cases.
     */
    private static final Integer MAX_BYTE_LENGTH             = 4096;

    /**
     * The default group of the Redis instance whitelist.
     */
    private static final String  DEFAULT_SECURITY_GROUP_NAME = "default";

    /**
     * The method for modifying the REDIS instance whitelist.
     */
    private static final String  MODIFY_MODE_APPEND          = "Append";

    /**
     * The address that the MNS client uses to send messages.
     */
    private static final String  MNS_END_POINT               = "http://%s.mns.%s.aliyuncs.com/";

    /**
     * The Redis instance ID to be added. Set the value based on the actual conditions.
     */
    private static final String  REDIS_ID                    = "";

    /**
     * The name of the queue that receives the result of the executed function. Set the value based on the actual conditions.
     */
    private static final String  QUEUE_NAME                  = "wujin-fc-callback";

    /**
     * The Alibaba Cloud account ID. Set the value based on the actual conditions.
     */
    private static final Long    USER_ID                     = 1111111111111111111L;

    /**
     * The region to which the scaling group, Message Service, and Function Compute belong. Set the value based on the actual conditions.
     */
    private static final String  REGION_ID                   = "cn-hangzhou";

    @Override
    public void handleRequest(InputStream inputStream, OutputStream outputStream, Context context) {
        FCResult result = new FCResult();
        String akId = context.getExecutionCredentials().getAccessKeyId();
        String akSecret = context.getExecutionCredentials().getAccessKeySecret();
        String securityToken = context.getExecutionCredentials().getSecurityToken();
        try {
            //Obtain the content that an MNS trigger used to trigger function execution
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
            //Obtain the private IP addresses of ECS instances that are being scaled.
            List<String> privateIps = getInstancesPrivateIps(contentModel.getInstanceIds(), client);
            if (CollectionUtils.isEmpty(privateIps)) {
                result.setSuccess(false);
                result.setMessage("privateIps is empty");
                sendMns(akId, akSecret, securityToken, result.toString());
                return;
            }
            List<String> needAppendIps = filterPrivateIpsForAppend(privateIps, client);
            if (! CollectionUtils.isEmpty(needAppendIps)) {
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
     * Build a client used for Redis API requests.
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
     * Send the execution result to Message Service as a message.
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
            if (client ! = null) {
                client.close();
            }
        }
    }

    /**
     * Filter out the private IP addresses that need to be added to the whitelist of the Redis instance.
     *
     * @ Param privateIps Filter out the private IP addresses of previous ECS instances.
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
            if (! securityIpGroup.getSecurityIpGroupName().equals(DEFAULT_SECURITY_GROUP_NAME)) {
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
                if (! existIps.contains(ip)) {
                    needAppendIps.add(ip);
                }
            }
        }
        return privateIps;
    }

    /**
     * Modify the private IP addresses in the default group of the Redis instance whitelist.
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
     * Obtain the input content and perform Base64 decoding.
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
            //Repeatedly read all content.
            while ((tmp = inputStream.read()) ! = -1 && len < MAX_BYTE_LENGTH) {
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
     * Obtain the private IP addresses of all listed instances and limit the maximum number of instances to 100 per request.
     *
     * @param instanceIds The list of instances.
     * @param client The request client.
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
                if (privateIp ! = null) {
                    privateIps.add(privateIp);
                }
            }
        }
        return privateIps;
    }

    /**
     * Obtain the private IP addresses from DescribeInstancesResponse.Instance.
     *
     * @param instance DescribeInstancesResponse.Instance
     */
    private String getPrivateIp(DescribeInstancesResponse.Instance instance) {
        String privateIp = null;
        if (VPC_NETWORK.equalsIgnoreCase(instance.getInstanceNetworkType())) {
            DescribeInstancesResponse.Instance.VpcAttributes vpcAttributes = instance
                    .getVpcAttributes();
            if (vpcAttributes ! = null) {
                List<String> privateIpAddress = vpcAttributes.getPrivateIpAddress();
                if (! CollectionUtils.isEmpty(privateIpAddress)) {
                    privateIp = privateIpAddress.get(0);
                }
            }
        } else {
            List<String> innerIpAddress = instance.getInnerIpAddress();
            if (! CollectionUtils.isEmpty(innerIpAddress)) {
                privateIp = innerIpAddress.get(0);
            }
        }
        return privateIp;
    }
}
```

Example of FCResult. java:

``` {#codeblock_d8s_6d4_80v}
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

Example of HookModel. java:

``` {#codeblock_p4x_n2o_ve7}
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

Example of MnsMessageModel. java:

``` {#codeblock_tp7_bia_gsl}
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

