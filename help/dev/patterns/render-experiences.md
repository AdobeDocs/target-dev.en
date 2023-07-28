---
title: Render experiences
description: Ensure that all necessary steps for rendering experiences are executed in the correct sequence.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: yes
hidefromtoc: yes
---
# Render experiences

Follow the steps in the *Render Experiences* diagram to ensure that all necessary tasks needed to render experiences are executed in the correct sequence.

>[!TIP]
>
>Click the images in this topic to expand to full screen.

## Render experiences diagram {#diagram}

Automatic out-of-the-box flicker handling available with at.js makes sense only when you have [!UICONTROL Automatic Page Load Request] enabled. This option hides the entire HTML body while fetching the experiences from [!DNL Target]. In this case, it is your responsibility to handle flicker. Search for implementation patterns available for flicker handling for guidance. 

The step numbers in the following illustration correspond to the sections below. 

![Render experiences diagram](/help/dev/patterns/assets/diagram-render-experiences-new.png){width="600" zoomable="yes"}

Click the following links to navigate to the desired sections:

* [3.1: Promotion](#promotion)
* [3.2: Cart-based criteria](#cart)
* [3.3: Popularity-based criteria](#popularity)
* [3.4: Item-based criteria](#item)
* [3.5: User-based criteria](#user)
* [3.6: Custom criteria](#custom)
* [3.7: Provide attributes used in inclusion rules](#inclusion)
* [3.8: Provide excludedIds](#exclude)
* [3.9: Provide entity attributes to update the product catalog for Recommendations](#entity-attributes)
* [3.10: Provide profile attributes used as keys for inclusion rules](#keys)
* [3.11: Fire page-load request](#fire)
* [3.12: Fire regional location request](#location)

## 3.1: Promotion {#promotion}

Add promoted items and control their placement in your Target Recommendations [designs](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

+++See details

**Available options**

* Promote by IDs
* [Promote by collection](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Promote by attribute](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Entity parameters required**

* Item attribute in promotions must be passed when using the "promote by attribute" option.

+++

[Return to the diagram at the top of this page.](#diagram)

## 3.2: Cart-based criteria {#cart}

Make recommendations based on the user's cart contents.

+++See details

**Available criteria**

* [!UICONTROL People Who Viewed These, Viewed Those]
* [!UICONTROL People Who Viewed These, Bought Those]
* [!UICONTROL People Who Bought These, Bought Those]

**Entity parameters required**

* cartIds

**Readings**

* [Cart-based ](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Return to the diagram at the top of this page.](#diagram)

## 3.3: Popularity-based criteria {#popularity}

Make recommendations based on the overall popularity of an item across your site or based on the popularity of items within a user's favorite or most-viewed category, brand, genre, and so forth.

+++See details

**Available criteria**

* [!UICONTROL Most Viewed Across the Site]
* [!UICONTROL Most Viewed by Category]
* [!UICONTROL Most Viewed by Item Attribute]
* [!UICONTROL Top Sellers Across the Site]
* [!UICONTROL Top Sellers by Category]
* [!UICONTROL Top Sellers by Item Attribute]
* [!UICONTROL Top by Analytics Metric]

**Entity parameters required**

* `entity.categoryId` or the item attribute for popularity based if the criteria is based on the current or the item attribute. 
* Nothing must be passed for Most Viewed/Top sold across the site.

**Readings**

* [Popularity-based](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Return to the diagram at the top of this page.](#diagram)

## 3.4: Item-based criteria {#item}

Make recommendations based on finding similar items to an item that the user is viewing or has recently viewed.

+++See details

**Available criteria** 

* [!UICONTROL People Who Viewed This, Viewed That]
* [!UICONTROL People Who Viewed This, Bought That]
* [!UICONTROL People Who Bought This, Bought That]
* [!UICONTROL Items with Similar Attributes]

**Entity parameters required**

* `entity.id`
* If any profile attribute is used as a key

**Readings**

* [Item based](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Return to the diagram at the top of this page.](#diagram)

## 3.5: User-based criteria {#user}

Make recommendations based on the user's behavior.

+++See details

**Available criteria**

* [!UICONTROL Recently Viewed Items]
* [!UICONTROL Recommended for You]

**Entity parameters required**

* `entity.id`

**Readings**

* [User-based](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Return to the diagram at the top of this page.](#diagram)

## 3.6: Custom criteria {#custom}

Make recommendations based on a custom file that you upload

+++See details

**Available criteria**

* [!UICONTROL Custom algorithm]

**Entity parameters required**

`entity.id` or the attribute used as a key for the custom algorithm

**Readings**

* [Custom criteria](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Return to the diagram at the top of this page.](#diagram)

## 3.7: Provide attributes used in inclusion rules {#inclusion}

+++See details

**Readings**

* [Use dynamic and static inclusion rules](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[Return to the diagram at the top of this page.](#diagram)

## 3.8: Provide excludedIds {#exclude}

Pass entity IDs for entities that you want to exclude from your recommendations. For example, you can exclude items that are already in the shopping cart.

+++See details

**Readings**

* [Can I dynamically exclude an entity?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[Return to the diagram at the top of this page.](#diagram)

## 3.9: Provide entity attributes to update the product catalog for [!DNL Recommendations] {#entity-attributes}

+++See details

**Readings**

* [Entity attributes](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

You can also accomplish this step by creating product feeds using the [!DNL Target] UI to update the product catalog for [!DNL Recommendations].

+++

[Return to the diagram at the top of this page.](#diagram)

## 3.10: Provide profile attributes used as keys for inclusion rules {#keys}

Provide the profile attributes that are used as keys for inclusion rules in any Recommendations criteria mentioned above.

+++ See details

**Readings**

* [Profile attributes](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html){target=_blank}

+++

[Return to the diagram at the top of this page.](#diagram)

## 3.11: Fire page-load request {#fire}

This step triggers a [!DNL Delivery API] call with `execute` > `pageLoad` payload in the request. The `getOffers()` method fetches the experience and `applyOffers()` renders the experience on the page. The pageLoad request is needed for rendering experiences authored in the [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank} (VEC).

+++See details

![Fire page-load request diagram](/help/dev/patterns/assets/fire-page-load-request.png){width="100" zoomable="yes"}

**Prerequisites**

* All data mapping must be done using the `targetPageParams` function.

**Readings**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Actions**

* Use the `getOffers` and `applyOffers` methods to fetch the experience using a Page Load Request API call.

+++

[Return to the diagram at the top of this page.](#diagram)

## 3.12: Fire regional location request (#location)

This step triggers a [!DNL Delivery API] call with `execute` > `mboxes` payload in its request. The `getOffers` method fetches the experience and `applyOffers` renders the experience to the page. You can send more than one mbox under the `execute` > `mboxes` payload.

+++See details

![Fire regional location request diagram](/help/dev/patterns/assets/fire-regional-location-request.png){width="100" zoomable="yes"}

**Prerequisites**

* All data mapping must be done using the `targetPageParams` function.

**Readings**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Actions**

* Use the `getOffers` and `applyOffers` methods to fetch the experience using a Page Load Request API call.

+++

[Return to the diagram at the top of this page.](#diagram)