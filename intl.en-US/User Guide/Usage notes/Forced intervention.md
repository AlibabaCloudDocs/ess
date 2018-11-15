# Forced intervention {#concept_25919_zh .concept}

This topic introduces the forced intervention.

Auto Scaling does not prevent users from performing forced interventions, such as deleting automatically created ECS instances from the ECS console. Auto Scaling handles forced interventions in the following ways:

|Resource|Forced intervention types|Solutions|
|:-------|:------------------------|:--------|
|ECS|An ECS instance is deleted from a scaling group through the ECS console or API.|Auto Scaling determines if the ECS instance is in an unhealthy state through [health check](reseller.en-US/User Guide/Usage notes/Remove an unhealthy ECS instance.md#), and if so, removes the instance from the scaling group. The ECS instance’s intranet IP address is not automatically deleted from the RDS access whitelist. When the number of ECS instances \(Total Capacity\) in the scaling group is smaller than the MinSize value, Auto Scaling automatically adds ECS instances to the group until the number of instances reaches the MinSize value.|
|ECS|The ECS OpenAPI permissions are revoked from Auto Scaling.|All scaling activity requests are rejected.|
|Server Load Balancer|An ECS instance is removed from a Server Load Balancer instance by force through the Server Load Balancer console or API.|Auto Scaling does not automatically detect this action or handle such an exception. The ECS instance remains in the scaling group, but is released if it was selected according to the removal policy of a scale-down activity.|
|Server Load Balancer|A Server Load Balancer instance is deleted \(or its health check function is disabled\) by force through the Server Load Balancer console or API.|No ECS instance is added to the scaling group that has been added to the Server Load Balancer instance. Scaling tasks can trigger scaling rules to remove ECS instances from the scaling group. ECS instances deemed unhealthy by the health check function can also be removed.|
|Server Load Balancer|A Server Load Balancer instance becomes unavailable \(due to overdue payment or a fault\).|All scaling activities fail, except for activities that are manually triggered to remove ECS instances.|
|Server Load Balancer|The Server Load Balancer API permissions are revoked from Auto Scaling.|Auto Scaling rejects all scaling activity requests for the scaling groups added to the Server Load Balancer instance.|
|RDS|The IP address of an ECS instance is removed from an RDS whitelist through the RDS console or API.|Auto Scaling does not detect this action automatically or handle such an exception. The ECS instance remains in the scaling group. If this instance is selected according to the removal policy of a scale-down activity, it is released.|
|RDS|An RDS instance is deleted by force through the RDS console or API.|The scaling group that configured the RDS instance will no longer add ECS instances. No ECS instance is added to the scaling group that has been added to this RDS instance. Scaling tasks can trigger scaling rules to remove ECS instances from the scaling group. ECS instances determined to be unhealthy by the health check function can also be removed.|
|RDS|An RDS instance becomes unavailable \(due to overdue payment or a fault\).|All scaling activities fail except for those manually triggered to remove ECS instances.|
|RDS|The RDS API permissions are revoked from Auto Scaling.|Auto Scaling rejects all scaling activity requests for the scaling groups added to the RDS instance.|

