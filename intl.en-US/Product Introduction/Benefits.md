# Benefits

This topic describes the features and scenarios of Auto Scaling.

## Features

-   Automatically adds or removes ECS instances based on your business requirements.
-   Automatically adds or removes ECS instances to or from the backend server groups of the associated SLB instances.
-   Automatically adds or removes IP addresses of ECS instances to or from the whitelists of the associated ApsaraDB for RDS instances.

## Benefits

-   On demand: ESS scales resources on demand to respond to traffic spikes in real time without the need to predict demand changes.
-   Automatic: ESS automatically creates and releases ECS instances without manual intervention. It also automatically configures SLB instances and whitelists of ApsaraDB for RDS instances.
-   Flexible: ESS allows you to schedule, customize, and fix the minimum number of instances, as well as configure automatic replacement of unhealthy instances. It also provides API operations to allow you to monitor instances by using external monitoring systems.
-   Intelligent: ESS intelligently schedules cloud computing resources to respond to various complex scenarios.

## Scenarios

-   Video streaming: Traffic loads surge during holidays and festivals. Cloud computing resources must be automatically scaled out to meet the increased demands.
-   Live streaming and broadcast: Traffic loads are ever-changing and difficult to predict. Alibaba Cloud computing resources must be scaled based on CPU utilization, application load, and bandwidth usage.
-   Gaming: Traffic loads increase at 12:00 and from 18:00 to 21:00. Cloud computing resources must be scaled out on a regular basis.
-   E-commerce: Traffic loads surge during big promotions. A large number of ECS instances must be created and available within minutes.

