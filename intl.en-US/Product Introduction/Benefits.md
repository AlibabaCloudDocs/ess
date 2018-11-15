# Benefits {#concept_evq_kfm_qfb .concept}

This article introduces the function, product features and scenarios of Auto Scaling.

## Overview {#section_zhg_bgm_qfb .section}

-   Automatically add or remove ECS instances when demand on your application increases or decreases.
-   Automatically configure the ECS instances of Sever Load Balancer.
-   Supports configure the ApsaraDB for RDS whitelist.

## Features {#section_scg_cgm_qfb .section}

-   On demand: Adjust resources to fit the demand curve in real time. You do not have to worry about your computing capacity when demand surges.
-   Automated: Automatically create and release ECS instances based on policies you specify. Configure the Server Load Balancer and RDS whitelists with no manual operation.
-   Flexible: You can setup scheduled scaling, dynamic scaling based on targets monitored, scaling fixed number of instances, and automated replacing of unhealthy instances. It also can use external monitoring systems through APIs.
-   Intelligent: Can be applied to complicated scenarios.

## Scenarios {#section_cdh_dgm_qfb .section}

-   Video sharing: Workload surges during holidays and festivals. Computing resources have to be scaled out automatically in real time.
-   Video streaming: Demand curve is difficult to predict manually. Computing resources have to be scaled out based on CPU usage, workload, or bandwidth.
-   Gaming: Demand increasing starts at 12:00 and lasts from 18:00 to 21:00, scheduled scaling is needed.

