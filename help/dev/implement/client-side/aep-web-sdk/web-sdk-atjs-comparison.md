---
title: Comparing at.js to the Experience Platform Web SDK
description: Learn how the at.js features compare to [!DNL Experience Platform Web SDK].
keywords: target;adobe target;activity.id;experience.id;renderDecisions;decisionScopes;prehiding snippet;vec;Form-Based Experience Composer;xdm;audiences;decisions;scope;schema;system diagram;diagram
feature: AEP Web SDK
---
# Compare the at.js library to the [!DNL Adobe Experience Platform Web SDK]

## Overview

This article provides an overview of the differences between the `at.js` library and the Experience Platform Web SDK.

## Installing the libraries

### Installing at.js

[!DNL Adobe] lets customers download the library directly from the [!DNL Adobe Experience Cloud], [!UICONTROL Implementation] tab. The at.js library is customized with settings that the customer has like: clientCode, imsOrgId, etc.

### Installing the Web SDK

The prebuilt version is available on a CDN. You can reference the library on the CDN directly on your page, or download and host it on your own infrastructure. It is available in minified and unminified formats. The unminified version is helpful for debugging purposes.

See [Install the Web SDK using the JavaScript library](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/library) for more information.

## Configuring the libraries

### Configuring at.js

At the end of every at.js file, you see a section where [!DNL Adobe] instantiates and pass a setting object. It is customizable, at download Adobe populates that section with current customer settings.

```javascript
window.adobe.target.init(window, document, {
  "clientCode": "demo",
  "imsOrgId": "",
  "serverDomain": "localhost:5000",
  "timeout": 2000,
  "globalMboxName": "target-global-mbox",
  "version": "2.0.0",
  "defaultContentHiddenStyle": "visibility: hidden;",
  "defaultContentVisibleStyle": "visibility: visible;",
  "bodyHiddenStyle": "body {opacity: 0 !important}",
  "bodyHidingEnabled": true,
  "deviceIdLifetime": 63244800000,
  "sessionIdLifetime": 1860000,
  "selectorsPollingTimeout": 5000,
  "visitorApiTimeout": 2000,
  "overrideMboxEdgeServer": false,
  "overrideMboxEdgeServerTimeout": 1860000,
  "optoutEnabled": false,
  "optinEnabled": false,
  "secureOnly": false,
  "supplementalDataIdParamTimeout": 30,
  "authoringScriptUrl": "//cdn.tt.omtrdc.net/cdn/target-vec.js",
  "urlSizeLimit": 2048,
  "endpoint": "/rest/v1/delivery",
  "pageLoadEnabled": true,
  "viewsEnabled": true,
  "analyticsLogging": "server_side",
  "serverState": {},
  "decisioningMethod": "server-side",
  "legacyBrowserSupport":  false
});
```

[Learn more](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)

### Configuring the Platform Web SDK

Configuration for the SDK is done with the [`configure`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/overview) command. The `configure` command is *always* called first.

## How to request and automatically render Page Load [!DNL Target] offers

### Using at.js

Using at.js 2.x, if you enable the setting `pageLoadEnabled,` the library triggers a call to [!DNL Target] Edge with `execute -> pageLoad`. If all the settings are set to the default values, no custom coding is necessary. Once at.js is added to the page and loaded by the browser, a [!DNL Target] Edge call is executed.

### Using [!DNL PLatform Web SDK]

Content created within the [!DNL Target] [Visual Experience Composer](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/visual-experience-composer) can be retrieved and rendered automatically by the SDK.

To request and automatically render [!DNL Target] offers, use the `sendEvent` command and set the `renderDecisions` option to `true.` Doing so forces the SDK to automatically render any personalized content that's eligible for automatic rendering. 

Example:

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

[!DNL Experience Platform Web SDK] automatically sends a notification with the offers that were executed by the [!DNL Platform WEB SDK]. This is an example of how a notification request payload looks like:

