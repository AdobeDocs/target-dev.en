---
keywords: implement, implementation, at.js, adobe experience platform web sdk, aep web sdk
description: Learn how to implement [!DNL Adobe Target] for client-side web using the [!DNL Adobe Experience Platform Web SDK] (AEP Web SDK) or the at.js JavaScript library.
title: How Do I Implement [!DNL Target] for Client-Side Web
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
---
# Overview: implement [!DNL Target] for client-side web

In a client-side implementation of [!DNL Adobe Target], [!DNL Target] delivers the experiences associated with an activity directly to the client browser. The browser decides which experience to display and displays it. With a client-side implementation, you can use a WYSIWYG editor, the [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC), or a non-visual interface, the [Form-based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), to create your activity and personalization experiences.

To implement [!DNL Target] client-side, you must use one of the following JavaScript libraries:

* [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)

  The [!UICONTROL Adobe Experience Platform Web SDK] lets you interact with the various services in the [!DNL Adobe Experience Cloud] (including [!DNL Target]) through the [!UICONTROL Adobe Experience Edge Network]. If you choose to migrate to the [!UICONTROL Adobe Experience Platform Web SDK], see [What is [!UICONTROL Adobe Experience Platform Web SDK]](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md).

* [[!DNL Target] at.js JavaScript library](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)

  The at.js JavaScript library improves page load times for web implementations, improves security, and provides better implementation options for single page applications. If you choose to migrate to at.js, see [How At.js Works](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) and [[!DNL Adobe Target] Skill Builder: Developer chat, migrate Adobe Target's mbox.js to at.js](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true).


See [Comparing the at.js library to the Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/adobe-target/web-sdk-atjs-comparison){target=_blank} to learn about the differences between the two implementation approaches.