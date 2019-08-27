# 使用弹性伸缩SDK快速创建多可用区伸缩组 {#concept_63514_zh .task}

本文以Java语言和Python语言为例介绍如何使用弹性伸缩SDK快速创建多可用区的伸缩组。

使用本教程进行操作前，请确保您已经注册了阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。

弹性伸缩的伸缩组分为经典网络伸缩组和专有网络伸缩组。在创建专有网络伸缩组时，您需要配置伸缩组对应的交换机。伸缩组创建完成后，通过该伸缩组弹性扩张的ECS实例都使用该交换机。

原弹性伸缩服务限定一个专有网络伸缩组只能配置一个交换机，由于一个交换机只归属于一个可用区，当您配置好伸缩组的交换机以后，如果交换机所在的可用区因库存不足等原因不能创建ECS实例，您伸缩组中的伸缩配置、伸缩规则以及伸缩组对应的报警任务等都将失效。

为了优化上述问题，提高伸缩组的可用性，伸缩组新增多可用区参数（VSwitchIds.N）。您在创建伸缩组的时候可以使用该参数为伸缩组配置多个交换机，当一个交换机所在可用区无法创建ECS实例的时候，弹性伸缩服务会为您自动切换到其它交换机所在的可用区。在使用该参数的时候，您需要注意以下几点：

-   如果使用了VSwitchIds.N多可用区参数，VSwitchId参数将被忽略。
-   VSwitchIds.N参数中，N的取值范围为\[1, 5\]，即一个伸缩组最多可以配置5个交换机。
-   VSwitchIds.N参数中指定的交换机必须在同一个专有网络下。
-   VSwitchIds.N参数中N代表交换机的优先级，编号为1的交换机为创建实例的第一选择，交换机优先级随编号的增大依次降低。
-   当优先级较高的交换机所在可用区无法创建实例时，会自动选择下一优先级的交换机来创建实例。在使用多可用区参数时，建议设置同一地域下不同可用区的交换机，降低因单可用区库存不足无法创建ECS实例的概率，提高伸缩组的可用性。

## 使用弹性伸缩Java SDK创建多可用区伸缩组 {#section_86e_2h2_53z .section}

