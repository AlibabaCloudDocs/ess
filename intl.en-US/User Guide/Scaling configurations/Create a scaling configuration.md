# Create a scaling configuration {#concept_25890_zh .concept}

This topic describes how to create a scaling configuration for a scaling group and specify an ECS instance template for automatic scaling.

## Background information {#section_tjl_mb5_cgb .section}

The scaling configuration creation process is similar to that of an ECS instance. However, as a scaling configuration is a template for ECS instance to be used during automatic scaling, it has several key differences such as supporting different instance types and not allowing you to configure certain parameters \(such as region or resource group\). See the actual interface of the Auto Scaling console when using this document. Brief descriptions of each parameter are also displayed on the interface. For more information about parameter descriptions, see[Create an instance by using the wizard](../../../../../reseller.en-US/Instances/Create an instance/Create an instance by using the wizard.md#) .

## Preparations {#section_t12_2rd_2gb .section}

-   If you need to create a scaling configuration during the[scaling group creation](reseller.en-US/User Guide/Use custom scaling configurations to create scaling groups.md#) process in the Auto Scaling console, perform operations from[step 3](reseller.en-US/User Guide/Scaling configurations/Create a scaling configuration.md#image_d53_ttn_qfb).
-   If you need to use the API examples provided in this topic,[set API access permissions](../../../../../reseller.en-US/General Reference/Create an AccessKey.md#) first.

## Procedure in the Auto Scaling console {#section_vgq_nb5_cgb .section}

1.  Log on to the[Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess). In the**Actions** column corresponding to a scaling group, click**Manage**.
2.  In the left-side navigation pane, clickInstance Configuration Source. On the tab page that appears, click**Create Scaling Configuration**.
3.  On theBasic Configurations page, configure the billing method, instance, image, storage, public network bandwidth, and security group. Click**Next: System Configurations**.

    **Note:** In the basic configurations:

    -   Billing method: Only the[Pay-As-You-Go](../../../../../reseller.en-US/Pricing/Pay-As-You-Go.md#) and[Preemptible instances](../../../../../reseller.en-US/Instances/Instance purchasing options/Preemptible instances/Preemptible instances.md#) methods are supported.
    -   Instance: Multiple instance types are supported. When the instance inventory of a specific type is insufficient, the instances of the alternate types will be used to improve the scaling success rate.
4.  On theSystem Configurations page, configure the logon credential, tag \(optional\), instance name \(optional\), and advanced options \(optional\). Click**Next: Preview**.

    **Note:** Advanced options are available only for scaling configurations in a VPC-type scaling group. The options include RAM role and custom data of instances.

5.  On thePreview page, check your configurations, enter the scaling configuration name, and click**Create**.
6.  In theActivated dialog box that appears, you can click Enable Configuration, click Create More to[create another scaling configuration](reseller.en-US/User Guide/Scaling configurations/Create a scaling configuration.md#image_xnb_stn_qfb), or close the dialog box.

## API example {#section_zd1_prd_2gb .section}

A scaling configuration is a template used by a scaling group to elastically create ECS instances. Before you use an API to create a scaling configuration, make sure that the request contains the ID of a scaling group, the ID of a security group to which ECS instances will belong, the ID of an ECS instance image, and the type of the ECS instances to be used.

We recommend that you choose an[Alibaba Cloud SDK](../../../../../reseller.en-US/Java SDK/Get started.md#) based on your programming language. Java SDK example:

```
import com.aliyuncs.CommonRequest;
import com.aliyuncs.CommonResponse;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.http.MethodType;
import com.aliyuncs.profile.DefaultProfile;
/*
pom.xml
<dependency> 
  <groupId>com.aliyun</groupId> 
  <artifactId>aliyun-java-sdk-core</artifactId> 
  <version>4.0.3</version>
</dependency> 
*/
public class CommonRpc {
    public static void main(String[] args) {
        DefaultProfile profile = DefaultProfile.getProfile("cn-hangzhou", "<accessKeyId>", "<accessSecret>");
        IAcsClient client = new DefaultAcsClient(profile);

        CommonRequest request = new CommonRequest();
        request.setMethod(MethodType.POST);
        request.setDomain("ess.aliyuncs.com");
        request.setVersion("2014-08-28");
        request.setAction("CreateScalingConfiguration");
        request.putQueryParameter("ScalingGroupId", "asg-bp1a4xzjr1ypd6016356");
        request.putQueryParameter("SecurityGroupId", "sg-bp147qpndp7iyj08l74h");
        request.putQueryParameter("ImageId", "centos6u5_64_20G_aliaegis_20140703.vhd");
        request.putQueryParameter("InstanceType", "ecs.t1.xsmall");
        try {
            CommonResponse response = client.getCommonResponse(request);
            System.out.println(response.getData());
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            e.printStackTrace();
        }
    }
}
```

After you have initiated a call through the Java SDK or other methods, the request body is similar as follows:

```
https://ess.aliyuncs.com/?Action=CreateScalingConfiguration
&ImageId=centos6u5_64_20G_aliaegis_20140703.vhd 
&InstanceType=ecs.t1.xsmall 
&ScalingGroupId=asg-bp1a4xzjr1ypd6016356
&SecurityGroupId=sg-bp147qpndp7iyj08l74h
&Version=2014-08-28 
```

In the request,

-    centos6u5\_64\_20G\_aliaegis\_20140703.vhd indicates the ID of the ECS instance image.
-    ecs.t1.xsmall indicates the type of the ECS instances.
-    AG6CQdPU8OKdwLjgZcJ2ea indicates the ID of the scaling group.
-    sg-280ih3w indicates the ID of the scaling group to which the ECS instances will belong.
-    2014-08-28 indicates the version of the API.

You can also customize attributes such as different instance types and ECS instance disks. For more information about the API, see[CreateScalingConfiguration](../../../../../reseller.en-US/API-Reference/Scaling configuration/CreateScalingConfiguration.md#).

