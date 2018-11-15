# Create a scaling configuration {#concept_25890_zh .concept}

This topic describes how to create a scaling configuration.

The process of creating a scaling configuration is similar to creating an ECS instance, but some configuration items are not supported, such as region. Follow the console to perform operations. Each configuration on the page is provided with a brief description. For more information about the meaning and usage, see [create an instance by using the wizard](../../../../reseller.en-US/User Guide/Instances/Create an instance/Create an instance by using the wizard.md#).

Follow these steps to create a scaling configuration:

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess), and click **Manage** in the **Actions** column.
2.  Go to the Scaling Configuration page, and click **Create Scaling Configuration**.
3.  On the Basic Configuration page, configure the billing method, instance, image, storage, public network bandwidth, and security group, and then click **Next: System Configuration**.

    **Note:** Auto Scaling only supports [Pay-As-You-Go instances](../../../../reseller.en-US/Pricing/Pay-As-You-Go.md#) and [preemptible instances](../../../../reseller.en-US/Product Introduction/Instances/Preemptible instance.md#), and only public images, custom images, and shared images are supported.

4.  On the System Configuration page, configure the tab \(optional\), logon credential, instance name \(optional\), and advanced options \(optional\), and then click **Confirm**.

    **Note:** Advanced options include instance RAM roles and user-defined data. You can configure the advanced options only for VPC-connected scaling groups.

5.  On the Confirm page, check the selected configurations, enter the scaling configuration names, and then click **Create**.
6.  In the Created successfully dialog box, click **Enable Configuration**. If you do not want to use the scaling configuration now, you can close the dialog box.

After successful creation, you can view and select the scaling configurations in the scaling configuration list.

