# Scaling activity status {#concept_d5r_gfn_qfb .concept}

This topic introduces the status of scaling activity in Auto Scaling.

A scaling activity is in the **Rejected** status if the request for execution is rejected.

A scaling activity is in the In **Progress** status if it is being executed.

After a scaling activity is completed, there are three possible states:

-   **Successful**\(`Successful`\): The scaling activity has successfully added or removed the ECS instances to or from the scaling group as specified by the MaxSize value or the MinSize value adjusted by the scaling rule.

    **Note:** When an ECS instance is successfully added to a scaling group, it has been created and added to the Server Load Balancer instance and the RDS access whitelist. If any of the above steps fail, the ECS instance is considered “failed”.

-   **Warning**\(`Warning`\): The scaling activity fails to add or remove at least one ECS instance to or from the scaling group as specified by the MaxSize value or the MinSize value adjusted by the scaling rule.
-   **Failed**\(`Failed`\): The scaling activity fails to add or remove any ECS instance to or from the scaling group as specified by the MaxSize value or the MinSize value adjusted by the scaling rule.

## Example {#section_pby_lhn_qfb .section}

A scaling rule is defined to be added five ECS instances. The existing Total Capacity of the scaling group is three ECS instances, and the MaxSize value is five ECS instances. When the scaling rule is executed, Auto Scaling adds only two ECS instances as specified by the MaxSize value. After the scaling activity is completed, there are three possible states:

-   **Successful**: Two ECS instances are created successfully and correctly added to the Sever Load Balancer instance and the RDS access whitelist.
-   **Warning**: Two ECS instances are created successfully, but only one is correctly added to the Sever Load Balancer instance and the RDS access whitelist. The other one failed, and is rolled back and released.
-   **Failed**: No ECS instances are created. Or two ECS instances are created successfully, but neither are added to the Server Load Balancer instance or the RDS access whitelist. Both are rolled back and released.

