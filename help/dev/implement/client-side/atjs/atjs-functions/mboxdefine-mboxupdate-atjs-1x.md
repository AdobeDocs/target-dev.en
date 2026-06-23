---
keywords: mboxDefine, mboxdefine, mbox define, mboxUpdate, mboxupdate, mbox update, at.js, functions, function, mboxDefine0
description: Use the [!UICONTROL mboxDefine()] and [!UICONTROL mboxUpdate()] functions for the [!DNL Adobe Target] at.js JavaScript library to define or update an mbox. (at.js 1.x)
title: How Do I Use the [!UICONTROL mboxDefine()] And [!UICONTROL mboxUpdate()] Functions?
feature: at.js
exl-id: 0a7dbea2-1cbd-4a5b-ba68-4c76a88d65c4
TQID: https://experienceleague.adobe.com/Fn-Ej8jk2AMEn79tOtRoP9GQc36Ugy6FtXyn6x7jkmA
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
    internal-label: at.js
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
---
# [!UICONTROL mboxDefine()] and [!UICONTROL mboxUpdate()] - at.js 1.x

Define and update an mbox in [!DNL Adobe Target].

>[!NOTE]
>
>These functions are available for at.js versions 1.*x* only. These functions were deprecated with the release of at.js 2.*x*. These functions return default content if used with at.js 2.*x*.

`[!UICONTROL mboxDefine()]` and `[!UICONTROL mboxCreate()]` are tied to HTML DIV elements where the offer should be displayed. These HTML DIV elements should have the `mboxDefault` class. If the HTML elements won't have this class attached, you could see some noticeable flicker.

## mboxDefine

Creates an internal mapping between a nodeId and an mbox name, but does not execute the request. Used in conjunction with `[!UICONTROL mboxUpdate()]`. Built into at.js mostly to ease the transition from mbox.js (now deprecated) to at.js.

## mboxUpdate

Executes the request and applies the offer to the element identified by the `nodeId` in the `mboxDefine()`. Can also be used to update an mbox initiated by `[!UICONTROL mboxCreate]`. Built into at.js mostly to ease the transition from mbox.js (now deprecated) to at.js. `mboxDefine()`/ `mboxUpdate()` could be replaced by [adobe.target.getOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) and [adobe.target.applyOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md) using the selector option.

## Example

```javascript {line-numbers="true"}
<div id="someId" class="mboxDefault"></div> 
<script> 
 mboxDefine('someId','mboxName','param1=value1','param2=value2'); 
 mboxUpdate('mboxName','param3=value3','param4=value4'); 
</script>
```

