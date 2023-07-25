---
title: Data collection
description: Ensure that all necessary tasks for data collection are executed in the correct sequence.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: yes
hidefromtoc: yes
---
# Data collection

Follow the steps in the *Data Collection* diagram to ensure that all necessary tasks needed for data collection are executed in the correct sequence.

>[!TIP]
>
>Click the images in this topic to expand to full screen.

## Collect data diagram {#diagram}

The step numbers in the following illustration correspond to the sections below.

![Data Collection diagram](/help/dev/patterns/assets/data-collection-diagram.png)

Click the following links to navigate to the desired sections:

* [2.1: Configure data mapping](#configure)
* [2.2 Link to Entity attributes](#entity-attributes)
* [2.3 Fire the Adobe Target Track API](#fire-api)

## 2.1: Configure data mapping {#configure}

This step helps ensure that all the data that needs to be send to [!DNL Adobe Target] is set.

+++See details

![Configure data mapping diagram](/help/dev/patterns/data-collection.md){width="100" zoomable="yes"}

**Prerequisites**

* Data layer should be ready with all the data that needs to be send to [!DNL Target].

**Readings**

[targetPageParams function](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Actions**

Use the `targetPageParams()` function to set all the required data that needs to be send to [!DNL Target].

+++

[Return to the diagram at the top of this page.](#diagram)

## 2.2: Link to Entity attributes {#entity-attributes}

Link to Entity attributes to update the product catalog for [!DNL Target Recommendations].

+++See details

**Readings**

* [Entity attributes](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Considerations**

* An alternate way to pass entity attributes is to update the product catalog to use [Recommendations product feeds](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank} in the Target UI.
* Passing entity attributes is applicable only on pages where product-catalog data is available in the data layer.
* Passing the `entity.event.detailsOnly=true` parameter in any call takes priority.

+++

[Return to the diagram at the top of this page.](#diagram)

## 2.3 Fire the Adobe Target Track API {#fire-api}

This step helps ensure that all the data that needs to be sent to [!DNL Target] is sent.

+++See details

![Fire Adobe Target Track API diagram](/help/dev/patterns/assets/fire-track-api.png){width="100" zoomable="yes"}

**Prerequisites**

* All data mapping must have been done using the [targetPageParams function](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Readings**

* [adobe.target.trackEvent() method](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)

**Actions**

Use [adobe.target.trackEvent() method](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) to send all data that needs to be sent to [!DNL Target].

+++

[Return to the diagram at the top of this page.](#diagram)
