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

## Initialize SDKs diagram {#diagram}

The step numbers in the following illustration correspond to the sections below. Click image to expand to full screen.

![Initialize SDKs diagram](/help/dev/patterns/assets/initialize-sdk.png){width="600" zoomable="yes"}


## 1. Load visitor API SDK

This step helps ensure that the `VisitorAPI.js` library is loaded, configured, and initialized correctly.

![Load Visitor API SDK diagram](/help/dev/patterns/assets/load-visitor-api-sdk.png){width="600" zoomable="yes"}

### Prerequisites

The following are prerequisites for performing this step:

* To use the Visitor ID/API service, your company must be enabled for the Adobe Experience Cloud and have an Organization ID. For more information, see [Experience Cloud Requirements: Organization ID](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html?){target=_blank} in the *Identity Service Help* guide.
* You need the VisitorAPI.js file. Reach out to your digital marketing team to get this file.

### Step 1: Configure and refer VisitorAPI.js

For more information, see [Implement the Experience Cloud Service for Target](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html){target=_blank}.

### Readings

The following links provide more information:

* [Experience Cloud Identity Service overview](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html){target=_blank}
* [About the ID Service](https://experienceleague.adobe.com/docs/id-service/using/intro/about-id-service.html){target=_blank}
* [Cookies and the Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html){target=_blank}
* [How the Experience Cloud Identity Service requests and sets IDs](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html){target=_blank}
* [Understanding ID synchronization and match rates](https://experienceleague.adobe.com/docs/id-service/using/intro/match-rates.html){target=_blank}

### Actions

Complete the following actions:

* Embed the `VisitorAPI.js` file on your webpages.
* Read about the [available configurations for the Visitor ID/API service](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html){target=_blank}.
* After the `VisitorAPI.js` file is loaded, use the `Visitor.getInstance` method to initialize using the necessary configurations you need.
* Familiarize yourself with all the [available methods](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html){target=_blank}.

[Return to the diagram at the top of this page.](#diagram)

## 2. Set Customer ID

This step helps ensure that your end users' known IDs (CRM ID, User ID, and so forth) are tied to the anonymous ID of Adobe for cross-device personalization.

![Set Customer ID](/help/dev/patterns/assets/set-customer-id.png){width="600" zoomable="yes"}

### Prerequisites

The following are prerequisites for performing this step:

* The end user's known ID should be available in the Data Layer.

### Step 2: Set Customer ID

For more information, see [setCustomerIDs](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html){target=_blank}.

### Readings

* [Real-time profile syncing for mbox3rdPartyId](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html){target=_blank}

### Actions

Complete the following actions:

* Use `visitor.setCustomerIDs` to set the end-user known ID.

[Return to the diagram at the top of this page.](#diagram)





