# Use Alibaba Cloud ESS SDK to create a multi-zone scaling group

This topic describes how to use Alibaba Cloud ESS SDK for Java or Python to create a multi-zone scaling group.

Before you perform the operations provided in the tutorial, you must have registered an Alibaba Cloud account. To create an Alibaba Cloud account, click [Create a new Alibaba Cloud account](https://account.alibabacloud.com/register/intl_register.htm).

The network type of a scaling group can be Virtual Private Cloud \(VPC\) or classic network. When you create a VPC-connected scaling group, you must configure a VSwitch for the scaling group. After the scaling group is created, all ECS instances that are created for the scaling group use this VSwitch.

Originally, Auto Scaling allows a VPC-connected scaling group to have only one VSwitch configured. A VSwitch belongs to only one zone. If ECS instances cannot be created in the zone where the VSwitch resides due to reasons such as insufficient resources, the scaling configurations, scaling rules, and event-triggered tasks in the scaling group become invalid.

To address the preceding issue and improve the availability of scaling groups, the VSwitchIds.N parameter is added to allow you to create multi-zone scaling groups. When you create a scaling group, you can use the VSwitchIds.N parameter to configure multiple VSwitches for the scaling group. When ECS instances cannot be created in the zone where a VSwitch resides, Auto Scaling automatically switches to the zone where a different VSwitch resides. When you use this parameter, take note of the following items:

-   If the VSwitchIds.N parameter is specified, the VSwitchId parameter is ignored.
-   The VSwitchIds.N parameter allows you to specify up to five VSwitches within a VPC across multiple zones when you create a scaling group. Valid values of N: 1 to 5.
-   VSwitches specified in the VSwitchIds. N parameter must be within the same VPC.
-   In the VSwitchIds.N parameter, N indicates the priority of each VSwitch. The VSwitch with N set to 1 has the highest priority to create ECS instances. The greater the N value, the lower the priority.
-   When an ECS instance cannot be created in the zone where the VSwitch with the highest priority resides, the instance will be created in the zone where the VSwitch with the second highest priority resides. We recommend that you specify multiple VSwitches across different zones in the same region to avoid failing to create ECS instances due to insufficient resources in a single zone and improve the availability of scaling groups.

## Use Alibaba Cloud ESS SDK for Java to create a multi-zone scaling group

1.  Install Alibaba Cloud ESS SDK for Java.

    Download the aliyun-java-sdk-core and aliyun-java-sdk-ess dependency libraries. You can visit [Maven Central](https://search.maven.org/) to search for and download the corresponding JAR packages. The JAR package version for aliyun-java-sdk-ess must be V2.1.3 or later and the package version for aliyun-java-sdk-core must be the latest.

    You can also use Apache Maven to manage the dependency libraries of your Java projects by adding the following dependencies to the pom.xml file:

    ```
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

2.  Use SDK for Java to create a multi-zone scaling group.

    After Alibaba Cloud ESS SDK for Java is imported to a Java project, you can use the SDK code to create a multi-zone scaling group. The following section shows the sample code:

    ```
    public class EssSdkDemo {
    public static final String       REGION_ID          = "cn-hangzhou";
    public static final String       AK                 = "ak";
    public static final String       AKS                = "aks";
    public static final Integer      MAX_SIZE           = 10;
    public static final Integer      MIN_SIZE           = 1;
    public static final String       SCALING_GROUP_NAME = "TestScalingGroup";
    
    // The list of VSwitches. The VSwitches are listed in descending order of priority. The first VSwitch has the highest priority.
    public static final String[]     vswitchIdArray     = { "vsw-id1", "vsw-id2", "vsw-id3", "vsw-id4", "vsw-id5" };
    public static final List<String> vswitchIds         = Arrays.asList(vswitchIdArray);
    public static void main(String[] args) throws Exception {
        IClientProfile clientProfile = DefaultProfile.getProfile(REGION_ID, AK, AKS);
        IAcsClient client = new DefaultAcsClient(clientProfile);
        createScalingGroup(client);
    }
    
    /**
     * Create a multi-zone scaling group.
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

    In the preceding code, the VSwitches are listed in descending order of priority. The first VSwitch has the highest priority.


## Use Alibaba Cloud ESS SDK for Python to create a multi-zone scaling group

1.  Install Alibaba Cloud ESS SDK for Python.

    To install Alibaba Cloud ESS SDK for Python, you must download and install the aliyun-python-sdk-ess and aliyun-python-sdk-core dependency libraries. We recommend that you use pip to install Python dependency libraries. For more information, visit [Installation-pip](https://pip.pypa.io/en/latest/installing/). After pip is installed, run the `pip install aliyun-python-sdk-ess==2.1.3 pip install aliyun-python-sdk-core==3.5.0` command to install the dependency libraries.

2.  Use SDK for Python to create a multi-zone scaling group.

    After Alibaba Cloud ESS SDK for Python is imported to a Python project, you can use the SDK code to create a multi-zone scaling group. The following section shows the sample code:

    ```
    #  coding=utf-8
    import json
    import logging
    from aliyunsdkcore import client
    from aliyunsdkess.request.v20140828.CreateScalingGroupRequest import CreateScalingGroupRequest
    logging.basicConfig(level=logging.INFO,
                    format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',
                    datefmt='%a, %d %b %Y %H:%M:%S')
    # Replace the following ak and aks values with your own AccessKey ID and AccessKey secret:
    ak = 'ak'
    aks = 'aks'
    scaling_group_name = 'ScalingGroupTest'
    max_size = 10
    min_size = 1
    vswitch_ids = ["vsw-id1", "vsw-id2", "vsw-id3", "vsw-id4", "vsw-id5"]
    region_id = 'cn-beijing'
    clt = client.AcsClient(ak, aks, region_id)   
    ```

    ```
    def _create_scaling_group():
    request = CreateScalingGroupRequest()
    request.set_ScalingGroupName(scaling_group_name)
    request.set_MaxSize(max_size)
    request.set_MinSize(min_size)
    request.set_VSwitchIds(vswitch_ids)
    response = _send_request(request)
    return response.get('ScalingGroupId')
    ```

    ```
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
    print 'Scaling group created successfully. Scaling group ID:' + str (scaling_group_id)
    ```

    In the preceding code, the VSwitches are listed in descending order of priority. The first VSwitch has the highest priority.


**Reference**  


[CreateScalingGroup](/intl.en-US/API Reference/Scaling group/CreateScalingGroup.md)

[CreateScalingConfiguration](/intl.en-US/API Reference/Scaling configuration/CreateScalingConfiguration.md)

[Configure parameters in a scaling configuration to implement automatic deployment](/intl.en-US/Best practices/Configure parameters in a scaling configuration to implement automatic deployment.md)

