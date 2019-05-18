# View scaling activities {#concept_tn5_4c2_sfb .concept}

You can view scaling activities in Auto Scaling, to understand the results of the activities triggered by various means, such as scheduled tasks and alarm tasks. This topic describes how to view scaling activities.

## Procedure {#section_nhb_sc2_sfb .section}

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  On the Scaling Groups page, click **Manage** in the **Actions** column corresponding to the scaling group to be viewed.
3.  In the left-side navigation pane of the displayed page, click **Scaling Activities**.

    **Note:** You can query information about scaling activities executed within the last 30 days.

4.  Click **View Details** in the **Actions** column corresponding to a scaling activity to view more information.

    **Note:** To troubleshoot a scaling activity in the **Failed** or **Rejected** state, see [Troubleshoot scaling activity exceptions](reseller.en-US/.md#).

    ![](images/21824_en-US.png)


You can also call [DescribeScalingActivities](../../../../reseller.en-US/API-Reference/Scaling group/DescribeScalingActivities.md#) to view scaling activities.

