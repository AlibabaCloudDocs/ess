# View ECS instances

This topic describes how to view ECS instances that have been added to a scaling group.

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the top navigation bar, select a region.

3.  Find the target scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   Click **Manage** in the **Actions** column.
4.  In the left-side navigation pane, click **ECS Instances**.

    -   The **Auto Created** tab shows ECS instances that are automatically created by Auto Scaling. You can change the status of an instance, remove it from the scaling group, or release it. If an automatically created instance is considered unhealthy, it will be removed from the scaling group and released.
    -   The **Manually Added** tab shows ECS instances that are manually added. You can change the status of an instance or remove it from the scaling group. If a manually added instance is not in the **Running** state, the instance is considered unhealthy and will be removed from the scaling group. Whether manually added ECS instances are released when they are removed from a scaling group depends on their management mode:
        -   If the lifecycle of the instances is not managed by the scaling group, the instances are removed from the scaling group but not released.
        -   If the lifecycle of the instances is managed by the scaling group, the instances are removed from the scaling group and released.

**References**  


[Move ECS instance to Standby](/intl.en-US/Instance Management/ECS instance/Switch an ECS instance to the Standby state.md)

[Switch to the protected state for an ECS instance](/intl.en-US/Instance Management/ECS instance/Switch an ECS instance to the Protected state.md)

[Remove from the protected state for an ECS instance](/intl.en-US/Instance Management/ECS instance/Remove an ECS instance from the Protected state.md)

[Add ECS instances](/intl.en-US/Instance Management/ECS instance/Manually add an ECS instance to a scaling group.md)

[Remove an ECS instance](/intl.en-US/Instance Management/ECS instance/Manually remove an ECS instance from a scaling group.md)