```json
{
  "events": [{
      "xdm": {
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                "scope": "cart",
                "scopeDetails": {
                  "decisionProvider": "TGT",
                  "activity": {
                    "id": "127019"
                  },
                  "experience": {
                    "id": "0"
                  },
                  "strategies": [
                    {
                      "step": "entry",
                      "algorithmID": "0",
                      "trafficType": "0"
                    },
                    {
                      "step": "display",
                      "algorithmID": "0",
                      "trafficType": "0"
                    }
                  ],
                  "characteristics": {
                    "eventToken": "bKMxJ8dCR1XlPfDCx+2vSGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                  }
                }
              }
            ]
          }
        },
        "eventType": "display",
        "web": {
          "webPageDetails": {
            "viewName": "cart",
            "URL": "https://alloyio.com/personalizationSpa/cart"
          },
          "webReferrer": {
            "URL": ""
          }
        },
        "device": {
          "screenHeight": 800,
          "screenWidth": 1280,
          "screenOrientation": "landscape"
        },
        "environment": {
          "type": "browser",
          "browserDetails": {
            "viewportWidth": 1280,
            "viewportHeight": 284
          }
        },
        "placeContext": {
          "localTime": "2021-12-10T15:50:34.467+02:00",
          "localTimezoneOffset": -120
        },
        "timestamp": "2021-12-10T13:50:34.467Z",
        "implementationDetails": {
          "name": "https://ns.adobe.com/experience/alloy",
          "version": "2.6.2",
          "environment": "browser"
        }
      }
    }
  ]
}
```

[Learn more](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

## How to request and *NOT* automatically render Page Load Target offers

### Using at.js

There are two ways to fire a call to [!DNL Target] Edge that fetches offers for page-load.

Example 1:

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox", 
   success: console.log,
   error: console.error
});
```

Example 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Learn more](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/atjs-functions)

### Using [!DNL Platform Web SDK]

Execute a `sendEvent` command with a special scope under `decisionScopes`: `__view__`. [!DNL Adobe] uses this scope as a signal to fetch all the page-load activities from [!DNL Target] and prefetch all views. The [!DNL Platform Web SDK] also tries to evaluate all the VEC view based activities. Disabling view prefetching is not currently supported in the [!DNL Platform Web SDK].

To access any personalization content, you could provide a callback function, which will be called after the SDK receives a successful response from the server. Your callback is provided a result object, which might contain propositions property containing any returned personalization content.

Example:

```javascript
alloy("sendEvent", {
    xdm: {...},
    decisionScopes: ["__view__"]
  }).then(function(result) {
    if (result.propositions) {
      result.propositions.forEach(proposition => {
        proposition.items.forEach(item => {
          if (item.schema === HTML_SCHEMA) {
            // manually apply offer
            document.getElementById("form-based-offer-container").innerHTML =
              item.data.content;
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
          // manually send the display notification event, so that Target/Analytics impressions aare increased
            alloy("sendEvent",{
              "xdm": {
                "eventType": "decisioning.propositionDisplay",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          }
        });
      });
    }
  });
```

[Learn more](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

## How to request specific Form Based Target mboxes

### Using at.js

You can fetch f activities using the `getOffer` function:

Example 1:

```javascript
adobe.target.getOffer({
   mbox: "hero-banner", 
   success: console.log,
   error: console.error
});
```

Example 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        mboxes: [
        {
          index: 0,
          name: "hero-banner"
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Learn more](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/atjs-functions.html)

### Using [!DNL Platform Web SDK]

You can fetch [!UICONTROL Form-Based Composer] based activities by using the `sendEvent` command and passing the mbox names under the `decisionScopes` option. The `sendEvent` command returns a promise that gets resolved with an object containing the requested activities / propositions:

This code snippet is how the `propositions` array looks like:

```javascript
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg=="
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

Example:

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];
        if (item.schema === HTML_SCHEMA) {
          // apply offer
          document.getElementById("form-based-offer-container").innerHTML =
            item.data.content;
          const executedPropositions = [
            {
              id: proposition.id,
              scope: proposition.scope,
              scopeDetails: proposition.scopeDetails
            }
          ];

          alloy("sendEvent", {
            "xdm": {
              "eventType": "decisioning.propositionDisplay",
              "_experience": {
                "decisioning": {
                  "propositions": executedPropositions
                }
              }
            }
          });
        }
      }
    }
  }
});
```

[Learn more](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

## How to apply the [!DNL Target] activities

### Using at.js

You can apply the [!DNL Target] activities using the `applyOffers` function: `adobe.target.applyOffer(options).`

Example:

```javascript
adobe.target.getOffers({...})
  .then(response => adobe.target.applyOffers({ response: response }))
  .then(() => console.log("Success"))
  .catch(error => console.log("Error", error));
