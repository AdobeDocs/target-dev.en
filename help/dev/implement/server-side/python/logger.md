---
title: Initialize the [!DNL Adobe Target] Python SDK to log requests
description: Learn how to log requests in the [!DNL Adobe Target] Python SDK.
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
TQID: https://experienceleague.adobe.com/9LSln8V3QIG9GTok2yTTnKvhlpQhaed3a-qJyA4jErg
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
subfeature_v2:
  - id: a94ced60-8199-4549-b453-ede2acb4101e
    internal-label: Hybrid implementation
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
---
# Logger (Python)

## Description

When [initializing the SDK](initialize-sdk.md), the `options["logger"]` object is an optional object. By default, an INFO level logger will be created under the `adobe.target` namespace. However, in order to customize log level or debug effectively when an issue occurs, a `logger` object can be provided when initializing the SDK.

The `logger` object is expected to have a `debug()` and an `error()` method. When an appropriate logger is provided, [!DNL Target] requests and responses will be logged.

## Example

### Python

```python {line-numbers="true"}
logger = logging.getLogger("org.logger")
logger.setLevel(logging.DEBUG)

client_options = {
  "client": "acmeclient",
  "organization_id": "1234567890@AdobeOrg",
  "logger": logger
}
target_client = TargetClient.create(client_options)
```

You should see requests and responses being printed in the console.
