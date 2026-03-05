---
title: Adobe Target Delivery API Client Hints
description: How do I use Client Hints in the [!DNL Adobe Target] Delivery API?
exl-id: 317b9d7d-5b98-464e-9113-08b899ee1455
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/ijbOsWitZdNHpjNduh8xtPyEYdw2tsWz2rB6jZ5JbQA
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: ff2b9b37-92e0-45fc-b853-379d44c08c89
    internal-label: Audience segmentation
---
# Client Hints and the [!UICONTROL Adobe Target Delivery API]

Client Hints must be sent to [!DNL Adobe Target] on the offers request.

Generally, it is recommended to send all available Client Hints to [!DNL Target]. For more information, see [User-agent and Client Hints](/help/dev/implement/client-side/atjs/user-agent-and-client-hints.md) in the [Client-side Implementation](../../implement/client-side/overview.md) section.

## Delivery API direct calls

### From the browser

In this case, the browser will send low-entropy Client Hints to [!DNL Target] automatically via request headers. But there are a couple browser-level limitations with this implementation. First - no Client Hints headers will be sent from the browser unless the request is being made over https. Second - Client Hints will not be sent on the first request to [!DNL Target] on the page. Client Hints headers will only be sent on the second request and all requests thereafter. This means that audience segmentation and personalization cannot be performed by [!DNL Target] on the first page visit. In order to get around both of these limitations, we strongly recommend using the User Agent Client Hints API in the browser to collect the Client Hints directly, and send them on the request payload.

### From a server

In this case the Client Hints must be manually forwarded from the browser to [!DNL Target] on the Delivery API request.

```
curl -X POST 'http://mboxedge28.tt.omtrdc.net/rest/v1/delivery?client=myClientCode&sessionId=abcdefghijkl00014' -d '{
  "context": {
    "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Safari/537.36",
    "clientHints": {
      "Sec-CH-UA-Model": "iPhone",
      "Sec-CH-UA-Mobile": true,
      "Sec-CH-UA-Platform": "iOS",
      "Sec-CH-UA": "[ { \"brand\": \"Chromium\", \"version\": \"91\" }, { \"brand\": \" Not;A Brand\", \"version\": \"99\" } ]",
      "Sec-CH-UA-Full-Version-List": "[ { \"brand\": \"Chromium\", \"version\": \"91.1.1.1\" }, { \"brand\": \" Not;A Brand\", \"version\": \"99.1.1.1\" } ]",
      "Sec-CH-UA-Platform-Version": "10.0.0",
      "Sec-CH-UA-Arch": "x86",
      "Sec-CH-UA-Bitness": "64"
    }
  },
  "execute": {
    "mboxes": [{
      "name": "home",
      "index": 1
    }]
  }
}'
```

## Formatting

Client Hints headers Sec-CH-UA and Sec-CH-UA-Full-Version-List have a different format than the results from the Client Hints browser API (navigator.userAgentData.brands/navigator.userAgentData.getHighEntropyValues). Both of these formats are accepted by Delivery API. The Delivery API will normalize the values into the format used in the request headers, which is important to keep in mind if accessing Client Hints in profile scripts.
