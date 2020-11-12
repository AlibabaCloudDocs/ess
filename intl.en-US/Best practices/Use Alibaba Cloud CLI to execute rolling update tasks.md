# Use Alibaba Cloud CLI to execute rolling update tasks

Alibaba Cloud Command Line Interface \(Alibaba Cloud CLI\) is a management tool based on Alibaba Cloud OpenAPI. You can use Alibaba Cloud CLI to call Alibaba Cloud APIs to flexibly manage and scale Alibaba Cloud services. This topic describes how to use Alibaba Cloud CLI to perform rolling update tasks.

-   Alibaba Cloud CLI is installed. For more information about how to install Alibaba Cloud CLI, see the "Installation Guide" section in [What is Alibaba Cloud CLI?]()
-   A scaling group is created and ECS instances are added to it.
-   The instance configuration source of the scaling group is a scaling configuration if you want to update the images of ECS instances in the scaling group.
-   Operation Orchestration Service \(OOS\) packages are created if you want to install OOS packages on ECS instances in the scaling group. For more information, see [Manage custom software on multiple ECS instances](https://www.alibabacloud.com/help/zh/doc-detail/169939.htm).

Rolling update tasks can be used to update the configurations of ECS instances in batches. For more information, see [Rolling update](/intl.en-US/Scaling Group/Rolling update.md).

## Procedure

This topic describes how to use Alibaba Cloud CLI to update images of, execute scripts on, and install OOS packages on ECS instances in a scaling group. Perform the following operations:

-   [Step 1: Create a RAM user and grant it permissions](#section_d0w_yd2_kov)
-   [Step 2: Configure and verify Alibaba Cloud CLI](#section_par_u1c_nco)
-   [Step 3: Use Alibaba Cloud CLI to execute a rolling update task](#section_cxb_gj6_plx)
-   [Execute rollback tasks to handle exceptions in rolling update tasks](#section_od2_7q0_tlh)

## Step 1: Create a RAM user and grant it permissions

1.  Log on to the [RAM console](https://ram.console.aliyun.com/).

2.  Create a RAM user.

    A RAM user named clitest is created in this example. For more information, see [Create a RAM user](/intl.en-US/RAM User Management/Create a RAM user.md).

    1.  In the left-side navigation pane, choose **Identities** \> **Users**.

    2.  On the Users page, click **Create User**.

    3.  On the **Create User** page, configure the parameters and then click **OK**.

        The following table describes the parameters.

        |Parameter|Example|
        |---------|-------|
        |**Logon Name**|clitest@sample.com|
        |**Display Name**|clitest|
        |**Access Mode**|**Programmatic Access**.An AccessKey pair is automatically created for the RAM user. The RAM user can call API operations or use SDKs to access Alibaba Cloud resources. |

    4.  On the **Basic Information** page, click **Download CSV File**.

        **Note:** The AccessKey secret is displayed only when you create an AccessKey pair, and is unavailable for subsequent queries. We recommend that you save the AccessKey secret for subsequent use. If an AccessKey pair is disclosed or lost, you must create a new one.

3.  Grant the RAM user permissions to manage resources.

    1.  In the left-side navigation pane, choose **Identities** \> **Users**.

    2.  Find the clitest user that you created. Click **Add Permissions** in the **Actions** column.

    3.  In the Add Permissions panel, select the policies that contain the permissions required to execute the rolling update task, and then click **OK**.

        The following table describes the parameters in the Add Permissions panel.

        |Parameter|Description|
        |---------|-----------|
        |**Authorization**|Keep the **Alibaba Cloud account all resources** default value selected.|
        |**Principal**|Keep the clitest@sample.com default value selected.|
        |**Select Policy**|Select the following system policies:        -   AliyunECSFullAccess: Provides permissions to manage Elastic Compute Service \(ECS\) resources such as ECS instances.
        -   AliyunESSFullAccess: Provides permissions to manage Auto Scaling resources such as scaling groups.
        -   AliyunOOSFullAccess: Provides permissions to manage OOS resources such as executions.
        -   AliyunOSSFullAccess: Provides permissions to manage Object Storage Service \(OSS\) resources such as buckets. |


## Step 2: Configure and verify Alibaba Cloud CLI

For information about the configuration parameters, see the "Configure Alibaba Cloud CLI" section in [What is Alibaba Cloud CLI?]()

1.  Open Alibaba Cloud CLI on your local computer.

2.  Configure Alibaba Cloud CLI.

    1.  Run the following command to open the configuration file:

        ```
        aliyun configure
        ```

    2.  Enter the AccessKey ID and AccessKey secret.

        ![cli-config](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6724913061/p160873.png)

3.  Run the following command to check whether Alibaba Cloud CLI is available:

    ```
    aliyun ecs DescribeRegions
    ```

    This command is used to query supported regions. If region information is returned, the command is executed. The following figure shows an example command output.

    ![cli-example](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6724913061/p160879.png)


## Step 3: Use Alibaba Cloud CLI to execute a rolling update task

This step provides example commands to demonstrate how to update images of, execute scripts on, and install OOS packages on ECS instances in the scaling group.

1.  Run an Alibaba Cloud CLI command to execute a rolling update task.

    For information about the OOS template parameters involved in the code, see [OOS template parameters](#section_gju_4ho_zbw).

    -   In the following example, an image update command is used to update images of ECS instances in the scaling group to Alibaba Cloud Linux 2.1903 LTS 64-bit.

        ```
        aliyun oos StartExecution --TemplateName ACS-ESS-RollingUpdateByReplaceSystemDiskInScalingGroup --Parameters "{
                \"invokeType\": \"invoke\",
                \"scalingGroupId\": \"asg-bp18p2yfxow2dloq****\",
                \"scalingConfigurationId\": \"asc-bp1bx8mzur534edp****\",
                \"imageId\": \"aliyun_2_1903_x64_20G_alibase_20200529.vhd\",
                \"sourceImageId\": \"centos_7_8_x64_20G_alibase_20200717.vhd\",
                \"OOSAssumeRole\": \"\",
                \"enterProcess\": [
                  \"ScaleIn\",
                  \"ScaleOut\",
                  \"HealthCheck\",
                  \"AlarmNotification\",
                  \"ScheduledAction\"
                ],
                \"exitProcess\":  [
                  \"ScaleIn\",
                  \"ScaleOut\",
                  \"HealthCheck\",
                  \"AlarmNotification\",
                  \"ScheduledAction\"
                ],
                \"batchNumber\": 2,
                \"batchPauseOption\": \"Automatic\"
              }"
        ```

    -   In the following example, a script execution command is used to run the df -h and ifconfig shell commands on ECS instances in the scaling group to view the disks and network configurations of the instances.

        ```
        aliyun oos StartExecution --TemplateName ACS-ESS-RollingUpdateByRunCommandInScalingGroup --Parameters "{
                \"invokeType\": \"invoke\",
                \"scalingGroupId\": \"asg-bp18p2yfxow2dloq****\",
                \"commandType\": \"RunShellScript\",
                \"invokeScript\": \"df -h\nifconfig\",
                \"rollbackScript\": \"df -h\nifconfig\",
                \"OOSAssumeRole\": \"\",
                \"exitProcess\": [
                  \"ScaleIn\",
                  \"ScaleOut\",
                  \"HealthCheck\",
                  \"AlarmNotification\",
                  \"ScheduledAction\"
                ],
                \"enterProcess\": [
                  \"ScaleIn\",
                  \"ScaleOut\",
                  \"HealthCheck\",
                  \"AlarmNotification\",
                  \"ScheduledAction\"
                ],
                \"batchNumber\": 2,
                \"batchPauseOption\": \"Automatic\"
              }"
        ```

    -   In the following example, a command for installing OOS packages is used to install the WordPress package on all ECS instances in the scaling group.

        ```
        aliyun oos StartExecution --TemplateName ACS-ESS-RollingUpdateByConfigureOOSPackage --Parameters "{
                \"invokeType\": \"invoke\",
                \"scalingGroupId\": \"asg-bp18p2yfxow2dloq****\",
                \"packageName\": \"wordpress\",
                \"packageVersion\": \"v4\",
                \"action\": \"install\",
                \"OOSAssumeRole\": \"\",
                \"enterProcess\": [
                  \"ScaleIn\",
                  \"ScaleOut\",
                  \"HealthCheck\",
                  \"AlarmNotification\",
                  \"ScheduledAction\"
                ],
                \"exitProcess\": [
                  \"ScaleIn\",
                  \"ScaleOut\",
                  \"HealthCheck\",
                  \"AlarmNotification\",
                  \"ScheduledAction\"
                ],
                \"batchNumber\": 2,
                \"batchPauseOption\": \"Automatic\"
              }"
        ```

2.  View the execution details.

    When you run CLI commands to execute rolling update tasks, executions are automatically created in OOS. You can find the execution based on the returned execution ID to view the details about the execution, such as the execution results and output. In the following example, a script execution output is used to describe how to obtain the execution ID and view the execution details.

    1.  Find the execution ID of the rolling update task in the command output.

        The following figure shows an example execution ID.

        ![exec-id](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6724913061/p161172.png)

    2.  Run the following Alibaba Cloud CLI command to view the execution details:

        ```
        aliyun oos ListExecutions --ExecutionId exec-40e2e17ef7e04****
        ```

        The following figure shows the example execution details.

        ![exec-outputs](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7724913061/p161174.png)


## Execute rollback tasks to handle exceptions in rolling update tasks

If exceptions occur during rolling update tasks or you want to use previous configurations after rolling update tasks are executed, you can execute rollback tasks to restore the configurations of the ECS instances. Example commands are provided in this section to demonstrate how to roll back rolling update tasks that have been executed.

1.  Find the execution ID of the rolling update task in the command output.

    The following figure shows an example execution ID.

    ![exec-id](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6724913061/p161172.png)

2.  Run an Alibaba Cloud CLI command to execute a rollback task.

    For information about the OOS template parameters involved in the code, see [OOS template parameters](#section_gju_4ho_zbw).

    **Note:** When you execute a rollback task, OOS automatically finds ECS instances to be rolled back based on the rolling update task, and suspends or resumes scaling processes of the scaling group. Therefore, you may not need to specify some parameters.

    -   In the following example, a command for rolling back image update is used to roll the images of ECS instances in the scaling group back to CentOS 7.8 64-bit.

        ```
        aliyun oos StartExecution --TemplateName ACS-ESS-RollingUpdateByReplaceSystemDiskInScalingGroup --Parameters "{
                \"invokeType\": \"rollback\",
                \"scalingGroupId\": \"asg-bp18p2yfxow2dloq****\",
                \"scalingConfigurationId\": \"asc-bp1bx8mzur534edp****\",
                \"sourceImageId\": \"centos_7_8_x64_20G_alibase_20200717.vhd\",
                \"sourceExecutionId\": \"exec-83dba59be77d430****\",
                \"OOSAssumeRole\": \"\",
                \"batchNumber\": 2,
                \"batchPauseOption\": \"Automatic\"
              }"
        ```

    -   In the following example, a command for rolling back script execution is used to execute the rollback script in the ECS instances. The df -h and ifconfig shell commands are still used here. You can change the script based on your configurations.

        ```
        aliyun oos StartExecution --TemplateName ACS-ESS-RollingUpdateByRunCommandInScalingGroup --Parameters "{
                \"invokeType\": \"rollback\",
                \"commandType\": \"RunShellScript\",
                \"rollbackScript\": \"df -h\nifconfig\",
                \"scalingGroupId\": \"asg-bp18p2yfxow2dloq****\",
                \"sourceExecutionId\": \"exec-40e2e17ef7e046****\",
                \"OOSAssumeRole\": \"\",
                \"batchNumber\": 2,
                \"batchPauseOption\": \"Automatic\"
              }"
        ```

    -   In the following example, a command for rolling back OOS package installation is used to install the previous version of the WordPress package that is created in OOS for the ECS instances in the scaling group.

        ```
        aliyun oos StartExecution --TemplateName ACS-ESS-RollingUpdateByConfigureOOSPackage --Parameters "{
                \"invokeType\": \"rollback\",
                \"scalingGroupId\": \"asg-bp18p2yfxow2dloq****\",
                \"packageVersion\": \"v3\",
                \"packageName\": \"wordpress\",
                \"sourceExecutionId\": \"exec-f4e61f2f21fe490****\",
                \"OOSAssumeRole\": \"\",
                \"batchNumber\": 2,
                \"batchPauseOption\": \"Automatic\"
              }"
        ```

3.  View the execution details.

    When you run CLI commands to execute a rollback task, executions are also automatically created in OOS. You can also use the methods in Step 3 to view the details of an execution, such as the execution results and output.


## OOS template parameters

The following tables list the parameters of the OOS public templates used in the preceding examples.

|Parameter|Description|
|---------|-----------|
|invokeType|The type of the task. Valid values:-   invoke: rolling update task
-   rollback: rollback task |
|scalingGroupId|The ID of the scaling group in which the task is to be executed.|
|scalingConfigurationId|The ID of the active scaling configuration in the scaling group.|
|imageId|The ID of the image used to replace the original image.|
|sourceImageId|The ID of the image used for the rollback task.|
|OOSAssumeRole|The RAM role used to execute the task. Default value: OOSServiceRole.|
|enterProcess|The scaling process that is suspended before the task is executed.|
|exitProcess|The scaling process that is resumed when the task is complete.|
|batchNumber|The number of batches in which the ECS instances in the scaling group are divided. The task is executed in these batches. Each batch contains at least one ECS instance.|
|batchPauseOption|Specifies whether and how to suspend the task. Valid values:-   Automatic: The task is not suspended but is complete one time.
-   FirstBatchPause: The task is suspended when the first batch of executions are complete.
-   EveryBatchPause: The task is suspended when each batch of executions are complete. |
|sourceExecutionId|The execution ID of the source rolling update task when a rollback task is executed.|

**Note:** You can log on to the OOS console to view more parameter descriptions. For example, to view the parameter descriptions for the China \(Hangzhou\) region, see [ACS-ESS-RollingUpdateByReplaceSystemDiskInScalingGroup](https://oos.console.aliyun.com/cn-hangzhou/template/public/detail/ACS-ESS-RollingUpdateByReplaceSystemDiskInScalingGroup).

|Parameter|Description|
|---------|-----------|
|invokeType|The type of the task. Valid values:-   invoke: rolling update task
-   rollback: rollback task |
|scalingGroupId|The ID of the scaling group in which the task is to be executed.|
|commandType|The type of the script to be executed. The value of RunShellScript indicates a shell script.|
|invokeScript|The script that is executed on ECS instances during a rolling update task.|
|rollbackScript|The script that is executed on ECS instances during a rollback task.|
|OOSAssumeRole|The RAM role used to execute the task. Default value: OOSServiceRole.|
|enterProcess|The scaling process that is suspended before the task is executed.|
|exitProcess|The scaling process that is resumed when the task is complete.|
|batchNumber|The number of batches in which the ECS instances in the scaling group are divided. The task is executed in these batches. Each batch contains at least one ECS instance.|
|batchPauseOption|Specifies whether and how to suspend the task. Valid values:-   Automatic: The task is not suspended but is complete one time.
-   FirstBatchPause: The task is suspended when the first batch of executions are complete.
-   EveryBatchPause: The task is suspended when each batch of executions are complete. |
|sourceExecutionId|The execution ID of the source rolling update task when a rollback task is executed.|

**Note:** You can log on to the OOS console to view more parameter descriptions. For example, to view the parameter descriptions for the China \(Hangzhou\) region, see [ACS-ESS-RollingUpdateByRunCommandInScalingGroup](https://oos.console.aliyun.com/cn-hangzhou/template/public/detail/ACS-ESS-RollingUpdateByRunCommandInScalingGroup).

|Parameter|Description|
|---------|-----------|
|invokeType|The type of the task. Valid values:-   invoke: rolling update task
-   rollback: rollback task |
|scalingGroupId|The ID of the scaling group in which the task is to be executed.|
|packageName|The name of the software package.|
|packageVersion|The version of the software package.|
|action|The action to be taken on the software package. Valid values:-   install
-   uninstall |
|OOSAssumeRole|The RAM role used to execute the task. Default value: OOSServiceRole.|
|enterProcess|The scaling process that is suspended before the task is executed.|
|exitProcess|The scaling process that is resumed when the task is complete.|
|batchNumber|The number of batches in which the ECS instances in the scaling group are divided. The task is executed in these batches. Each batch contains at least one ECS instance.|
|batchPauseOption|Specifies whether and how to suspend the task. Valid values:-   Automatic: The task is not suspended but is complete one time.
-   FirstBatchPause: The task is suspended when the first batch of executions are complete.
-   EveryBatchPause: The task is suspended when each batch of executions are complete. |
|sourceExecutionId|The execution ID of the source rolling update task when a rollback task is executed.|

**Note:** You can log on to the OOS console to view more parameter descriptions. For example, to view the parameter descriptions for the China \(Hangzhou\) region, see [ACS-ESS-RollingUpdateByConfigureOOSPackage](https://oos.console.aliyun.com/cn-hangzhou/template/public/detail/ACS-ESS-RollingUpdateByConfigureOOSPackage).

