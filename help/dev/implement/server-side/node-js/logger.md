---
title: Initialize the [!DNL Adobe Target] Node.js SDK to log requests
description: Learn how to log requests in the [!DNL Adobe Target] Node.js SDK.
feature: APIs/SDKs
exl-id: 5db3e301-47b3-4330-b185-c0c03f72e790
---
# Logger (Node.js)

## Description

When [initializing the SDK](initialize-sdk.md), the `options.logger` object is an optional object. However, in order to debug effectively when an issue occurs, a `logger` object should be provided when initializing the SDK.

The `logger` object is expected to have a `debug()` and an `error()` method. When an appropriate logger is provided, such as `console`, [!DNL Target] requests and responses will be logged.

## Example

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg",
  logger: console
};

const targetClient = TargetClient.create(CONFIG);

const request = {
    execute: {
        mboxes: [{
            name: "a1-serverside-ab",
            index: 1
        }]
    }
};

const response = await targetClient.getOffers({ request, targetCookie });
```

You should see requests and responses being printed in the console.