1.  导入弹性伸缩Java SDK。 下载依赖库aliyun-java-sdk-core、aliyun-java-sdk-ess，您可以查看[maven-central](https://search.maven.org/)界面，搜索并下载相应的jar包，aliyun-java-sdk-ess对应的jar包的版本号需要是2.1.3及以上版本才能使用多可用区参数，aliyun-java-sdk-core对应的jar包的版本号推荐使用最新版本。

    您也可以使用maven来管理您Java项目的依赖库，在项目对应的pom.xml文件中加入下面的依赖项：

    ``` {#codeblock_y8z_u6d_l8u .language-bash}
    <dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-java-sdk-ess</artifactId>
    <version>2.1.3</version>
    </dependency>
    <dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-java-sdk-core</artifactId>
    <version>3.5.0</version>
    </dependency> 
    ```

2.  使用Java SDK创建多可用区伸缩组。 将弹性伸缩Java SDK导入到Java工程后，您即可以通过SDK编码创建多可用区伸缩组，示例代码如下：

    ``` {#codeblock_g42_hm1_1im .language-bash}
    public class EssSdkDemo {
    public static final String       REGION_ID          = "cn-hangzhou";
    public static final String       AK                 = "ak";
    public static final String       AKS                = "aks";
    public static final Integer      MAX_SIZE           = 10;
    public static final Integer      MIN_SIZE           = 1;
    public static final String       SCALING_GROUP_NAME = "TestScalingGroup";
    
    //交换机列表，交换机优先级从前往后依次降低，第一位的交换机优先级最高。
    public static final String[]     vswitchIdArray     = { "vsw-id1", "vsw-id2", "vsw-id3", "vsw-id4", "vsw-id5" };
    public static final List<String> vswitchIds         = Arrays.asList(vswitchIdArray);
    public static void main(String[] args) throws Exception {
        IClientProfile clientProfile = DefaultProfile.getProfile(REGION_ID, AK, AKS);
        IAcsClient client = new DefaultAcsClient(clientProfile);
        createScalingGroup(client);
    }
    
    /**
     * 创建多可用区伸缩组。
     * @param client
     * @return
     * @throws Exception
    */
    public static String createScalingGroup(IAcsClient client) throws Exception {
        CreateScalingGroupRequest request = new CreateScalingGroupRequest();
        request.setRegionId("cn-beijing");
        request.setMaxSize(MAX_SIZE);
        request.setMinSize(MIN_SIZE);
        request.setScalingGroupName(SCALING_GROUP_NAME);
        request.setVSwitchIds(vswitchIds);
        CreateScalingGroupResponse response = client.getAcsResponse(request);
        return response.getScalingGroupId();
    }
    }          
    ```

    上述代码中，VSwitch的优先级随其在列表中出现的顺序依次降低，排在列表最前面的VSwitch优先级最高。


## 使用弹性伸缩Python SDK创建多可用区伸缩组 {#section_p20_2oi_gm4 .section}

1.  安装弹性伸缩Python SDK。 和Java语言类似，您需要先下载依赖库aliyun-python-sdk-ess、aliyun-python-sdk-core。本文推荐使用pip的方式安装Python依赖包，pip安装说明请参见[Installation-Pip](https://pip.pypa.io/en/latest/installing/)。 安装好pip以后，您可以使用命令`pip install aliyun-python-sdk-ess==2.1.3 pip install aliyun-python-sdk-core==3.5.0`安装两个依赖库。
2.  使用Python SDK创建多可用区伸缩组。 导入弹性伸缩Python SDK依赖库后，您即可以即可以通过SDK编码创建多可用区伸缩组，示例代码如下：

    ``` {#codeblock_egi_9el_rnw .language-bash}
    #  coding=utf-8
    import json
    import logging
    from aliyunsdkcore import client
    from aliyunsdkess.request.v20140828.CreateScalingGroupRequest import CreateScalingGroupRequest
    logging.basicConfig(level=logging.INFO,
                    format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',
                    datefmt='%a, %d %b %Y %H:%M:%S')
    # 请替换自己的ak信息。
    ak = 'ak'
    aks = 'aks'
    scaling_group_name = 'ScalingGroupTest'
    max_size = 10
    min_size = 1
    vswitch_ids = ["vsw-id1", "vsw-id2", "vsw-id3", "vsw-id4", "vsw-id5"]
    region_id = 'cn-beijing'
    clt = client.AcsClient(ak, aks, region_id)   
    ```

    ``` {#codeblock_cp0_qs6_v9r .language-bash}
    def _create_scaling_group():
    request = CreateScalingGroupRequest()
    request.set_ScalingGroupName(scaling_group_name)
    request.set_MaxSize(max_size)
    request.set_MinSize(min_size)
    request.set_VSwitchIds(vswitch_ids)
    response = _send_request(request)
    return response.get('ScalingGroupId')
    ```

    ``` {#codeblock_5j7_lzl_a0k .language-bash}
    def _send_request(request):
    request.set_accept_format('json')
    try:
        response_str = clt.do_action(request)
        logging.info(response_str)
        response_detail = json.loads(response_str)
        return response_detail
    except Exception as e:
        logging.error(e)
    if __name__ == '__main__':
    scaling_group_id = _create_scaling_group()
    print '创建伸缩组成功，伸缩组ID:' + str(scaling_group_id)
    ```

    上述代码中，VSwitch的优先级随其在列表中出现的顺序依次降低，排在列表最前面的VSwitch优先级最高。


## 更多信息 {#section_ujs_j05_2du .section}

-   更多伸缩组创建说明，请参见[CreateScalingGroup](../../../../cn.zh-CN/API参考/伸缩组/CreateScalingGroup.md#)。
-   更多伸缩配置创建说明，请参见[CreateScalingConfiguration](../../../../cn.zh-CN/API参考/伸缩配置/CreateScalingConfiguration.md#)。
-   在控制台创建伸缩组和伸缩配置的过程，请参见[让弹性伸缩更灵活的新特性](cn.zh-CN/最佳实践/让ESS更灵活的新特性.md#)。

