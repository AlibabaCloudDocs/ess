# Use Alibaba Cloud SDK for Python to execute rolling update tasks

Alibaba Cloud SDK for Python allows you to access Alibaba Cloud services without the need to perform complex coding. This topic describes how to use Alibaba Cloud SDK for Python to call API operations provided by Operation Orchestration Service \(OOS\) to execute rolling update tasks on Linux computers.

-   A scaling group is created and ECS instances are added to it.
-   Python is installed on your local computer.
-   A RAM user is created and an AccessKey pair is obtained for the RAM user.

Rolling update tasks can be used to update the configurations of ECS instances in batches. You can use rolling update tasks to update the images of, execute scripts on, and install OOS packages on the running ECS instances in batches in a scaling group.

## Procedure

To use Alibaba Cloud SDK for Python to execute a script on ECS instances on a local computer, perform the following operations:

-   [Step 1: Install Alibaba Cloud SDK for Python](#section_2s7_41j_w30)
-   [Step 2: Execute a rolling update task](#section_ogk_ybh_2p7)
-   [Execute rollback tasks to handle exceptions in rolling update tasks](#section_3n9_swu_j8p)

## Step 1: Install Alibaba Cloud SDK for Python

1.  Run the following command to check the version of Python:

    ```
    python --version
    ```

    If the version of Python is returned, Python is installed. The following figure shows an example command output.

    ![python-version](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4714913061/p165119.png)

2.  Run the following command to install the SDK core library:

    ```
    pip install aliyun-python-sdk-core
    ```

3.  Run the following command to install the OOS SDK:

    ```
    pip install aliyun-python-sdk-oos
    ```


## Step 2: Execute a rolling update task

Sample code is provided in this step to demonstrate how to execute a script on ECS instances.

1.  Create a Python script and enter the code used to execute the rolling update task.

    For information about the OOS template parameters involved in the code, see [OOS template parameters](#section_j3p_cao_xwp). The following content shows the sample code:

    ```
    # -*- coding: UTF-8 -*-
    
    from aliyunsdkcore.client import AcsClient
    from aliyunsdkcore.acs_exception.exceptions import ClientException
    from aliyunsdkcore.acs_exception.exceptions import ServerException
    from aliyunsdkoos.request.v20190601 import StartExecutionRequest
    import json
    
    # Create an AcsClient instance.
    client = AcsClient('<accessKeyId>', '<accessSecret>', 'cn-hangzhou')
    
    # Create a request and configure the JSON data format.
    request = StartExecutionRequest.StartExecutionRequest()
    request.set_accept_format('json')
    
    # Replace the template name based on the selected update method.
    request.set_TemplateName("ACS-ESS-RollingUpdateByRunCommandInScalingGroup")
    
    # Replace parameters based on the selected template.
    parameters = {"invokeType": "invoke",
                  "scalingGroupId": "asg-bp18p2yfxow2dloq****",
                  "commandType": "RunShellScript",
                  "invokeScript": "df -h\nifconfig",
                  "rollbackScript": "df -h\nifconfig",
                  "OOSAssumeRole": "",
                  "exitProcess": [
                      "ScaleIn",
                      "ScaleOut",
                      "HealthCheck",
                      "AlarmNotification",
                      "ScheduledAction"
                    ],
                  "enterProcess": [
                      "ScaleIn",
                      "ScaleOut",
                      "HealthCheck",
                      "AlarmNotification",
                      "ScheduledAction"
                    ],
                  "batchNumber": 2,
                  "batchPauseOption": "Automatic"}
    
    request.set_Parameters(json.dumps(parameters))
    
    # Initiate the API request and show the response.
    response = client.do_action_with_exception(request)
    print(response)
    ```

2.  Execute the Python script and check the output.

    You can find information such as the execution ID of the rolling update task in the output. The following figure shows an example output.

    **Note:** To execute a rollback task, you must enter the execution ID of the source rolling update task.

    ![rollingupdate-py](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4714913061/p165127.png)


## Execute rollback tasks to handle exceptions in rolling update tasks

If exceptions occur during rolling update tasks or you want to use previous configurations after rolling upgrade tasks are executed, you can execute rollback tasks to restore the configurations of the ECS instances. Sample code is provided in this section to demonstrate how to roll back rolling update tasks that have been executed.

1.  Create a Python script and enter the code used to execute the rollback task.

    For information about the OOS template parameters involved in the code, see [OOS template parameters](#section_j3p_cao_xwp). The following content shows the sample code:

    ```
    # -*- coding: UTF-8 -*-
    
    from aliyunsdkcore.client import AcsClient
    from aliyunsdkcore.acs_exception.exceptions import ClientException
    from aliyunsdkcore.acs_exception.exceptions import ServerException
    from aliyunsdkoos.request.v20190601 import StartExecutionRequest
    import json
    
    # Create an AcsClient instance.
    client = AcsClient('<accessKeyId>', '<accessSecret>', 'cn-hangzhou')
    
    # Create a request and configure the JSON data format.
    request = StartExecutionRequest.StartExecutionRequest()
    request.set_accept_format('json')
    
    # Replace the template name based on the selected update method.
    request.set_TemplateName("ACS-ESS-RollingUpdateByRunCommandInScalingGroup")
    
    # Specify the parameters used in the rollback task.
    parameters = {"invokeType": "rollback",
                  "scalingGroupId": "asg-bp18p2yfxow2dlo****",
                  "commandType": "RunShellScript",
                  "rollbackScript": "df -h\nifconfig",
                  "OOSAssumeRole": "",
                  "sourceExecutionId": "exec-8fe4a73e9ffd423****",
                  "batchNumber": 2,
                  "batchPauseOption": "Automatic"}
    
    request.set_Parameters(json.dumps(parameters))
    
    # Initiate the API request and show the response.
    response = client.do_action_with_exception(request)
    print(response)
    ```

2.  Execute the Python script and check the output.

    The following figure shows an example output.

    ![rollingupdate-rollback-py](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4714913061/p165129.png)


## OOS template parameters

This following table lists the parameters of the ACS-ESS-RollingUpdateByRunCommandInScalingGroup public template used in the preceding examples.

|Parameter|Description|
|---------|-----------|
|invokeType|The type of the task. Valid values:-   invoke: rolling update task
-   rollback: rollback task |
|scalingGroupId|The ID of the scaling group in which the task is to be executed.|
|commandType|The type of script to be executed. The value of RunShellScript indicates a shell script.|
|invokeScript|The script that is executed on the ECS instances during a rolling update task.|
|rollbackScript|The script that is executed on the ECS instances during a rollback task.|
|OOSAssumeRole|The RAM role used to execute the task. Default value: OOSServiceRole.|
|enterProcess|The scaling process that is suspended before the task is executed.|
|exitProcess|The scaling process that is resumed when the task is complete.|
|batchNumber|The number of batches in which the ECS instances in the scaling group are divided. The task is executed in these batches. Each batch contains at least one ECS instance.|
|batchPauseOption|Specifies whether and how to suspend the task. Valid values:-   Automatic: The task is not suspended but is complete one time.
-   FirstBatchPause: The task is suspended when the first batch of executions are complete.
-   EveryBatchPause: The task is suspended when each batch of executions are complete. |
|sourceExecutionId|The execution ID of the source rolling update task when a rollback task is executed.|

**Related topics**  


[t1944459.md\#]()

