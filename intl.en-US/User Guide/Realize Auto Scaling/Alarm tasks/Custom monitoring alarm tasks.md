# Custom monitoring alarm tasks {#concept_rx4_xbd_sfb .concept}

This topic introduces custom monitoring alarm tasks in Auto Scaling.

The monitored objects of a custom monitoring alarm task are the metrics that you choose to be reported to CloudMonitor. In some scenarios, system metrics may not contain the metrics you need. You may have your own monitoring system and be concerned with some metrics related to your specific business. By using custom monitoring alarm tasks, you can import custom metrics specific to your business from your own monitoring system to CloudMonitor to create alarm tasks.

Custom monitoring alarm tasks in Auto Scaling are associated with custom metrics in Alibaba Cloud CloudMonitor. Therefore, you must report custom monitoring data \(custom metrics\) to CloudMonitor before you can use custom monitoring alarm tasks. CloudMonitor custom monitoring is a service that allows you to define metrics and alarm rules as needed. With this service, you can monitor target metrics, report collected monitoring data to CloudMonitor for processing, and set alarm rules for these metrics.

## Report monitoring data to CloudMonitor {#section_j22_1cd_sfb .section}

CloudMonitor custom monitoring allows you to report monitoring data. You can report time-series data that you have collected to CloudMonitor. The reported data is called a time sequence. CloudMonitor allows you to report data through open APIs, Java SDKs, and the Alibaba Cloud command line interface \(CLI\). The following section describes how to report monitoring data by using Java SDKs. For more information, see [Report monitoring data](../../../../reseller.en-US/User Guide/Custom monitoring/Report monitoring data.md#).

Before using a Java SDK, you must import the JAR file containing the SDK to a project. If you use Apache Maven to manage a project, you only need to add the following dependency to the project:

``` {#codeblock_vhx_mkm_okd}
<dependency> 
    <groupId>com.aliyun</groupId> 
    <artifactId>aliyun-java-sdk-core</artifactId> 
    <version>3.2.6</version>
</dependency> 
<dependency> 
    <groupId>com.aliyun.openservices</groupId> 
    <artifactId>aliyun-cms</artifactId>
    <version>0.2.4</version>
</dependency> 
```

You can run the following commands to report custom metrics to CloudMonitor:

``` {#codeblock_pl6_4ce_ieg}
static String endPoint     = "https://metrichub-cms-cn-hangzhou.aliyuncs.com";
CMSClient cmsClient = new CMSClient(endPoint, accAutoScalingKey, accAutoScalingSecret);
CustomMetricUploadRequest request = CustomMetricUploadRequest.builder()
                    .append(CustomMetric.builder()
                    .setMetricName("myCustomMetric")//Set the custom metric name.
                    .setGroupId(54504L)//Set the group ID.
                    . Settime (new date () //Set the time.
                    .setType(CustomMetric.TYPE_VALUE)//Set the type to original value.
                    .appendValue(MetricAttribute.VALUE, number)//Add an original value. The key must be original values.
                    .appendDimension("key1", "value1")//Add a dimension.
                    .appendDimension("key2","value2")
                    .build())
                 .build();
            CustomMetricUploadResponse response = cmsClient.putCustomMetric(request);//Report data.
```

The preceding example shows how to report a metric to CloudMonitor. When reporting a metric, you must specify the groupId parameter that represents the application group in CloudMonitor. The application group can be a group that you have created in CloudMonitor or a group that does not exist. You can create application groups and view their details on the **Application Groups** page of the [CloudMonitor Console](https://partners-intl.console.aliyun.com/#/cms). The reported custom metrics \(also called time sequences\) are displayed on the **Custom Monitoring** page.

We recommend that you push custom monitoring data to an existing application group in CloudMonitor to increase the flexibility of CloudMonitor and other functions. An application group in CloudMonitor is a logical group of multiple cloud services. You can also choose to push data to any group regardless of existing groups.

CloudMonitor automatically aggregates reported monitoring data. If you need to report large amounts of data to CloudMonitor, you can also aggregate the data locally before reporting it. For more information, see [Report monitoring data](../../../../reseller.en-US/User Guide/Custom monitoring/Report monitoring data.md#).

## Limits {#section_psb_ycd_sfb .section}

CloudMonitor has the following limits on user-reported monitoring data:

-   The QPS of an Alibaba Cloud account is limited to 100.
-   A maximum of 100 data records can be reported at a time. The maximum body size is 256 KB.
-   The metricName field can contain only letters, numbers, and underscores \(\_\). It must start with a letter. If the field starts with a character other than a letter, the character will be replaced with the uppercase letter A. If the field contains characters other than letters, numbers, and underscores \(\_\), the characters are invalid and will be replaced with underscores \(\_\) .
-   The dimensions field cannot contain equal signs \(=\), ampersands \(&\), or commas \(,\). Such characters are invalid and will be replaced with underscores \(\_\).
-   Each key-value pair in the metricName and dimensions fields can contain a maximum of 64 characters. If the key-value pair exceeds 64 characters, it will be truncated.