```

Learn more about the `applyOffers` command from the [dedicated documentation](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/adobe-target-applyoffers-atjs-2).

### Using [!DNL Platform Web SDK]

You can apply the [!DNL Target] activities using the `applyPropositions` command.

Example:

```javascript
alloy("applyPropositions", {
    propositions: [...]
});
```

Learn more about the `applyPropositions` command from the [dedicated documentation](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content).

## How to track events

### Using at.js

You can track events by using the `trackEvent` function or using `sendNotifications.`

This function fires a request to report user actions, such as clicks and conversions. This function does not deliver activities in the response.

**Example 1**

```javascript
adobe.target.trackEvent({ 
    "type": "click",
    "mbox": "some-mbox"
});
```

**Example 2**

```javascript
adobe.target.sendNotifications({ 
    request: {
       notifications: [{
          ...,
          mbox: {
            name: "some-mbox"
          },
          type: "click",
          ...
       }]
    }
});
```

[Learn more](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-trackevent.html)

### Using [!DNL Platform Web SDK]

You can track events and user actions by calling the `sendEvent` command, populating the `_experience.decisioning.propositions` XDM `fieldgroup`, and setting the `eventType` to one of two values:

* `decisioning.propositionDisplay`: Signals the rendering of the [!DNL Target] activity.
* `decisioning.propositionInteract`: Signals a user interaction with the activity, like a mouse click.

The `_experience.decisioning.propositions` XDM `fieldgroup` is an array of objects. The properties of each object are derived from the `result.propositions` that gets returned in the `sendEvent` command: `{ id, scope, scopeDetails }.`

**Example 1 - Track a `decisioning.propositionDisplay` event after rendering an activity**

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['discount']
}).then(function(result) {
  var propositions = result.propositions;

  var discountProposition;
  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      if (proposition.scope === "discount") {
        discountProposition = proposition;
        break;
      }
    }
  }

  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        var discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
        break;  
      }
    }
    // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered.
    alloy("sendEvent", {
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": [{
              "id": id,
              "scope": scope,
              "scopeDetails": scopeDetails
            }],
            "propositionEventType": {
              "display": 1
            }
          }
        }
      }
    });
  }
});
```

**Example 2 - Track a `decisioning.propositionInteract` event after a click metric occurs**

```javascript

alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items.length; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

[Learn more](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content#manual)

**Example 3 - Track an event fired after performing an action**

This example tracks an event which was fired after performing a specific action, such as clicking a button.
You can add any additional custom parameters through the `__adobe.target` data object.

You can also add the `commerce` XDM object.

```js
alloy("sendEvent", {
    "xdm": {
        "_experience": {
            "decisioning": {
                "propositions": [
                    {
                        "scope": "orderConfirm" //example scope name
                    }
                ],
                "propositionEventType": {
                    "display": 1
                }
            }
        },
        "eventType": "decisioning.propositionDisplay"
    },
    "commerce": {
        "order": {
            "purchaseID": "a8g784hjq1mnp3",
            "purchaseOrderNumber": "VAU3123",
            "currencyCode": "USD",
            "priceTotal": 999.98
        }
    },
    "data": {
        "__adobe": {
            "target": {
                "pageType": "Order Confirmation",
                "user.categoryId": "Insurance"
            }
        }
    }
})
```

## How to trigger a view change in a Single Page Application

### Using at.js

Use the `adobe.target.triggerView` function. This function can be called whenever a new page is loaded or when a component on a page is re-rendered. The `adobe.target.triggerView()` function should be implemented for single page applications (SPAs) to use the [!UICONTROL Visual Experience Composer] (VEC) to create [!UICONTROL A/B Test] and [!UICONTROL Experience Targeting] (XT) activities. If `adobe.target.triggerView()` is not implemented on the site, the VEC cannot be used for SPAs.

**Example**

```javascript
adobe.target.triggerView("homeView")
```

[Learn more](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)

### Using [!DNL Platform Web SDK]

To trigger or signal a single page application [!UICONTROL View Change], set the `web.webPageDetails.viewName` property under the `xdm` option of the `sendEvent` command. The [!DNL Platform Web SDK] checks the view cache, if there are offers for the `viewName` specified in `sendEvent` it executes them and send a display notification event.

**Example**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  xdm:{
    web:{
      webPageDetails:{
        viewName: "homeView"
      }
    }
  }
});
```

[Learn more](/help/dev/implement/client-side/aep-web-sdk/spa-implementation.md)

