---
title: Initialize SDKs
description: Ensure that all necessary steps for loading the Adobe Experience Platform Web SDK is executed in the correct sequence.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: yes
hidefromtoc: yes
---
# Initialize SDKs

Follow the *Activity Initialize SDK* step diagram to ensure that all necessary steps leading up to the loading of the [!DNL Adobe Experience Platform Web SDK] are executed in the correct sequence.

>[!TIP]
>
>Click the images in this topic to expand to full screen.


## Initialize SDKs diagram {#diagram}

The step numbers in the following illustration correspond to the sections below. 

![Initialize SDKs diagram](/help/dev/patterns/assets/initialize-sdk.png){width="600" zoomable="yes"}

Click the following links to navigate to the desired sections:

* [1.1: Load visitor API SDK](#load)
* [1.2: Set Customer ID](#set)
* [1.3 Configure automatic page load request](#automatic)
* [1.4 Configure flicker handling](#flicker)
* [1.5 Configure data mapping](#data-mapping)
* [1.6 Promotion](#promotion)
* [1.7 Cart-based criteria](#cart)
* [1.8 Popularity-based criteria](#popularity)
* [1.9 Item-based criteria](#item)

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

![Set Customer ID](/help/dev/patterns/assets/set-customer-id.png){width="100" zoomable="yes"}

### Prerequisites

* The end user's known ID should be available in the Data Layer.

### Set Customer ID

For more information, see [setCustomerIDs](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html){target=_blank}.

### Readings

* [Real-time profile syncing for mbox3rdPartyId](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html){target=_blank}

### Actions

* Use `visitor.setCustomerIDs` to set the end-user known ID.

[Return to the diagram at the top of this page.](#diagram)

## 1.3: Configure automatic page load request {#automatic}

This step enables at.js to fetch all the experiences that need to be rendered on the page while loading the at.js JavaScript library file.

![Configure automatic page load request](/help/dev/patterns/assets/configure-automatic-page-request.png){width="100" zoomable="yes"}

### Prerequisites

* Not all data in the data layer needs to be sent to [!DNL Target]. You should have a discussion with the business team (digital marketing team) to determine what data is valuable for experimentation, optimization, and personalization. Only this data should be sent to [!DNL Target].
* Ensure that you do not send any Personally Identifiable Information (PII) data to [!DNL Target].

### Configure automatic page load request

For more information, see [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

### Readings

Learn about the `pageLoadEnabled` setting in [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

### Actions

* Modify the `window.targetGlobalSettings` object to enable automatic page load requests.

[Return to the diagram at the top of this page.](#diagram)

## 1.4: Configure flicker handling {#flicker}

This step helps ensure that there is no page flicker when delivering experiences.

![Configure flicker handling diagram](/help/dev/patterns/assets/flicker-handling.png){width="100" zoomable="yes"}

### Prerequisites

* Have a discussion with the team responsible for web page performance regarding the pros and cons of controlling flicker using the default method used by at.js. You can search for design patterns that let you use custom flicker handling solution, such as loader animation. If you do not find a pattern, you can request a new pattern.

### Configure flicker handling

For more information, see [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

Setting `bodyHidingEnabled` to `true` hides the entire page body while the page load request in in progress. If you have not enabled the automatic page load request for any reason (data later not ready, for example), it is bes to set this setting to `false`.

If you have disabled bodyHidingEnabled because you do not want to fire APLR and want to fire the page request later, or you do not need flicker handling, you must implement your own flicker handling. You can handle flicker two ways: hiding the sections under test or by showing a throbber on the sections under test.

### Readings

* [How at.js manages flicker](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
* Learn about the bodyHiddenStyle and bodyHidingEnabled objects in [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

### Actions

* Modify `window.targetGlobalSettings` object to set `bodyHiddenStyle` and `bodyHidingEnabled`.

[Return to the diagram at the top of this page.](#diagram)

## 1.5 Configure data mapping {#data-mapping}

This step helps ensure that all the data that needs to be sent to [!DNL Target] is set.

![Data mapping diagram](/help/dev/patterns/assets/data-mapping.png){width="100" zoomable="yes"}

### Prerequisites

* The data layer should be ready with all the data that needs to be sent to [!DNL Target].
* Recommendations: enrich profile.
  * Pass entity.id to capture data for recently viewed criteria and items based on criteria based on last viewed product.
  * Pass entity.id to capture data for popularity criteria based on favorite category.
  * Profile attribute if custom criteria is based on it or used in inclusion rule filtering in any criteria.
* Recommendations: ingest product data.
  * Other entity parameters (reserved and custom) can be passed to ingest or update the product catalog in Recommendations.
  * The product catalog can also be updated by seeing entity feeds using the Target UI or API.

### Map data to Target

For more information, see [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

### Readings

* [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)
* [Plan and implement Recommendations](/help/dev/implement/recommendations/recommendations.md)
* [Set up your Recommendations catalog](/help/dev/implement/recommendations/recommendations.md)

### Actions

* Use the `targetPageParams()` function to set all the required data that needs to be sent to [!DNL Target].

[Return to the diagram at the top of this page.](#diagram)

## 1.6 Promotion {#promotion}

Add promoted items and control their placement in your Target Recommendations [designs](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

### Available options

* Promote by IDs
* [Promote by collection](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Promote by attribute](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

### Entity parameters required

* Item attribute in promotion needs to be passed when using the "promote by attribute" option.

[Return to the diagram at the top of this page.](#diagram)

## 1.7 Cart-based criteria {#cart}

Make recommendations based on the user's [cart contents](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based){target=_blank}.

### Available criteria

* [!UICONTROL People Who Viewed These, Viewed Those]
* [!UICONTROL People Who Viewed These, Bought Those]
* [!UICONTROL People Who Bought These, Bought Those]

### Entity parameters required

* cartIds

[Return to the diagram at the top of this page.](#diagram)

## 1.8 Popularity-based criteria {#popularity}

Make recommendations based on the overall [popularity](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank} of an item across your site or based on the popularity of items within a user's favorite or most-viewed category, brand, genre, and so forth.

### Available algorithms

* [!UICONTROL Most Viewed Across the Site]
* [!UICONTROL Most Viewed by Category]
* [!UICONTROL Most Viewed by Item Attribute]
* [!UICONTROL Top Sellers Across the Site]
* [!UICONTROL Top Sellers by Category]
* [!UICONTROL Top Sellers by Item Attribute]
* [!UICONTROL Top by Analytics Metric]

### Entity parameters required

* `entity.categoryId` or the item attribute for popularity based if the criteria is based on the current or the item attribute. 
* Nothing needs to be passed for Most Viewed/Top sold across the site.

[Return to the diagram at the top of this page.](#diagram)

1.9 Item-based criteria {#item}

Make recommendations based on finding similar items to an item that the user is currently viewing or has recently viewed.

Available algorithm: 

* [!UICONTROL People Who Viewed This, Viewed That]
People Who Viewed This, Bought That
People Who Bought This, Bought That
Items with Similar Attributes
Entity Parameters Required
entity.id
if any profile attribute used as a key


















