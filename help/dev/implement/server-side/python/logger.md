---
title: Initialize the [!DNL Adobe Target] Python SDK to log requests
description: Learn how to log requests in the [!DNL Adobe Target] Python SDK.
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
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