## How to leverage [!UICONTROL Response Tokens]

Personalization content returned from [!DNL Target] includes [response tokens](https://experienceleague.adobe.com/en/docs/target/using/administer/response-tokens). Response tokens are details about the activity, offer, experience, user profile, geo information, and more. These details can be shared with third-party tools or used for debugging. Response tokens can be configured in the [!DNL Target] user interface.

### Using at.js

Use at.js custom events to listen for the [!DNL Target] response and read the response tokens.

**Example**

```javascript
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(e) { 
  console.log("Request succeeded", e.detail); 
}); 
```

[Learn more](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)

### Using [!DNL Platform Web SDK]

>[!IMPORTANT]
>
>Ensure that you are using [!DNL Experience Platform Web SDK] version 2.6.0 or later.

The response tokens are returned as part of the `propositions` that are exposed in the result of the `sendEvent` command. Each proposition contains an array of `items,` and each item has a `meta` object populated with response tokens if they are enabled in the [!DNL Target] admin UI. [Learn more](https://experienceleague.adobe.com/en/docs/target/using/administer/response-tokens)

**Example**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Format of result.propositions:
      /*
        [
            {
                "id": "",
                "scope": "",
                "items": [
                    {
                        "id": "",
                        "schema": "",
                        "data": {},
                        "meta": { // RESPONSE TOKENS
                            "activity.name": ...,
                            "offer.id": ...,
                            "profile.activeActivities": ...
                        }
                    }
                ],
                "scopeDetails": {}
                "renderAttempted": false
            }
        ]
      */
    }
  });
