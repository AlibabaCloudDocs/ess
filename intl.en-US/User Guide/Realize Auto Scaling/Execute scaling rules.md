# Execute scaling rules {#concept_rxw_2bx_rfb .concept}

This section describes how to execute rules for manually or automatically scaling ECS instance resources.

## Prerequisites {#section_bpw_hbx_rfb .section}

Before you execute a scaling rule, the following prerequisites must be met:

-   The status of the scaling group where a scaling rule is located must be **Enabled**.
-   Any in-progress scaling activity is not allowed in a scaling group where the scaling rule is located.
-   The number of ECS instances is not limited in a scaling group. However, you still need to follow the [Usage restrictions for ECS instances](../../../../../reseller.en-US/Product Introduction/Limits.md#).

## Manually execute a scaling rule {#section_ovq_3cx_rfb .section}

If you must temporarily scale the resources of an ECS instance, you can manually execute a scaling rule.

**Note:** When no in-progress scaling activity exists in a scaling group, scaling activities that are triggered by manually executed scaling rules can be immediately run without following the specified [Cool-down time](reseller.en-US/User Guide/Usage notes/Cool-down time.md#).

1.  On the Scaling Rules page, click**Execute** in the **Actions**column.
2.  In the Run Scaling Rule dialog box, click **Confirm**.
3.  If a scaling rule is executed, a prompt appears in the upper-right corner of the page.

    ![](images/21704_en-US.png)

    If a scaling rule fails to be executed, an error appears.

    ![](images/21705_en-US.png)

4.  On the Scaling Activities page, you can view more details.

## Execute a scaling rule by a scheduled task {#section_qhr_lbx_rfb .section}

For businesses that frequently use ECS instance resources, you can select scheduled tasks. When [creating a scheduled task](reseller.en-US/User Guide/Scheduled tasks/Create a scheduled task.md#), you can specify a scaling rule. The scaling rule will be executed at the specified point in time.

![](images/21700_en-US.png)

## Execute a scaling rule by an event-triggered task {#section_rgw_fcx_rfb .section}

For businesses that infrequently use ECS instance resources, you can select event-triggered tasks. When [creating an event-triggered task](reseller.en-US/User Guide/Alarm tasks/Create event-triggered tasks.md#), you can specify a scaling rule. The scaling rule will be executed when the specified condition is met.

You can set either the System Monitoring type or the Custom Monitoring type for an event-triggered task to meet monitoring requirements in various scenarios. For more information, see the [Overview of event-triggered tasks](reseller.en-US/User Guide/Alarm tasks/Auto Scaling alarm tasks.md#).

![Execute scaling rules -  Configure event-triggered tasks with the System Monitoring type](images/21701_en-US.png)

![Execute scaling rules -  Configure event-triggered tasks with the Custom Monitoring type](images/21702_en-US.png)

