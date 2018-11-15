# View a scaling configuration {#task406 .task}

Scaling configurations have two life cycle status. **Active**: The scaling group uses the scaling configuration in active status to create ECS instances. **Inactive**: Inactive scaling configurations are still in a scaling group, but are not used to create ECS instances. You can select a scale configuration according to your business needs. The scaling group automatically creates ECS instances only based on the Active scaling configuration.

The scaling configuration include much content, and you may forget the specific configuration items. Therefore, Auto Scaling also provides the function to view the details of the scaling configurations for you to learn each scaling configuration at any time, and to select a template for the ECS instance.

Follow these steps to view the details of a scaling configuration and select a scaling configuration:

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess), and click **Manage** in the **Actions** column after a scaling group. 
2.  Go to the Scale Configuration page, and click **View Details** in the **Actions** column after a specified scaling configuration. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40569/154227268432028_en-US.png)

3.  After you confirm the configuration, click **Select** to enable the scaling configuration. 

    **Note:** After you select a scaling configuration, the other scaling configurations are in the **Inactive** status.


After you select a scaling configuration, when the scale-up conditions are met, the corresponding scaling group automatically creates ECS instances based on this scaling configuration.

