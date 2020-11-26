# API usage instructions

Before you call Auto Scaling API, you must activate Auto Scaling on the Alibaba Cloud official website and grant Auto Scaling the API permission in the console.

## Prerequisites

Auto Scaling is activated and granted the permission to call Auto Scaling API. For more information, see [Manage the Auto Scaling service linked role](/intl.en-US/Quick Start/Manage the Auto Scaling service linked role.md).

## Errors

Before you call Auto Scaling API, you must activate Auto Scaling on the Alibaba Cloud official website and grant Auto Scaling the API permission to scale ECS instances. The following table describes the errors that may occur when the preceding requirements are not met.

|HTTP status code|Error code|Error message|Description|
|:---------------|:---------|:------------|-----------|
|403|Forbidden.Unsubscribed|Do not have permission to access this API.|The error message returned because Auto Scaling is not activated and not granted the permission to call the API operation.|
|403|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|The error message returned because Auto Scaling is not authorized to call the specified operation.|

