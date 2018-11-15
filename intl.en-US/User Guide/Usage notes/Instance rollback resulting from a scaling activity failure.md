# Instance rollback resulting from a scaling activity failure {#concept_kmc_phn_qfb .concept}

This topic describes the instance rollback resulting from a scaling activity failure.

When a scaling activity fails to add one or more ECS instances to a scaling group, the failed ECS instances are rolled back. The scaling activity is not rolled back.

For example, if a scaling group has 20 ECS instances, out of which 19 instances are added to the Server Load Balancer instance, only the one ECS instance that fails to be added is automatically released.

Auto Scaling uses Alibaba Cloud’s Resource Access Management \(RAM\) service to adjust the resources of ECS instances through ECS Open APIs. Therefore, API usage fees apply.

