---
keywords: implement, implementing, implementation, adobe launch, launch, race, redirect, experience platform launch, platform launch, tags, adobe platform, implement2
description: Learn how to implement the [!DNL Adobe Target] at.js library using [!DNL Adobe Experience Platform], the preferred method to implement Target.
title: How Do I Implement [!DNL Target] using [!DNL Adobe Experience Platform]?
feature: Implement Server-side
exl-id: 0a325871-194a-479c-a3bf-294e3dde3e9a
---
# Implement [!DNL Target] using [!DNL Adobe Experience Platform]

Tags in [!DNL Adobe Experience Platform] are the next generation of tag management capabilities from [!DNL Adobe]. Tags give customers a simple way to deploy and manage the analytics, marketing, and advertising tags necessary to power relevant customer experiences.

>[!NOTE]
>
>Adobe Experience Platform Launch has been rebranded as a suite of data collection technologies in [!DNL Adobe Experience Platform]. Several terminology changes have rolled out across the product documentation as a result. Please refer to the following [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?) for a consolidated reference of the terminology changes.

The following table lists the various sources where you can get more information:

| Resource | Details |
|--- |--- |
|[Add Adobe Target](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/target.html#implement-solutions)|This tutorial provides step-by-step instructions to implement [!DNL Target] in a website with tags in [!DNL Adobe Experience Platform]. Topics include adding the at.js JavaScript library, firing the global mbox, adding parameters, and integrating with other solutions. This article is part of a larger tutorial that shows you how to implement Adobe Experience Platform, and other Adobe Experience Cloud solutions.|
|[Quickstart guide](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html)|Information about deploying and managing the analytics, marketing, and advertising tags necessary to power relevant customer experiences.|
|[Adobe [!DNL Target] extension overview](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html)|Information about implementing [!DNL Target] using [!DNL Adobe Experience Platform].|

## Advantages of implementing at.js using the [!DNL Target] extension

The following advantages apply only if you use tags in [!DNL Adobe Experience Platform] to implement at.js. For this reason, Adobe strongly suggests that you use tags in [!DNL Adobe Experience Platform] rather than a manual implementation of at.js.

* **Solves [!DNL Adobe Analytics] and [!DNL Target] race condition:** Because the [!DNL Analytics] call could be fired before the [!DNL Target] call, the [!DNL Target] call is not stitched to the [!DNL Analytics] call. This sequencing can lead to incorrect data. The [!DNL Target] extension ensures that the [!DNL Analytics] beacon call waits until the [!DNL Target] call completes, successfully or not. Using tags in [!DNL Adobe Experience Platform] solves the data inconsistency customers can experience when implementing manually.

  >[!NOTE]
  >
  >Use the Send Beacon action in the [!DNL Adobe Analytics] extension so that the [!DNL Analytics] call waits for the [!DNL Target] call. If you directly call `s.t()` or `s.tl()` using custom code, [!DNL Analytics] calls do not wait until [!DNL Target] calls are complete.

* **Prevents incorrect redirect offer handling:** If you have [!DNL Target] and [!DNL Analytics] on the page, and there is a redirect offer executed by Target, you can experience a situation in which the [!DNL Analytics] tracker fires a request when it shouldn't (because the user is being redirected to a different URL). If you implement [!DNL Target] and [!DNL Analytics] via tags in [!DNL Adobe Experience Platform], you'll not experience this issue. Using tags in [!DNL Adobe Experience Platform], [!DNL Target] instructs [!DNL Analytics] to abort the [!DNL Analytics] beacon request.
