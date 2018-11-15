# Remove an unhealthy ECS instance {#concept_wvk_thn_qfb .concept}

This topic introduces how to remove an unhealthy ECS instance.

After an ECS instance has been successfully added to a scaling group, the Auto Scaling service regularly scans its status. If the ECS instance is not in the **Running**\(`Running`\) status, Auto Scaling removes the ECS instance from the scaling group.

-   If the ECS instance was created automatically, Auto Scaling immediately removes and releases it.
-   If the ECS instance was added manually, Auto Scaling immediately removes it, but does not stop or release it.

The removal of unhealthy ECS instances is not restricted by the MinSize value. If, due to removal, the number of ECS instances \(Total Capacity\) in the scaling group is smaller than the MinSize value, Auto Scaling automatically adds ECS instances to the group until the number of instances reaches the MinSize value.

