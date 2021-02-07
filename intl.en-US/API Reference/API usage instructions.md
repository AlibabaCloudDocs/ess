# API usage instructions

Before you call Auto Scaling API, you must activate Auto Scaling on the official Alibaba Cloud website and grant Auto Scaling the API permissions in the console.

## Prerequisites

Auto Scaling is activated. The following permissions are granted to Auto Scaling and RAM users:

-   The permissions on related cloud resources granted to Auto Scaling. For more information, see [Manage the Auto Scaling service linked role](/intl.en-US/Quick Start/Manage the Auto Scaling service linked role.md).
-   The permissions on related cloud resources granted to RAM users, including `AliyunESSFullAccess` and `AliyunECSFullAccess`. For more information, see [Grant permissions to a RAM user](/intl.en-US/RAM User Management/Grant permissions to a RAM user.md).

## Errors

Before you call Auto Scaling API, you must activate Auto Scaling on the official Alibaba Cloud website and grant Auto Scaling the API permissions to scale ECS instances. The following table describes the errors that may occur if the preceding requirements are not met.

|HTTP status code|Error code|Error message|Description|
|:---------------|:---------|:------------|-----------|
|403|Forbidden.Unsubscribed|Do not have permission to access this API.|The error message returned because Auto Scaling is not activated and not granted the permissions to call the specified API operation.|
|403|Forbidden.Unauthorized|A required authorization for the specified action is not supplied.|The error message returned because Auto Scaling is not authorized to call the specified API operation.|

