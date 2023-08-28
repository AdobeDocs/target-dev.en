---
keywords: adobe.target.applyOffer, applyOffer, applyoffer, apply offer, at.js, functions, function, $8
description: Use the [!UICONTROL adobe.target.applyOffer()] function for the [!DNL Adobe Target] at.js JavaScript library to apply the response content.
title: How Do I Use the [!UICONTROL adobe.target.applyOffer()] Function?
feature: at.js
exl-id: 957bbe92-8012-4bd5-95d6-1ae38b72bb16
---
# [!UICONTROL adobe.target.applyOffer(options)]

This function is for applying the response content with [!DNL Adobe Target].

>[!NOTE]
>
>`applyOffer` requires the `mbox` parameter. If no mbox name is specified, an error occurs.

The options parameter is mandatory and has the following structure:

| Key | Type | Required | Description |
|--- |--- |--- |--- |
|mbox|String|Yes|Mbox name<br />With at.js 1.3.0 (and later) Target enforces that the mbox key is used. This key has been required in the past, but Target now enforces its use to ensure that Target has proper validation and customers are using the function correctly.|
|selector|String or DOM Element|No|HTML element or CSS selector used to identify the HTML element where Target should place the offer content. If selector is not provided, Target assumes that the HTML element should use HTML HEAD.|
|Offer|Array|Yes|An array actions that should be applied to the element.|

## Example

The following example shows how to use `[!UICONTROL getOffer]` and `[!UICONTROL applyOffer]` together:

```javascript {line-numbers="true"}
adobe.target.getOffer({   
  "mbox": "mbox",   
  "success": function(offers) {           
        adobe.target.applyOffer( {  
           "mbox": "mbox", 
           "offer": offers  
        } ); 
  },   
  "error": function(status, error) {           
      if (console && console.log) { 
        console.log(status); 
        console.log(error); 
      } 
  }, 
 "timeout": 5000 
}); 
```