```

[Learn more](/help/dev/implement/client-side/aep-web-sdk/accessing-response-tokens.md)

## How to manage flicker

### Using at.js

Using at.js you can manage flicker by setting `bodyHidingEnabled: true` so that at.js is the one that would take care of 
pre-hiding the personalized containers before it fetches and applies the DOM changes.

The page sections that contain personalized content can be pre-hidden by overriding at.js `bodyHiddenStyle.`

By default `bodyHiddenStyle` hides the whole HTML `body.` 

Both settings can be overridden using `window.targetGlobalSettings.` `window.targetGlobalSettings` should be placed before loading at.js.

### Using [!DNL Platform Web SDK]

Using [!DNL Platform Web SDK] the customer can set up their pre-hiding style in the configure command, like in the following example:

```javascript
alloy("configure", {
  datastreamId: "configurationId",
  orgId: "orgId@AdobeOrg",
  debugEnabled: true,
  prehidingStyle: "body { opacity: 0 !important }"
});
```

When loading the [!DNL Platform Web SDK] async, [!DNL Adobe] recommends that the following snippet is injected in the page before [!DNL Platform Web SDK] is injected:

```html
<script>
  !function(e,a,n,t){
  if (a) return;
  var i=e.head;if(i){
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
  setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

## How is A4T being handled

### Using at.js

There are two types of A4T logging that are supported using at.js:

* Analytics Client Side Logging
* Analytics Server Side Logging

#### Analytics Client Side Logging

**Example 1: Using [!DNL Target] Global Setting**

Analytics Client Side Logging can be enabled by setting `analyticsLogging: client_side` in the at.js settings or by overriding the `window.targetglobalSettings` object.

When this option is set up, the format of the payload that is returned looks like the following:

```json
{
  "analytics": {
    "payload": {
      "pe": "tnt",
      "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
    }
  }
}
```

The payload can then be forwarded to [!DNL Analytics] via the[!DNL  Data Insertion API].
 
Example 2: Configuring it in every `getOffers` function:

```javascript
adobe.target.getOffers({
      request: {
        experienceCloud: {
          analytics: {
            logging: "client_side"
          }
        },
        prefetch: {
          mboxes: [{
            index: 0,
            name: "a1-serverside-xt"
          }]
        }
      }
    })
    .then(console.log)
```

 This code snippet is how the response payload looks like: 

```json
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "bucharest",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "romania"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}

```

The [!DNL Analytics] payload (`tnta` token) should be included in the [!DNL Analytics] hit using [Data Insertion API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md).

#### [!DNL Analytics] Server Side Logging

[!DNL Analytics] Server Side Logging can be enabled by setting `analyticsLogging: server_side` in the at.js settings or by overriding the `window.targetglobalSettings` object.

Then the data flows as the following:

![Diagram showing the Analytics Server Side Logging workflow](/help/dev/implement/client-side/aep-web-sdk/assets/a4t-server-side-atjs.png)

[Learn More](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html)

### Using [!DNL Platform Web SDK]

The web SDK also supports:

* Analytics Client Side logging
* Analytics Server Side logging

#### [!DNL Analytics] Client Side Logging

[!DNL Analytics] Client Side Logging is enabled when [!DNL Adobe Analytics] is disabled for that DataStream configuration. 

![Diagram showing the Analytics Client Side Logging workflow](/help/dev/implement/client-side/aep-web-sdk/assets/analytics-disabled-datastream-config.png)

The customer has access to the [!DNL Analytics] token (`tnta`) that needs to be shared with [!DNL Analytics] using [Data Insertion API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) by chaining the `sendEvent` command and iterate through the resulting propositions array.

**Example**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  for (var i = 0; i < results.propositions.length; i++) {
    var proposition = results.propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getAnalyticsPayload(proposition);
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // send the page view Analytics hit with collected Analytics payload using Data Insertion API
});
```

Here is a diagram to show how data flows when [!DNL Analytics] Client Side is enabled:

![Data flow diagram in Analytics Client Side logging](/help/dev/implement/client-side/aep-web-sdk/assets/analytics-client-side-logging.png)

#### [!DNL Analytics] Server Side Logging

[!DNL Analytics] Server Side Logging is enabled when [!DNL Analytics] is enabled for that DataStream configuration.

![Datastreams UI showing the Analytics settings.](/help/dev/implement/client-side/aep-web-sdk/assets/analytics-enabled-datastream-config.png)

When Server Side [!DNL Analytics] Logging is enabled the A4T payload that needs to be shared with [!DNL Analytics] so that the [!DNL Analytics] reporting shows correct impressions and conversions is shared at the Edge Network level, so that the customer doesn't have to do any additional processing.

Here is how data flows into the systems when Server Side Analytics Logging is enabled:

![Diagram showing the data flow in Server Side Analytics Logging](/help/dev/implement/client-side/aep-web-sdk/assets/analytics-server-side-logging.png)

## How to set [!DNL Target] Global Settings

### Using at.js

You can override settings in the at.js library using `window.targetGlobalSettings,` rather than configuring the settings in the [!DNL Target] UI or by using REST APIs.

The override should be defined before at.js is loaded or in Administration > Implementation > Edit at.js Settings > Code Settings > Library Header.

Example:

```javascript
window.targetGlobalSettings = {  
   timeout: 200, // using custom timeout  
   visitorApiTimeout: 500, // using custom API timeout  
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com  
};
```

[Learn more](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html)

### Using [!DNL Platform Web SDK]

This feature is not supported in the Web SDK.

## How to update [!DNL Target] Profile attributes

### Using at.js

**Example 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "profile.name": "test",
     "profile.gender": "female"
   },
   success: console.log,
   error: console.error
});
```

**Example 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          profileParameters: {
            name: "test",
            gender: "female"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

### Using [!DNL Platform Web SDK]

To update a [!DNL Target] profile, use the `sendEvent` command and set the `data.__adobe.target` property, prefixing the key names using `profile.`

**Example**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## How do I use [!DNL Target Recommendations]

### Using at.js

**Example 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "entity.name": "T-shirt",
     "entity.id": "1234"
   },
   success: console.log,
   error: console.error
});
```

**Example 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          parameters: {
            "entity.name": "T-shirt",
            "entity.id": "1234"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Learn more](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-getoffers-atjs-2.html)

### Using [!DNL Platform Web SDK]

To send [!DNL Recommendations] data, use the `sendEvent` command and set the `data.__adobe.target` property, prefixing the key names using `entity.`

**Example**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.name": "T-shirt",
        "entity.id": "1234"
      }
    }
  }
});
```

## How do I use third-party IDs

### Using at.js

Using at.js there are multiple ways of sending `mbox3rdPartyId`, using `getOffer,` or `getOffers`:

**Example 1**

```javascript
adobe.target.getOffer({
  mbox:"test",
  params:{
    "mbox3rdPartyId": "1234"
  },
  success: console.log,
  error: console.error
});
```

**Example 2**

