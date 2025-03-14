---
keywords: Browsers, Prerequisites, Requirements, internet explorer, chrome, firefox, safari, android, surface, Browsers0
description: Learn which internet browsers [!DNL Adobe Target] supports for its interface and for content delivery.
title: What Browsers Does [!DNL Target] Support?
feature: Implementation
exl-id: 1d778e14-26b0-477b-ac28-d304db70a133
---
# Supported browsers

The [!DNL Adobe Target] application and content delivery has been tested across a wide range of browsers and devices.

For more important information about TLS, see [TLS (Transport Layer Security) Encryption Changes](tls-transport-layer-security-encryption.md).

## [!DNL Target] Standard/Premium interface

The [!DNL Target] interface supports the following browsers and devices:

>[!NOTE]
>
>Target supports the latest version of each listed browser and the latest version minus 1. 


| Device Type | Browser Version |
|--- |--- |
|[!DNL Windows]|<ul><li>[!DNL Microsoft Edge]</li><li>[!DNL Google Chrome]</li><li>[!DNL Mozilla Firefox]</li></ul>|
|[!DNL Mac]|<ul><li>[!DNL Microsoft Edge]</li><li>[!DNL Google Chrome]</li><li>[!DNL Mozilla Firefox]</li></ul>|

## Visual editing requirements 

To be able to open, author, and preview your web pages reliably in the [!UICONTROL Visual Experience Composer] (VEC), you must have the [Adobe Experience Cloud Visual Editing Helper browser extension](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension){target=_blank} installed on your web browser or use [!UICONTROL Enhanced Experience Composer (EEC)].

>[!NOTE]
>
>[!DNL Google Chrome] and [!DNL Microsoft Edge] are currently the only browsers that support visual editing of web pages in [!DNL Adobe Target].


## Content delivery

Content delivery has been tested across the following browsers and devices:

| Device Type | Browser Version |
|--- |--- |
|Windows|<ul><li>Microsoft Internet Explorer 9 and 10. Tested in emulation mode. **Note**: Content delivery on IE 9 is no longer supported with at.js 1.3.0 (and later). Content delivery on IE 10, 11, and all older versions is no longer supported with at.js 2.5.0 (and later).</li><li>Internet Explorer 11. **Note**: Content delivery on IE 10, 11, and all older versions is no longer supported with at.js 2.5.0 (and later).</li><li>Microsoft Edge</li><li>Chrome (latest, latest minus 1)</li><li>Firefox (latest, latest minus 1)</li></ul>|
|Mac|<ul><li>Apple Safari (Latest). **Note**: For more information about how Safari handles first- and third-party cookies, see [Target Cookie](../implement/client-side/atjs/atjs-cookies.md).</li><li>Firefox (latest, latest minus 1)</li><li>Chrome (latest, latest minus 1)</li></ul>|
|Mobile/Tablet|<ul><li>Apple iOS (latest)</li><li>Android devices and tablets (Android 4 and later)</li><li>Microsoft Surface (Windows 8.1)</li></ul>|

Note the following:

* The [!DNL Adobe Experience Platform Web SDK] is designed to work optimally in the latest versions of [!DNL Google Chrome], [!DNL Safari], [!DNL Firefox], and [!DNL Microsoft Edge Chromium]. You might have trouble using certain features on older versions of these browsers or deprecated browsers, such as [!DNL Internet Explorer].
* For at.js implementations, [!DNL Target] displays default content in earlier versions of Internet Explorer and possibly in earlier versions of the above-listed browsers.
* Internet Explorer treats all unknown elements (such as custom elements) as the same element type. As a result, delivery does not work with custom elements.
* [!DNL Target] displays default content in browsers not listed above and in browsers using [quirks mode](https://en.wikipedia.org/wiki/Quirks_mode). at.js requires a doctype that renders in standard mode, for example: `<!DOCTYPE html>` .
* [!DNL Adobe] Delivery infrastructure is being secured to NOT support TLS 1.0 devices and browsers after September 12, 2018. See [TLS (Transport Layer Security) Encryption Changes](../before-implement/tls-transport-layer-security-encryption.md) to understand the overall impact of this change.
