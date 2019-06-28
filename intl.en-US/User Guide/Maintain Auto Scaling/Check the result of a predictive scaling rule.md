# Check the result of a predictive scaling rule {#task_266608 .task}

You can check whether the result calculated based on a predictive scaling rule meets your expectation.

1.  Log on to the [Auto Scaling console](https://partners-intl.console.aliyun.com/#/ess).
2.  On the Scaling Groups page, locate the row that contains the target scaling group and click **Manage** in the **Actions** column.
3.  In the left-side navigation pane, click Scaling Rules. On the page that appears, locate the row that contains the target predictive scaling rule and click **View Details** in the **Actions** column. 

    The Rule Details page shows multiple metrics to help you understand the predicted result. You can enable **Forecast and Scale** after confirming that the predicted result meets your expectations. For more information about the operation, see [Modify a predictive scaling rule](reseller.en-US/User Guide/Maintain Auto Scaling/Modify a scaling rule.md#).

    -   Compare the actual and predicted CPU usage to evaluate the forecast accuracy.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/220366/156171700447840_en-US.png)

    -   Compare the actual and predicted number of ECS instances to evaluate the forecast accuracy.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/220366/156171700447841_en-US.png)

    -   Check whether the execution results of the scheduled plans generated from forecast meet your expectations.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/220366/156171700447842_en-US.png)


If you have enabled **Forecast and Scale**, the system automatically creates forecast tasks for the predictive scaling rule based on the scheduled plans generated from forecast. Forecast tasks are scheduled tasks. You can view details about forecast tasks on the Scheduled Tasks page. These tasks are named in the following format: PredictiveScaling-Scaling rule name-Execution time.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/220366/156171700447843_en-US.png)

Forecast tasks change the boundary values of the scaling group and are deleted after being successfully executed. You can view details about forecast tasks on the Scaling Activities page.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/220366/156171700447844_en-US.png)

