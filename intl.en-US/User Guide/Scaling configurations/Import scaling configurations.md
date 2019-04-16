# Import scaling configurations {#task_dr2_pf4_qfb .task}

You can import a scaling configuration file to a scaling group to improve the efficiency of creating scaling configurations. However, the network type must be the same for both the source scaling group and the target scaling group.

1.  Log on to the [Auto Scaling Console](https://essnew.console.aliyun.com/). 
2.  On the Scaling Groups page, click **Manage** in the **Actions** column. 
3.  In the left-side navigation pane, select Instance Configuration Source. 
4.  On the **Scaling Configurations** tab, click **Import**. 
5.  Click **Select File** to select a .csv file to be imported. 
6.  In the Preview area, select the required scaling configuration, and click **Import**. 

    **Note:** 

    -   You can add a suffix to the name of an imported scaling configuration to avoid duplicate names.
    -   If you cannot select a scaling configuration in the **Preview** area, the network type of the target scaling group may be different from that of the source scaling group.
7.  View the importing result, and click **OK**. 

