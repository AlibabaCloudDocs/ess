# Set rules for generating sequential and unique hostnames

This topic describes how to set rules for hostnames in a scaling configuration to generate sequential and unique hostnames for ECS instances during scale-out events. This helps you manage ECS instances in a more efficient manner.

Auto Scaling can create one or more ECS instances during a single scale-out event in a scaling group based on scaling rules. Auto Scaling can also create multiple ECS instances during multiple scale-out events. You can use one of the following methods to set rules for hostnames in a scaling configuration or launch template:

-   If you want to make the hostnames of ECS instances in a scaling group sequential and unique, you must set rules for the hostnames in a scaling configuration instead of in a launch template. For more information, see [\(Recommended\) Sorting at a fixed-value increment](#section_176_bta_c6q) and [Dynamic sorting based on extended sequential values](#section_05e_tib_3s5).

    **Note:** The hostnames of ECS instances in a scaling group are sequentially generated but not necessarily consecutive. For example, the hostnames of created ECS instances in a scaling group are ess-node-0999, ess-node-1000, and ess-node-1002. This indicates that the ess-node-1001 ECS instance fails to start normally. Auto Scaling considers this instance unhealthy, removes it from the scaling group, and then creates another instance whose hostname is ess-node-1002.

-   If you want to make the hostnames of only ECS instances that are created during a single scale-out event sequential and unique, you can set the hostnames based on the specified sorting rule. For more information, see [Batch configure sequential names or hostnames for multiple instances](/intl.en-US/Best Practices/Batch configure sequential names or hostnames for multiple instances.md).
-   If you have no naming requirements for hostnames, you can use regular hostnames without the need to set hostnames based on the preceding rules. For example, if you set the hostname to hostname for a scaling group, the hostnames of all created ECS instances in the scaling group are hostname.

In this topic, two example scenarios are used to describe how to set rules for generating sequential and unique hostnames by using the Auto Scaling console and by calling API operations.

## Scenario 1: Set sequential and unique hostnames in the console

1.  Create a scaling group.

    For more information, see [Create a scaling group](/intl.en-US/Scaling Group/Scaling group/Create a scaling group.md).

2.  Create a scaling configuration and enable it.

    In the **System Configurations \(Optional\)** step, specify the naming convention in the **Host** section. In this example, enter ess-node-\(AUTO\_INCREMENT\)\[0,3\]-ecshost.

    **Note:** In this example, the naming convention specifies to increment the hostname by a fixed value for each created ECS instance. For more information, see [\(Recommended\) Sorting at a fixed-value increment](#section_176_bta_c6q).

    For more information, see [Create a scaling configuration](/intl.en-US/Scaling Group/Instance Configuration Source/Create a scaling configuration.md).

3.  Enable the scaling group.

    For more information, see [Enable a scaling group](/intl.en-US/Scaling Group/Scaling group/Enable a scaling group.md).

4.  Create and manually execute a scaling rule.

    1.  Create a scaling rule. For more information, see [Create a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Create a scaling rule.md).

        In this example, set Rule Type to Simple Scaling Rule and Operation to Add 3 Instances.

    2.  Manually execute the scaling rule. For more information, see [Execute a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Execute a scaling rule.md).

        After the scaling rule is executed, the hostnames of the three ECS instances are displayed as ess-node-000-ecshost, ess-node-001-ecshost, and ess-node-002-ecshost.


## Scenario 2: Set sequential and unique hostnames by calling API operations

1.  Call the [CreateScalingGroup](/intl.en-US/API Reference/Scaling group/CreateScalingGroup.md) operation to create a scaling group.

2.  Call the [CreateScalingConfiguration](/intl.en-US/API Reference/Scaling configuration/CreateScalingConfiguration.md) operation to create a scaling configuration.

    Set the HostName parameter to ess-node-\(AUTO\_INCREMENT\)\[0,3\]-ecshost.

    **Note:** In this example, the naming convention specifies to increment the hostname by a fixed value for each created ECS instance. For more information, see [\(Recommended\) Sorting at a fixed-value increment](#section_176_bta_c6q).

3.  Call the [EnableScalingGroup](/intl.en-US/API Reference/Scaling group/EnableScalingGroup.md) operation to enable the scaling group.

4.  Create and manually execute a scaling rule.

    1.  Call the [CreateScalingRule](/intl.en-US/API Reference/Scaling rule/CreateScalingRule.md) operation to create a scaling rule.

        In this example, a simple scaling rule is created to add three ECS instances.

    2.  Call the [ExecuteScalingRule](/intl.en-US/API Reference/Trigger task/ExecuteScalingRule.md) operation to execute the scaling rule.

        After the scaling rule is executed, the hostnames of the three ECS instances are displayed as ess-node-000-ecshost, ess-node-001-ecshost, and ess-node-002-ecshost.


## \(Recommended\) Sorting at a fixed-value increment

Hostnames are in the name\_prefix\(AUTO\_INCREMENT\)\[begin\_number,bits\]name\_suffix format.

|Segment|Required|Description|Example|
|-------|--------|-----------|-------|
|name\_prefix|Yes|The prefix of the hostname.|ess-node-|
|\(AUTO\_INCREMENT\)|Yes|The fixed value used to indicate the sorting method.|\(AUTO\_INCREMENT\)|
|\[begin\_number,bits\]|Yes|The sequential value of the hostname. After this segment is specified, the sequential values of hostnames are incremented. **Note:** By default, the system sequentially increments the values. If a created ECS instance in a scaling group cannot be started, Auto Scaling removes the instance from the scaling group and creates another instance. Therefore, the hostnames of ECS instances in the scaling group may not be consecutively incremented.

-   begin\_number: the start value of the sequential value. Valid values: 0 to 999999.
    -   When Auto Scaling creates instances in a scaling group for the first time, the start value that you specified takes effect. If the start value is not specified, 0 is used.
    -   When Auto Scaling creates instances in a scaling group not for the first time, the start value increments starting from the maximum sequential value of existing hostnames in the scaling group.
-   bits: the number of digits of the sequential value. Valid values: 1 to 6. Default value: 6.

**Note:** We recommend that you set bits to at least 3. Otherwise, the upper limit of the sequential values may be reached in a short period of time. If Auto Scaling needs to create more ECS instances after the upper limit is reached, an error is reported and the scale-out event is suspended. In this case, you must set the rules for generating hostnames again.

The \[begin\_number,bits\] segment cannot contain spaces. By default, when the number of digits of the specified begin\_number value is greater than the bits value, bits is set to 6.

|\[0,6\]|
|name\_suffix|No|The suffix of the instance name or hostname.|-ecshost|

|Example|Existing hostname with the maximum sequential value in a scaling group|Hostname \(three created ECS instances\)|Description|
|-------|----------------------------------------------------------------------|----------------------------------------|-----------|
|ess-node-\(AUTO\_INCREMENT\)\[0,3\]-ecshost|N/A|ess-node-000-ecshost, ess-node-001-ecshost, and ess-node-002-ecshost.|The number of digits of all sequential values is the bits value. When Auto Scaling creates instances in a scaling group for the first time, the sequential value starts from the begin\_number value and sequentially increments based on the number of created instances.|
|-   ess-node-\(AUTO\_INCREMENT\)\[\]-ecshost
-   ess-node-\(AUTO\_INCREMENT\)\[,\]-ecshost

|N/A|ess-node-000000-ecshost, ess-node-000001-ecshost, and ess-node-000002-ecshost.|If begin\_number is not specified, begin\_number is set to 0. If bits is not specified, bits is set to 6.|
|ess-node-\(AUTO\_INCREMENT\)\[99,1\]-ecshost|ess-node-000099-ecshost|ess-node-000100-ecshost, ess-node-000101-ecshost, and ess-node-000102-ecshost.|-   When Auto Scaling creates instances in a scaling group not for the first time, the sequential value increments starting from the maximum sequential value of existing hostnames in the scaling group.
-   By default, when the number of digits of the specified begin\_number value is greater than the bits value, bits is set to 6. |
|ess-node-\(AUTO\_INCREMENT\)\[0,2\]-ecshost|ess-node-99-ecshost|An error is reported and the scale-out event is suspended.|-   When Auto Scaling creates instances in a scaling group not for the first time, the sequential value increments starting from the maximum sequential value of existing hostnames in the scaling group.
-   If Auto Scaling needs to create more ECS instances after the upper limit is reached, an error is reported and the scale-out event is suspended. In this case, you must set the rules for generating hostnames again. |
|ess-node-\(AUTO\_INCREMENT\)\[0,4\]|ess-node-0998-ecshost|ess-node-0999, ess-node-1000, and ess-node-1002.|-   When Auto Scaling creates instances in a scaling group not for the first time, the sequential value increments starting from the maximum sequential value of existing hostnames in the scaling group.
-   By default, the system sequentially increments the values. If a created ECS instance in a scaling group cannot be started, Auto Scaling removes the instance from the scaling group and creates another instance. Therefore, the hostnames of ECS instances in the scaling group may not be consecutively incremented. In this example, the hostname of the ECS instance that fails to start is ess-node-1001. |

## Dynamic sorting based on extended sequential values

Hostnames are in the name\_prefix\(ess\_extend\_begin,ess\_extend\_bits\)\[begin\_number,bits\]name\_suffix format.

|Segment|Required|Description|Example|
|-------|--------|-----------|-------|
|name\_prefix|Yes|The prefix of the hostname.|ess-node-|
|\(ess\_extend\_begin,ess\_extend\_bits\)|Yes|The extended sequential value of the hostname. When the base sequential value of existing hostnames in a scaling group is equal to the maximum sequential value, one value is added to the extended sequential value. Then, the base sequential value increments from 0 again until the upper limit is reached. -   ess\_extend\_begin: the start value of the extended sequential value. Valid values: 0 to ZZZ. Each valid value ranges from 0 to 9, a to z, and A to Z. For example, if one value is added to 9, a is obtained. If one value is added to z, A is obtained.
    -   When Auto Scaling creates instances in a scaling group for the first time, the start value that you specified takes effect. If the start value is not specified, 0 is used.
    -   When Auto Scaling creates instances in a scaling group not for the first time, the start value increments starting from the maximum sequential value of existing hostnames in the scaling group.
-   ess\_extend\_bits: the number of digits of the extended sequential value. Valid values: 1 to 3. Default value: 3.

**Note:** If Auto Scaling needs to create more ECS instances after the upper limits of extended sequential values and base sequential values are both reached, an error is reported and the scale-out event is suspended. In this case, you must set the rules for generating hostnames again.

The \(ess\_extend\_begin,ess\_extend\_bits\) segment cannot contain spaces. By default, when the number of digits of the specified ess\_extend\_begin value is greater than the bits value, bits is set to 3.

|\(0,3\)|
|\[begin\_number,bits\]|Yes|The base sequential value of the hostname. After this segment is specified, the base sequential values of hostnames are incremented to the maximum value. Then, one value is added to the extended sequential value and the base sequential value increments from 0 again until the upper limit is reached. **Note:** By default, the system sequentially increments the values. If a created ECS instance in a scaling group cannot be started, Auto Scaling removes the instance from the scaling group and creates another instance. Therefore, the hostnames of ECS instances in the scaling group may not be consecutively incremented.

-   begin\_number: the start value of the base sequential value. Valid values: 0 to 999999.
    -   When Auto Scaling creates instances in a scaling group for the first time, the start value that you specified takes effect. If the start value is not specified, 0 is used.
    -   When Auto Scaling creates instances in a scaling group not for the first time, the start value increments starting from the maximum sequential value of existing hostnames in the scaling group.
-   bits: the number of digits of the base sequential value. Valid values: 1 to 6. Default value: 6.

**Note:**

-   When the sum of the maximum base sequential value of existing hostnames and the number of instances to be created in a scaling group is greater than or equal to the maximum base sequential value, the hostnames of instances in the scaling group may not be consecutively incremented. To ensure that the hostnames of ECS instances in the scaling group are consecutively incremented, we recommend that you set the number of digits of base sequential values to at least 3.
-   If Auto Scaling needs to create more ECS instances after the upper limits of extended sequential values and base sequential values are both reached, an error is reported and the scale-out event is suspended. In this case, you must set the rules for generating hostnames again.

The \[begin\_number,bits\] segment cannot contain spaces. By default, when the number of digits of the specified begin\_number value is greater than the bits value, bits is set to 6.

|\[0,6\]|
|name\_suffix|No|The suffix of the instance name or hostname.|-ecshost|

|Example|Existing hostname with the maximum sequential value in a scaling group|Hostname \(three created ECS instances\)|Description|
|-------|----------------------------------------------------------------------|----------------------------------------|-----------|
|ess-node-\(0,3\)\[0,3\]-ecshost|N/A|ess-node-000000-ecshost, ess-node-000001-ecshost, and ess-node-000002-ecshost.|When Auto Scaling creates instances in a scaling group for the first time, the sequential values for hostnames of the instances are set based on the following rules:-   Extended sequential value: The number of digits of all extended sequential values is the ess\_extend\_bits value. The start value of all extended sequential values is the ess\_extend\_begin value. If the base sequential value reaches the maximum value, one value is added to the extended sequential value and the base sequential value increments from 0 again.
-   Base sequential value: The number of digits of all base sequential values is the bits value. The start value of all base sequential values is the begin\_number value. The base sequential value is incremented based on the number of ECS instances to be created. If the base sequential value reaches the maximum value, one value is added to the extended sequential value and the base sequential value increments from 0 again. |
|-   ess-node-\(\)\[\]-ecshost
-   ess-node-\(,\)\[,\]-ecshost

|N/A|ess-node-000000000-ecshost, ess-node-000000001-ecshost, and ess-node-000000002-ecshost.|-   Extended sequential value: If ess\_extend\_begin is not specified, ess\_extend\_begin is set to 0. If ess\_extend\_bits is not specified, ess\_extend\_bits is set to 3.
-   Base sequential value: If begin\_number is not specified, begin\_number is set to 0. If bits is not specified, bits is set to 6. |
|ess-node-\(0,1\)\[0,1\]-ecshost|ess-node-08-ecshost|ess-node-10-ecshost, ess-node-11-ecshost, and ess-node-12-ecshost.|-   When Auto Scaling creates instances in a scaling group not for the first time, the base sequential value increments starting from the maximum sequential value of existing hostnames in the scaling group.
-   When the sum of the maximum base sequential value of existing hostnames and the number of instances to be created in a scaling group is greater than or equal to the maximum base sequential value, the hostnames of instances in the scaling group may not be consecutively incremented. To ensure that the hostnames of ECS instances in the scaling group are consecutively incremented, we recommend that you set the number of digits of base sequential values to at least 3. |
|ess-node-\(0,1\)\[0,1\]-ecshost|ess-node-Z9-ecshost|An error is reported and the scale-out event is suspended.|-   When Auto Scaling creates instances in a scaling group not for the first time, the base sequential value increments starting from the maximum sequential value of existing hostnames in the scaling group.
-   If Auto Scaling needs to create more ECS instances after the upper limits of extended sequential values and base sequential values are both reached, an error is reported and the scale-out event is suspended. In this case, you must set the rules for generating hostnames again. |
|ess-node-\(0,1\)\[0,3\]|ess-node-0099-ecshost|ess-node-0100, ess-node-0101, and ess-node-0103.|-   When Auto Scaling creates instances in a scaling group not for the first time, the base sequential value increments starting from the maximum sequential value of existing hostnames in the scaling group.
-   By default, the system sequentially increments the values. If a created ECS instance in a scaling group cannot be started, Auto Scaling removes the instance from the scaling group and creates another instance. Therefore, the hostnames of ECS instances in the scaling group may not be consecutively incremented. In this example, the hostname of the ECS instance that fails to start is ess-node-0102. |
|ess-node-\(0,1\)\[99,1\]-ecshost|ess-node-0000099-ecshost|ess-node-0000100-ecshost, ess-node-0000101-ecshost, and ess-node-0000102-ecshost.|-   When Auto Scaling creates instances in a scaling group not for the first time, the base sequential value increments starting from the maximum sequential value of existing hostnames in the scaling group.
-   By default, when the number of digits of the specified begin\_number value is greater than the bits value, bits is set to 6. |

