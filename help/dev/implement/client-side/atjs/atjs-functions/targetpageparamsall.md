---
keywords: targetPageParamsAll, targetpageparamsall, PageParamsAll, pageparamsall, page params, page parameters, at.js, functions, function, targetPageParamsAll0
description: Use the [!UICONTROL targetPageParamsAll()] function for the [!DNL Adobe Target] at.js JavaScript library to attach parameters to all mboxes from outside of the request code.
title: How Do I Use the [!UICONTROL targetPageParamsAll()] Function?
feature: at.js
exl-id: 32045e60-6904-42a1-bf71-fd7e167a829f
---
# [!UICONTROL targetPageParamsAll()]

This method allows you to attach parameters to all mboxes from outside of the request code.

This is very useful for including the same set of parameters on multiple mbox calls. The function needs to be defined by the customer. It should return an array of parameters that will be passed to all mbox requests on the page. This function can be defined before at.js is loaded or in **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit]** > **[!UICONTROL Code Settings]** > **[!UICONTROL Library Header]**.

You can pass in parameters to target-global-mbox using the [!UICONTROL targetPageParamsAll()] function in any of the following ways:

* An ampersand-delimited list 
* An array 
* A JSON object

## Examples

Ampersand-delimited list (values must be URL encoded):

```javascript {line-numbers="true"}
function targetPageParamsAll() { 
    return "param1=value1&param2=value2&p3=hello%20world"; 
}
```

Array (values do not need to be URL encoded):

```javascript {line-numbers="true"}
targetPageParamsAll = function() { 
     return ["a=1", "b=2", "c=hello world"]; 
};
```

JSON (values do not need to be URL encoded):

```javascript {line-numbers="true"}
targetPageParamsAll = function() { 
  return { 
    "a": 1, 
    "b": 2, 
    "profile": { 
        "age": 26, 
        "country": { 
          "city": "San Francisco" 
        } 
      } 
  }; 
};
```
