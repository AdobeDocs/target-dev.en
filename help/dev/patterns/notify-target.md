---
title: Notify Target
description: Ensure that all events that need to be tracked by [!DNL Target] are sent using the trackEvent method.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: yes
hidefromtoc: yes
---
# Notify [!DNL Target]

Completing this step ensures that all events that need to be sent to [!DNL Adobe Target] are sent using the `trackEvent` method.

Any event that needs to be tracked in [!DNL Target] can be a primary conversion event or a success metric.

>[!TIP]
>
>Click the images in this topic to expand to full screen.

## Notify [!DNL Target] diagram {#diagram}

The step number in the following illustration corresponds to the section below.

![Notify Target diagram](/help/dev/patterns/assets/diagram-notify-target.png){width="600" zoomable="yes"}

## Fire [!DNL Adobe Target] Track API

This step helps you ensure that all events that need to be sent to [!DNL Target] are sent using the `trackEvent` method.

+++See details

![Fire Adobe Target Track API diagram](/help/dev/patterns/assets/fire-adobe-target-track-api-diagram.png){width="100" zoomable="yes"}

You send the order conversion attributes as mentioned in the Prerequisite section below. The name of the mbox does not matter, but the conversion is to use `orderConfirmPage`.

You don't need to include the order conversion attributes in this call. These calls ideally record success metrics that can be thought of as mini-conversion events before the main conversion events. `CardIds` must be included in cart-based recommendations based on the `Add to Cart` event.

**Prerequisites**

* Meet with your business team to identify all events that can be considered as conversion or success metrics. You must also identify the conversion event that generates revenue so that those details can be sent to [!DNL Target] along with the event data.
* Ensure that the following attributes are available in the data layer so that you can send them with the conversion event. The conversion event generates revenue, such as a product purchase or Add to Cart event.

  * `productPurchaseId`: Product IDs that were purchased as part of the order. Comma separate multiple products.
  * `orderTotal`: Order total for the purchase.
  * `orderId`: Order ID of the purchase.

* If you are tracking an event for cart add, send `cartIds` as a parameter. A comma-separated list of product IDs can be passed for `cardIds`.

**Readings**

* [adobe.target.trackEvent() method](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
* [cartIds for cart-based criteria](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based){target=_blank}

**Actions**

* Use `adobe.target-trackEvent()` method to send all data that needs to be sent to [!DNL Target].