```javascript
adobe.target.getOffers({
    request: {
      id:{
        thirdPartyId: "1234"
      },
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

Or there is a way to set up the `mbox3rdPartyId` either in `targetPageParams` or `targetPageParamsAll.`

When setting `targetPageParams`, it sends in the requests for `target-global-mbox` also known as `pag-lLoad`.

The recommendation is to be set using `targetPageParamsAll` as it will be sent in every [!DNL Target] request. The advantage of using `targetPageParamsAll` is that you can define the `mbox3rdPartyId` on the page once to ensure that all the [!DNL Target] requests have the right `mbox3rdPartyId.`

```javascript
window.targetPageParamsAll = function() {
      return {
        "mbox3rdPartyId": "1234"
      };
    };
```

```javascript
window.targetPageParams = function() {
  return {
    "mbox3rdPartyId": "1234"
  };
};
```

[Learn more](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetpageparams.html)

### Using [!DNL Platform Web SDK]

[!DNL Platform Web SDK] supports [!DNL Target] Third-Party ID. However, it requires a few more steps.

Identity Map allows the customers to send multiple identities. All the identities are namespaced. Each namespace can have one or more identities. A particular identity can be marked as primary. With this knowledge in mind you can see what are the necessary steps to set up for the [!DNL Platform Web SDK ]to use [!DNL Target] Third-Party ID.

1. Set up the namespace that contains the [!DNL Target] Third-Party ID in the datastream configuration page:

  ![Datastreams UI showing the Target third party ID namespace field](/help/dev/implement/client-side/aep-web-sdk/assets/mbox3rdpartyid.png)
  
1. Send that identity namespace in every `sendEvent` command like this:

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "identityMap": {
      "TGT3PID": [
        {
          "id": "1234",
          "primary": true
        }
      ]
    }
  }
});
```

## How do I set property tokens

### Using at.js

Using at.js there are two ways of setting up the property tokens, either using `targetPageParams` or `targetPageParamsAll.` Using `targetPageParams` adds the property token to the `target-global-mbox` call, but using `targetPageParamsAll` adds the token to all the [!DNL Target] calls:

**Example 1**

```javascript
   window.targetPageParamsAll = function() {
      return {
        "at_property": "1234"
      };
    };
```

**Example 2**

```javascript
window.targetPageParams = function() {
      return {
        "at_property": "1234"
      };
    };
```

### Using [!DNL Platform Web SDK]

Using [!DNL Platform Web SDK] customers are able to set up the property at a higher level, when setting up the datastream configuration, under the [!DNL Adobe Target] namespace:

![Datastreams UI showing the Adobe Target settings.](/help/dev/implement/client-side/aep-web-sdk/assets/at-property-setup.png)

This means that every [!DNL Target] call for that specific Data Stream configuration contains that property token.

## How do I prefetch mboxes

### Using at.js

This functionality is available only in at.js 2.x. at.js 2.x has a new function named `getOffers`. The `getOffers` function allows customers to prefetch content for one or more mboxes. Here is an example:

```javascript
adobe.target.getOffers({
    request: {
      prefetch: {
        mboxes: [{
          index: 0,
          name: "test-mbox",
          parameters: {
            ...
          },
          profileParameters: {
            ...
          }
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

>[!NOTE]
>
>Adobe recommends ensuring that every `mbox` in the `mboxes` array has its own index. Usually the first mbox has `index=0` the next one `index=1,` and so forth. 

### Using [!DNL Platform Web SDK]

This functionality is currently not supported in [!DNL Platform Web SDK].

## How do I debug my [!DNL Target] implementation

### Using at.js

The at.js library exposes these debugging features:

* Mbox Disable - disable [!DNL Target] from fetching and rendering to check if the page is broken without [!DNL Target] interactions
* Mbox Debug - at.js logs every action
* Target Trace - with an mbox trace token generated in a trace object with details that participated in the decisioning process is available under `window.___target_trace` object.

>[!NOTE]
>
>All these debugging features are available with enhanced capabilities in [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob).

### Using [!DNL Platform Web SDK]

You have multiple debugging capabilities when using [!DNL Platform Web SDK]:

* Using [Assurance](https://experienceleague.adobe.com/en/docs/experience-platform/assurance/home)
* [Web SDK debug enabled](https://experienceleague.adobe.com/en/docs/experience-platform/assurance/home)
* Use [Web SDK monitoring hooks](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* Use [Adobe Experience Platform Debugger](https://experienceleague.adobe.com/en/docs/experience-platform/debugger/home)
* Target Trace