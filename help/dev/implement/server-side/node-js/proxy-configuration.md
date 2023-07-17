---
title: Implement proxy configuration in the [!DNL Adobe Target] Node.js SDK
description: Learn how to configure the [!UICONTROL TargetClient] proxy configuration in the [!DNL Adobe Target] Node.js SDK.
feature: APIs/SDKs
exl-id: c9f04e81-3fa3-4e64-a974-379420b0518a
---
# Proxy Configuration (Node.js)

To configure a proxy for the Node SDK's HTTP requests, override the fetch API used by the SDK during initialization.

The following is a basic example showing how to override `fetchApi` during the `TargetClient` initialization to add a proxy:

```javascript {line-numbers="true"}
const { ProxyAgent } = require("undici");

const proxyAgent = new ProxyAgent("your proxy address here");

const fetchImpl = (url, options) => {
  const fetchOptions = options;
  fetchOptions.dispatcher = proxyAgent;
  return fetch(url, fetchOptions);
};

client = TargetClient.create({
    ...,
    fetchApi: fetchImpl
});
```

Note that this only works for Node versions 18.2+, in which `undici.fetch` is the default `fetch` for node.
Please visit the [Node SDK samples repo](https://github.com/adobe/target-nodejs-sdk-samples/tree/master/proxy-configuration)
for proxy configuration examples for older versions of node and more information.
