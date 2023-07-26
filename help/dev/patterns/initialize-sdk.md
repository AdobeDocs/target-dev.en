---
title: Initialize SDKs
description: Ensure that all necessary steps for loading the Adobe Experience Platform Web SDK are executed in the correct sequence.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: yes
hidefromtoc: yes
---
# Initialize SDKs

Follow the steps in the *Initialize SDK* diagram to ensure that all necessary tasks needed to load the [!DNL Adobe Target] at.js JavaScript library are executed in the correct sequence. 

>[!TIP]
>
>Click the images in this topic to expand to full screen.

## Initialize SDKs diagram {#diagram}

For a multi-page application, this flow happens every time the page reloads, or the visitor navigates to a new page on the website.

The step numbers in the following illustration correspond to the sections below. 

![Initialize SDKs diagram](/help/dev/patterns/assets/diagram-initiaze-sdk.png){width="600" zoomable="yes"}

Click the following links to navigate to the desired sections:

* [1.1: Load visitor API SDK](#load)
* [1.2: Set Customer ID](#set)
* [1.3: Configure automatic page load request](#automatic)
* [1.4: Configure flicker handling](#flicker)
* [1.5: Configure data mapping](#data-mapping)
* [1.6: Promotion](#promotion)
* [1.7: Cart-based criteria](#cart)
* [1.8: Popularity-based criteria](#popularity)
* [1.9: Item-based criteria](#item)
* [1.10: User-based criteria](#user)
* [1.11: Custom criteria](#custom)
* [1.12: Provide attributes used in inclusion rules](#inclusion)
* [1.13: Provide excludedIds](#exclude)
* [1.14: Pass the entity.event.detailsOnly=true parameter](#true)
* [1.15: Configure remote data mapping](#remote)
* [1.16: Load at.js](#web)

## 1.1: Load visitor API SDK {#load}

This step helps ensure that the `VisitorAPI.js` library is loaded, configured, and initialized correctly. 

+++See details

![Load Visitor API SDK diagram](/help/dev/patterns/assets/load-visitor-api-sdk.png){width="100" zoomable="yes"}

**Prerequisites**

* To use the Visitor ID/API service, your company must be enabled for the Adobe Experience Cloud and have an Organization ID. For more information, see [Experience Cloud Requirements: Organization ID](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html?){target=_blank} in the *Identity Service Help* guide.
* You need the VisitorAPI.js file. Reach out to your digital marketing team to get this file.

**Configure and refer VisitorAPI.js**

For more information, see [Implement the Experience Cloud Service for Target](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html){target=_blank}.

**Readings**

* [Experience Cloud Identity Service overview](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html){target=_blank}
* [About the ID Service](https://experienceleague.adobe.com/docs/id-service/using/intro/about-id-service.html){target=_blank}
* [Cookies and the Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html){target=_blank}
* [How the Experience Cloud Identity Service requests and sets IDs](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html){target=_blank}
* [Understanding ID synchronization and match rates](https://experienceleague.adobe.com/docs/id-service/using/intro/match-rates.html){target=_blank}

**Actions**

* Embed the `VisitorAPI.js` file on your webpages.
* Read about the [available configurations for the Visitor ID/API service](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html){target=_blank}.
* After the `VisitorAPI.js` file is loaded, use the `Visitor.getInstance` method to initialize using the necessary configurations you need.
* Familiarize yourself with all the [available methods](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html){target=_blank}.

+++

[Return to the diagram at the top of this page.](#diagram)

## 1.2: Set Customer ID {#set}

This step helps ensure that your end users' known IDs (CRM ID, User ID, and so forth) are tied to the anonymous ID of Adobe for cross-device personalization.

+++See details

![Set Customer ID](/help/dev/patterns/assets/set-customer-id.png){width="100" zoomable="yes"}

**Prerequisites**

* The end user's known ID should be available in the Data Layer.

**Set Customer ID**
For more information, see [setCustomerIDs](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html){target=_blank}.

**Readings**

* [Real-time profile syncing for mbox3rdPartyId](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html){target=_blank}

**Actions**

* Use `visitor.setCustomerIDs` to set the end-user known ID.

+++

[Return to the diagram at the top of this page.](#diagram)

## 1.3: Configure automatic page load request {#automatic}

This step enables at.js to fetch all the experiences that must be rendered on the page while loading the at.js JavaScript library file.

+++See details

![Configure automatic page load request](/help/dev/patterns/assets/configure-automatic-page-request.png){width="100" zoomable="yes"}

**Prerequisites**

* Not all data in the data layer must be sent to [!DNL Target]. You should have a discussion with the business team (digital marketing team) to determine what data is valuable for experimentation, optimization, and personalization. Only this data should be sent to [!DNL Target].
* Ensure that you do not send any Personally Identifiable Information (PII) data to [!DNL Target].

**Configure automatic page load request**

For more information, see [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Readings**

Learn about the `pageLoadEnabled` setting in [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Actions**

* Modify the `window.targetGlobalSettings` object to enable automatic page load requests.

+++

[Return to the diagram at the top of this page.](#diagram)

## 1.4: Configure flicker handling {#flicker}

This step helps ensure that there is no page flicker when delivering experiences.

+++See details

![Configure flicker handling diagram](/help/dev/patterns/assets/flicker-handling.png){width="100" zoomable="yes"}

**Prerequisites**

* Have a discussion with the team responsible for web page performance regarding the pros and cons of controlling flicker using the default method used by at.js. You can search for design patterns that let you use custom flicker handling solution, such as loader animation. If you do not find a pattern, you can request a new pattern.

**Configure flicker handling**

For more information, see [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

Setting `bodyHidingEnabled` to `true` hides the entire page body while the page load request in progress. If you have not enabled the automatic page load request for any reason (data later not ready, for example), it is best to set this setting to `false`.

If you have disabled `bodyHidingEnabled` because you do not want to fire APLR and want to fire the page request later, or you do not need flicker handling, you must implement your own flicker handling. You can handle flicker two ways: hiding the sections under test or by showing a throbber on the sections under test.

**Readings**

* [How at.js manages flicker](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
* Learn about the bodyHiddenStyle and bodyHidingEnabled objects in [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Actions**

* Modify `window.targetGlobalSettings` object to set `bodyHiddenStyle` and `bodyHidingEnabled`.

+++

[Return to the diagram at the top of this page.](#diagram)

## 1.5: Configure data mapping {#data-mapping}

This step helps ensure that all the data that must be sent to [!DNL Target] is set.

+++See details

![Data mapping diagram](/help/dev/patterns/assets/data-mapping.png){width="100" zoomable="yes"}

**Prerequisites**

* The data layer should be ready with all the data that must be sent to [!DNL Target].
* Recommendations: enrich profile.
  * Pass entity.id to capture data for recently viewed criteria and items based on criteria based on last viewed product.
  * Pass entity.id to capture data for popularity criteria based on favorite category.
  * Profile attribute if custom criteria is based on it or used in inclusion rule filtering in any criteria.
* Recommendations: ingest product data.
  * Other entity parameters (reserved and custom) can be passed to ingest or update the product catalog in Recommendations.
  * The product catalog can also be updated by seeing entity feeds using the Target UI or API.

**Map data to [!DNL Target]**

For more information, see [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Readings**

* [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)
* [Plan and implement Recommendations](/help/dev/implement/recommendations/recommendations.md)
* [Set up your Recommendations catalog](/help/dev/implement/recommendations/recommendations.md)

**Actions**

* Use the `targetPageParams()` function to set all the required data that must be sent to [!DNL Target].

+++

[Return to the diagram at the top of this page.](#diagram)

## 1.6: Promotion {#promotion}

Add promoted items and control their placement in your Target Recommendations [designs](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

+++See details

**Available options**

* Promote by IDs
* [Promote by collection](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Promote by attribute](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Entity parameters required**

* Item attribute in promotion must be passed when using the "promote by attribute" option.

+++

[Return to the diagram at the top of this page.](#diagram)

## 1.7: Cart-based criteria {#cart}

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

## 1.8: Popularity-based criteria {#popularity}

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

## 1.9: Item-based criteria {#item}

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

## 1.10: User-based criteria {#user}

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

## 1.11: Custom criteria {#custom}

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

## 1.12: Provide attributes used in inclusion rules {#inclusion}

+++See details

**Readings**

* [Use dynamic and static inclusion rules](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[Return to the diagram at the top of this page.](#diagram)

## 1.13: Provide excludedIds {#exclude}

Pass entity IDs for entities that you want to exclude from your recommendations. For example, you can exclude items that are already in the shopping cart.

+++See details

**Readings**

* [Can I dynamically exclude an entity?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[Return to the diagram at the top of this page.](#diagram)

## 1.14: Pass the `entity.event.detailsOnly=true` parameter {#true}

Use entity attributes to pass product or content information to [!DNL Target Recommendations].

+++See details

**Readings**

* [Entity attributes](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=en){target=_blank}

+++

[Return to the diagram at the top of this page.](#diagram)

## 1.15: Configure remote data mapping (remote)

This step ensures that all the data that must be sent to [!DNL Target] is set.

+++See details

![Remote data mapping diagram](/help/dev/patterns/assets/remote-data-mapping.png){width="100" zoomable="yes"}

**Prerequisites**

* Data layer should be ready with all the data that must be sent to [!DNL Target].

**Set up data providers**

For more information, see [Data providers](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

**Readings**

[targetPageParams function](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Actions**

Use `targetPageParams()` function to set all the required data that must be sent to [!DNL Target].

+++

[Return to the diagram at the top of this page.](#diagram)

## 1.16: Load at.js {#web}

This step ensures that the at.js SDK library is loaded and initialized.

+++See details

![Load Adobe Target Web SDK diagram](/help/dev/patterns/assets/load-web-sdk.png){width="100" zoomable="yes"}

**Prerequisites**

* Download or ask your digital marketing team for the Web SDK library file called at.js 2.*x*

*Readings*

* [How Target works](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html){target=_blank}
* [How at.js works](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
* [Implement Target without a tag manager](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

**Actions**

Embed the at.js file on all your webpages where experimentation, optimization, personalization, and data collection must happen.

+++

[Return to the diagram at the top of this page.](#diagram)





























