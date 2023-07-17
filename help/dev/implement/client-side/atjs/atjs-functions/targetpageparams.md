---
keywords: targetPageParams, targetpageparams, pageParams, pageparams, page params, page parameters, at.js, functions, function, targetPageParams0
description: Use the [!UICONTROL targetPageParams()] function for the [!DNL Adobe Target] at.js JavaScript library to attach parameters to the global mbox from outside of the request code.
title: How Do I Use the [!UICONTROL targetPageParams()] Function?
feature: at.js
exl-id: 274e4d1f-843a-443b-ad98-7139dc4a13f8
---
# [!UICONTROL targetPageParams()] 

This method allows you to attach parameters to the global mbox from outside of the request code.

This function is very useful for including the same set of parameters on multiple mbox calls. The function needs to be defined by the customer. It should return an array of parameters that will be passed only to the global mbox request. This function can be defined before at.js is loaded or in **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit]** > **[!UICONTROL Library Header]**.

You can pass in parameters to target-global-mbox using the `[!UICONTROL targetPageParams()]` function in any of the following ways:

* An ampersand-delimited list 
* An array 
* A JSON object

## Examples

Ampersand-delimited list (values must be URL encoded):

```javascript {line-numbers="true"}
function targetPageParams() { 
    return "param1=value1&param2=value2&p3=hello%20world"; 
}
```

Array (values do not need to be URL encoded):

```javascript {line-numbers="true"}
targetPageParams = function() { 
     return ["a=1", "b=2", "c=hello world"]; 
};
```

JSON (values do not need to be URL encoded):

```javascript {line-numbers="true"}
targetPageParams = function() { 
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
