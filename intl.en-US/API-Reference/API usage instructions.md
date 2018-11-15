# API usage instructions {#concept_25925_zh .concept}

Before calling the Auto Scaling API, you must activate the Auto Scaling service on the Alibaba Cloud official website, and grant Auto Scaling the API permission in the console.

For the detailed operations, see [access resources](../../../../reseller.en-US//Authorization/Access resources.md#).

## Prerequisite {#section_bsy_hk2_sfb .section}

Before calling the Auto Scaling API, you must activate the Auto Scaling service on the Alibaba Cloud official website, and grant Auto Scaling the API permission in the console. For the detailed operations, see [access resources](../../../../reseller.en-US//Authorization/Access resources.md#).

## Errors {#section_ccb_zn2_sfb .section}

Before calling the Auto Scaling API, you need to activate Auto Scaling at Alibaba Cloud website, and authorize your Auto Scaling to access API on the Auto Scaling console \(based on Alibaba Cloud Resource Access Management \[RAM\], Auto Scaling uses ECS API to replace the ECS instance resources\). Errors will occur in case of any inconformity:

|Error codes|Error code|Description|HTTP status code|
|:----------|:---------|:----------|:---------------|
|Auto Scaling is not activated and thus the API cannot be called.|Forbidden.Unsubscribed|Do not have permission to access this API.|403|
|You have not fully authorized Open API to Auto Scaling.|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|403|

