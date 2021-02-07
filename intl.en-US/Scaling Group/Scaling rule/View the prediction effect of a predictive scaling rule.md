# View the prediction effect of a predictive scaling rule

You can check whether the prediction based on a predictive scaling rule meets your expectations.

1.  Log on to the [Auto Scaling console](https://essnew.console.aliyun.com/).

2.  In the left-side navigation pane, click **Scaling Groups**.

3.  In the top navigation bar, select a region.

4.  Find the scaling group and use one of the following methods to open the details page of the scaling group:

    -   Click the ID of the scaling group in the **Scaling Group Name/ID** column.
    -   Click **Details** in the **Actions** column.
5.  In the upper part of the page, click the **Scaling Rules** tab.

6.  Find the predictive scaling rule and click its ID in the Scaling Rule ID/Name column.

    The scaling rule details page shows multiple metrics to help you evaluate the prediction. You can enable **Predict and Scale** after you confirm that the prediction meets your expectations. For more information, see [Modify a scaling rule](/intl.en-US/Scaling Group/Scaling rule/Modify a scaling rule.md).

    -   Compare the actual and predicted CPU utilization to evaluate the prediction accuracy.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0678449951/p47840.png)

    -   Compare the actual and predicted numbers of ECS instances to evaluate the prediction accuracy.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0678449951/p47841.png)

    -   Check whether the scheduled plans generated from the prediction meet your expectations.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0678449951/p47842.png)


If **Predict and Scale** is enabled, Auto Scaling automatically creates scheduled tasks for the predictive scaling rule based on the scheduled plans generated from the prediction. You can view the details of the scheduled tasks on the Scheduled Tasks page. These tasks are named in the following format: PredictiveScaling-Scaling rule name-Execution time.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0678449951/p47843.png)

These scheduled tasks change the minimum and maximum numbers of ECS instances in the scaling group and are deleted after they are executed. You can view the details of the scaling activities triggered by these scheduled tasks on the Scaling Activities page.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0678449951/p47844.png)

