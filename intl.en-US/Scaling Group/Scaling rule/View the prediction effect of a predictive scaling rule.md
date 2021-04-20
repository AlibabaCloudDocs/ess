# View the prediction effect of a predictive scaling rule

You can check whether the prediction based on a predictive scaling rule meets your expectations so that you can determine whether to make corresponding adjustments. For example, if the predictive mode of a predictive scaling rule is set to **Predict Only** and the prediction meets your expectations, you can set the predictive mode to **Predict and Scale**. This way, Auto Scaling can automatically adjust the minimum and maximum numbers of instances.

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Find the scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   In the **Actions** column corresponding to the scaling group, click **Details**.
5.  In the upper part of the page, click the **Scaling Rules** tab.

6.  Find the predictive scaling rule and click its ID in the **Scaling Rule ID/Name** column.

    You can set the predictive mode to **Predict and Scale** after you confirm that the prediction meets your expectations. For more information, see [Modify a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Modify a scaling rule.md).

    The scaling rule details page shows multiple metrics to help you evaluate the prediction effect.

    ![](../images/p47840.png "Actual and predicted CPU utilization")

    ![](../images/p47841.png "Actual and predicted numbers of ECS instances in the scaling group")

    ![](../images/p47842.png "Scheduled plans generated from the prediction")


If the predictive mode is set to **Predict and Scale**, Auto Scaling automatically creates scheduled tasks for the predictive scaling rule based on the scheduled plans generated from the prediction. You can view the details of the scheduled tasks on the **Scheduled Tasks** page. These tasks are named in the following format: PredictiveScaling-Scaling rule name-Execution time.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0678449951/p47843.png)

After the scheduled tasks are executed, the minimum and maximum numbers of instances in the scaling group are modified, and the system automatically deletes scheduled tasks that are successfully executed. You can view the details of the scaling activities triggered by these scheduled tasks on the **Scaling Activities** tab.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0678449951/p47844.png)

