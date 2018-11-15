# Scaling activity process {#concept_mz2_rdn_qfb .concept}

This topic introduces the scaling activity process.

A scaling activity’s lifecycle starts with determining the scaling group’s health status and boundary conditions and ends with enabling the cool-down time.

## Automatic scaling {#section_rv5_h2n_qfb .section}

**Scaling up**

1.  Determine the scaling group’s health status and boundary conditions.
2.  Allocate the activity ID and execute the scaling activity.
3.  Create ECS instances.
4.  Modify Total Capacity.
5.  Allocate IP addresses to the created ECS instances.
6.  Add the ECS instances to the RDS access whitelist.
7.  Launch the ECS instances.
8.  Attach the ECS instances to the Server Load Balancer and set the **weight** to 0. Wait 60s and then set the weight to 50.
9.  Complete the scaling activity, and enable the cool-down time.

**Scaling down**

1.  Determine the scaling group’s health status and boundary conditions.
2.  Allocate the activity ID and execute the scaling activity.
3.  The Server Load Balancer stops forwarding traffic to the ECS instances. Wait 60s and then remove the ECS instances from the Server Load Balancer.
4.  Disable the ECS instances.
5.  Remove the ECS instances from the RDS access whitelist.
6.  Release the ECS instances.
7.  Modify Total Capacity.
8.  Complete the scaling activity, and enable the cool-down time.

## Manually add or remove an existing ECS instance {#section_xkz_n2n_qfb .section}

**Manually add an existing ECS instance**

1.  Determine the scaling group’s health status and boundary conditions, and check the ECS instance’s status and type.
2.  Allocate the activity ID and execute the scaling activity.
3.  Add the ECS instance.
4.  Modify Total Capacity.
5.  Add the ECS instance to the RDS access whitelist.
6.  Attach the ECS instance to the Server Load Balancer and set the **weight** to 0. Wait 60ss and then set the weight to 50.
7.  Complete the scaling activity, and enable the cool-down time.

**Manually remove an existing instance**

1.  Determine the scaling group’s health status and boundary conditions.
2.  Allocate the activity ID and execute the scaling activity.
3.  The Server Load Balancer stops forwarding traffic to the ECS instance.
4.  Wait 60s and then remove the ECS instance from the Server Load Balancer.
5.  Remove the ECS instance from the RDS access whitelist.
6.  Modify Total Capacity.
7.  Remove the ECS instance from the scaling group.
8.  Complete the scaling activity, and enable the cool-down time.

