# Delete a scaling group

This topic describes how to delete a scaling group that is no longer needed.

If you delete a scaling group, its scaling configurations and scaling rules are also deleted. If ECS instances in the scaling group are in the Running state, Auto Scaling first stops the ECS instances. Then, Auto Scaling removes all the manually added ECS instances and releases all the automatically added ECS instances.

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Find the scaling group and click **Delete** in the **Actions** column.

5.  In the message that appears, click **OK**.


The scaling group enters the **Deleting** state. After the scaling group is deleted, it is no longer displayed on the Scaling Groups page.

