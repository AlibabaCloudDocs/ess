# Disable a scaling group

This topic describes how to disable a scaling group that is no longer needed.

The scaling group is in the **Enabled** state.

If a scaling activity is being executed when you disable the scaling group, the scaling activity continues until it is complete. Scaling requests that are made after the scaling group is disabled are rejected.

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Find the scaling group and choose ![more](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0570524161/p166432.png) \> **Disable** in the **Actions** column.

5.  In the **Disable Scaling Group** message, click **OK**.

    The scaling group enters the **Disabled** state.


**Related topics**  


[DisableScalingGroup](/intl.en-US/API Reference/Scaling group/DisableScalingGroup.md)

