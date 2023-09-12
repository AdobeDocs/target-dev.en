---
title: Configure data collection
description: Ensure that all necessary tasks for data collection are executed in the correct sequence.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: yes
hidefromtoc: yes
---
# Configure data collection

Follow the steps in the *Data Collection* diagram to ensure that all necessary tasks needed for data collection are executed in the correct sequence.

>[!TIP]
>
>Click the images in this topic to expand to full screen.

The data layer is ready during page load or the data layer change after page load.

If you have already mapped data during the [initialize SDK phase](/help/dev/patterns/recs-atjs/initialize-sdk.md), you must execute the steps in this diagram if:

* Your data layer is augmented in any way on the same page and you want to send that additional data to [!DNL Target]
* You want to send product-catalog data to [!DNL Target Recommendations]

## Collect data diagram {#diagram}

The step numbers in the following illustration correspond to the sections below.

![Data Collection diagram](/help/dev/patterns/recs-atjs/assets/data-collection-diagram.png){width="600" zoomable="yes"}

Click the following links to navigate to the desired sections:

* [2.1: Configure data mapping](#configure)
* [2.2 Link to Entity attributes](#entity-attributes)
* [2.3 Fire the Adobe Target Track API](#fire-api)

## 2.1: Configure data mapping {#configure}

This step helps ensure that all the data that must be sent to [!DNL Adobe Target] is set.

+++See details

![Configure data mapping diagram](/help/dev/patterns/recs-atjs/assets/cofigure-data-mapping.png){width="400" zoomable="yes"}

**Prerequisites**

* Data layer should be ready with all the data that must be sent to [!DNL Target].

**Readings**

[targetPageParams function](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Actions**

Use the `targetPageParams()` function to set all the required data that must be sent to [!DNL Target].

+++

[Return to the diagram at the top of this page.](#diagram)

## 2.2: Link to entity attributes {#entity-attributes}

Link to entity attributes to update the product catalog for [!DNL Target Recommendations].

+++See details

**Readings**

* [Entity attributes](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Considerations**

* An alternate way to pass entity attributes is to update the product catalog in the [!DNL Target] UI to use [Recommendations product feeds](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank}.
* Passing entity attributes is applicable only on pages where product-catalog data is available in the data layer.
* Passing the `entity.event.detailsOnly=true` parameter in any call takes priority.

+++

[Return to the diagram at the top of this page.](#diagram)

## 2.3 Fire the Adobe Target Track API {#fire-api}

This step helps ensure that all the data that must be sent to [!DNL Target] is sent.

+++See details

![Fire Adobe Target Track API diagram](/help/dev/patterns/recs-atjs/assets/fire-track-api.png){width="400" zoomable="yes"}

**Prerequisites**

* All data mapping must have been done using the [targetPageParams function](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Readings**

* [adobe.target.trackEvent() method](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)

**Actions**

Use [adobe.target.trackEvent() method](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) to send all data that must be sent to [!DNL Target].

+++

[Return to the diagram at the top of this page.](#diagram)

