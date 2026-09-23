---
title: Adobe Target Delivery API Getting Started
description: How do I use the [!UICONTROL Adobe Target Delivery API]?
keywords: delivery api
exl-id: 142ec3be-b017-4cdc-9079-b1cc173a710a
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/DC-YVq6VfAaqMU1utmIMw73gzp4PIJgQjaS0a8FQEO4
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
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# Getting Started with the [!UICONTROL Adobe Target Delivery API]

>[!IMPORTANT]
>
>This guide applies to [!DNL at.js] and direct server-side implementations that call the [!UICONTROL Target Delivery API] directly. If you are implementing [!DNL Target] using the [!UICONTROL Adobe Experience Platform Web SDK], use the Interact API (`sendEvent` command over the [!UICONTROL Experience Platform Edge Network]) instead. See [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md) for more information.

A [!UICONTROL Target Delivery API] call looks like this:

```
curl -X POST \
  'https://`clientCode`.tt.omtrdc.net/rest/v1/delivery?client=`clientCode`&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
      "context": {
        "channel": "web",
        "browser" : {
          "host" : "demo"
        },
        "address" : {
          "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
        },
        "screen" : {
          "width" : 1200,
          "height": 1400
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          }
        ]
      }
    }'
```

The `clientCode` can be retrieved from the [!DNL Target] UI by navigating to **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

Before making a [!UICONTROL Target Delivery API] call, follow these steps to ensure a response contains the relevant experience to show end users:

1. Create a [!DNL Target] activity (A/B, XT, AP or Recommendations) using the [Form-Based Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en) or the [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).
1. Use the Delivery API to get a response for the mboxes used in the [!DNL Target] activity created in Step 2.
1. Present the experience to the visitor.
