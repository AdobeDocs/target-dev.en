---
title: Single-Page Application Implementation for the[!DNL Adobe Experience Platform Web SDK]
description: Learn how to create a single-page application (SPA) implementation of the [!DNL Adobe Experience Platform Web SDK]using [!DNL Target].
keywords: target;adobe target;xdm views; views;single page applications;SPA;SPA lifecycle;client-side;AB testing;AB;Experience targeting;XT;VEC
feature: AEP Web SDK
---

# Single-page application implementation 

[!DNL Adobe Experience Platform Web SDK] provides rich features that equip your business to execute personalization on next-generation, client-side technologies such as single-page applications (SPAs).

Traditional websites used "Page-to-Page" navigation models, also called Multi Page Applications. In these websites designs are tightly linked to URLs, and moving between pages required a full page load. 

Modern web applications, such as single-page applications, have instead adopted a model that propels rapid use of browser UI rendering, which is often independent of page reloads. These experiences are triggered by customer interactions, such as scrolls, clicks, and cursor movements. As the paradigms of the modern web have evolved, the relevance of traditional generic events, such as a page load, to deploy personalization and experimentation no longer work.   

![Diagram showing the SPA lifecycle compared to traditional page lifecycle.](/help/dev/implement/client-side/aep-web-sdk/assets/spa-vs-traditional-lifecycle.png)

## Benefits of [!DNL Experience Platform Web SDK] for SPAs

Here are some benefits to using [!DNL Adobe Experience Platform Web SDK] for your single-page applications: 

* Ability to cache all offers on page-load to reduce multiple server calls to a single server call. 
* Improve the user experience on your site because offers are shown immediately via the cache without the lag time introduced by traditional server calls. 
* A single line of code and one-time developer setup enables marketers to create and run [!UICONTROL A/B Test] and [!UICONTROL Experience Targeting] (XT) activities via the [!UICONTROL Visual Experience Composer] (VEC) on your SPA. 

## XDM Views and single-page applications 

The [!UICONTROL Adobe Target] VEC for SPAs takes advantage of a concept called [!UICONTROL Views]: a logical group of visual elements that together make up an SPA experience. A single-page application can, therefore, be considered as transitioning through views, instead of URLs, based on user interactions. A [!UICONTROL View] can typically represent a whole site or grouped visual elements within a site. 

To further explain what Views are, the following example uses a hypothetical online e-commerce site implemented in [!DNL React] to explore example [!UICONTROL Views].  

After navigating to the home site, a hero image promotes an Easter sale as well as the newest products available on the site. In this case, a [!UICONTROL View] could be defined for the entire home screen. This [!UICONTROL View] could simply be called "home."

![Sample image of a single-page application in a browser window.](/help/dev/implement/client-side/aep-web-sdk/assets/example-views.png)

As the customer becomes more interested in the products that the business is selling, they decide to click the **Products** link. Similar to the home site, the entirety of the products site can be defined as a [!UICONTROL View]. This [!UICONTROL View] could be named "products-all." 

![Sample image of a single-page application in a browser window, with all products displayed.](/help/dev/implement/client-side/aep-web-sdk/assets/example-products-all.png)

Since a [!UICONTROL View] can be defined as a whole site or a group of visual elements on a site. The four products shown on the products site could be grouped and considered as a [!UICONTROL View]. This view could be named "products." 

![Sample image of a single-page application in a browser window, with example products displayed.](/help/dev/implement/client-side/aep-web-sdk/assets/example-products.png)

When the customer decides to click the **Load More** button to explore more products on the site, the website URL does not change in this case. However, a [!UICONTROL View] can be created here to represent only the second row of products that are shown. The [!UICONTROL View] name could be "products-page-2."

![Sample image of a single-page application in a browser window, with example products displayed on an additional page.](/help/dev/implement/client-side/aep-web-sdk/assets/example-load-more.png)

The customer decides to purchase a few products from the site and proceeds to the checkout screen. On the checkout site, the customer is given options to choose normal delivery or express delivery. A [!UICONTROL View] can be any group of visual elements on a site, so a [!UICONTROL View] could be created for delivery preferences and be called "Delivery Preferences."

![Sample image of a single-page application checkout page in a browser window.](/help/dev/implement/client-side/aep-web-sdk/assets/example-check-out.png)

The concept of [!UICONTROL Views] can be extended much further than this scenario. These scenarios are just a few examples of [!UICONTROL Views] that can be defined on a site.

## Implementing [!UICONTROL XDM Views] 

[!UICONTROL XDM Views] can be leveraged in [!DNL Target] to empower marketers to run A/B and XT tests on SPAs via the [!UICONTROL Visual Experience Composer]. Doing so requires performing the following steps to complete a one-time developer setup: 

1. Install [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview).
2. Determine all [!UICONTROL XDM Views] in your single-page application that you want to personalize.  
3. After defining the [!UICONTROL XDM Views], to deliver A/B or XT VEC activities, implement the `sendEvent()` function with `renderDecisions` set to `true` and the corresponding [!UICONTROL XDM View] in your Single Page Application. The [!UICONTROL XDM View] must be passed in `xdm.web.webPageDetails.viewName`. This step allows marketers to leverage the [!UICONTROL Visual Experience Composer] to launch A/B and XT tests for those XDM.  

    ```javascript
    alloy("sendEvent", { 
      "renderDecisions": true, 
      "xdm": { 
        "web": { 
          "webPageDetails": { 
          "viewName":"home" 
          }
        } 
      } 
    });
    ```
 
>[!NOTE] 
>
>On the first `sendEvent()` call, all [!UICONTROL XDM Views] that should be rendered to the end-user are fetched and cached. Subsequent `sendEvent()` calls with [!UICONTROL XDM Views] passed in are read from the cache and rendered without a server call. 
 
## `sendEvent()` function examples

This section outlines three examples showing how to invoke the `sendEvent()` function in React for a hypothetical e-commerce SPA. 

### Example 1: A/B test home page

The marketing team want to run A/B tests on the entire home page.

![Sample image of a single-page application in a browser window.](/help/dev/implement/client-side/aep-web-sdk/assets/use-case-1.png)

To run A/B tests on the whole home site, `sendEvent()` must be invoked with the XDM `viewName` set to `home`: 

```jsx
function onViewChange() { 
  
  var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash 

  viewName = viewName || 'home'; // view name cannot be empty 

  // Sanitize viewName to get rid of any trailing symbols derived from URL 

  if (viewName.startsWith('#') || viewName.startsWith('/')) { 
    viewName = viewName.substr(1); 
  }
   
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName":"home" 
        } 
      } 
    }
  }); 
} 

// react router v4 

const history = syncHistoryWithStore(createBrowserHistory(), store); 

history.listen(onViewChange); 

// react router v3 

<Router history={hashHistory} onUpdate={onViewChange} > 
```

### Example 2: Personalized products

The marketing team want to personalize the second row of products by changing the price label color to red after a user clicks **Load More**. 

![Sample image of a single-page application in a browser window, showing personalized offers.](/help/dev/implement/client-side/aep-web-sdk/assets/use-case-2.png)

```jsx
function onViewChange(viewName) { 

  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName
        }
      } 
    } 
  }); 
} 

class Products extends Component { 
  
  render() { 
    return ( 
      <button type="button" onClick={this.handleLoadMoreClicked}>Load more</button> 
    ); 
  } 

  handleLoadMoreClicked() { 
    var page = this.state.page + 1; // assuming page number is derived from component's state 
    this.setState({page: page}); 
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### Example 3: A/B test delivery preferences

The marketing team want to run an A/B test to see whether changing the color of the button from blue to red when **Express Delivery** is selected. The team thinks this change can boost conversions (as opposed to keeping the button color blue for both delivery options). 
 
![Sample image of a single-page application in a browser window, with A/B testing.](/help/dev/implement/client-side/aep-web-sdk/assets/use-case-3.png)

To personalize content on the site depending on which delivery preference is selected, a [!UICONTROL View] can be created for each delivery preference. When **Normal Delivery** is selected, the [!UICONTROL View] can be named "checkout-normal." If **Express Delivery** is selected, the [!UICONTROL View] can be named "checkout-express". 

```jsx
function onViewChange(viewName) { 
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName 
        }
      }
    }
  }); 
} 

class Checkout extends Component { 

  render() { 
    return ( 
      <div onChange={this.onDeliveryPreferenceChanged}> 
        <label> 
          <input type="radio" id="normal" name="deliveryPreference" value={"Normal Delivery"} defaultChecked={true}/> 
          <span> Normal Delivery (7-10 business days)</span> 
        </label> 
        <label> 
          <input type="radio" id="express" name="deliveryPreference" value={"Express Delivery"}/> 
          <span> Express Delivery* (2-3 business days)</span> 
        </label> 
      </div> 
    ); 
  } 

  onDeliveryPreferenceChanged(evt) { 
    var selectedPreferenceValue = evt.target.value; 
    onViewChange(selectedPreferenceValue); 
  } 

} 
```

## Using the [!UICONTROL Visual Experience Composer] for a SPA 

When you have finished defining your [!UICONTROL XDM Views] and implemented `sendEvent()` with those [!UICONTROL XDM Views] passed in, the VEC is able to detect these [!UICONTROL Views] and allow users to create actions and modifications for A/B or XT activities. 

>[!NOTE]
>
>To use the VEC for your SPA, you must install and activate either the [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) or [Chrome VEC Helper Extension](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension). 

### [!UICONTROL Modifications] panel 

The [!UICONTROL Modifications] panel captures the actions created for a particular [!UICONTROL View]. All actions for a [!UICONTROL View] are grouped under that [!UICONTROL View]. 

### Actions 

Clicking an action highlights the element on the site where this action is applied. Each VEC action created under a [!UICONTROL View] has the following icons: **Information**, **Edit**, **Clone**, **Move**, and **Delete**. These icons are explained in more detail in the table that follows.

|Icon|Description|
|---|---|
|Information|Displays the details of the action.|
|Edit|Allows you to edit the properties of the action directly. |
|Clone|Clone the action to one or more [!UICONTROL Views] that exist on the [!UICONTROL Modifications] panel or to one or more [!UICONTROL Views] that you have browsed and navigated to in the VEC. The action doesn't have to necessarily exist in the [!UICONTROL Modifications] panel.<br/><br/>**Note:** After a clone operation is made, you must navigate to the [!UICONTROL View] in the VEC via [!UICONTROL Browse] to see whether the cloned action was a valid operation. If the action cannot be applied to the [!UICONTROL View], you see an error.| 
|Move |Moves the action to a [!UICONTROL Page Load Event] or any other [!UICONTROL View] that already exists in the [!UICONTROL Modifications] panel.<br/><br/>**Page Load Event:** Any actions corresponding to the page load event are applied on the initial page load of your web application. <br/><br/>**Note:** After a move operation is made, you must navigate to the [!UICONTROL View] in the VEC via [!UICONTROL Browse] to see whether the move was a valid operation. If the action cannot be applied to the [!UICONTROL View], see an error.|
|Delete |Deletes the action.|

## Using the VEC for SPAs examples

This section outlines three examples for using the [!UICONTROL Visual Experience Composer] to create actions and modifications for A/B or XT activities.

### Example 1: Update "home" View

Earlier in this article a [!UICONTROL View] named "home" was defined for the entire home site. Now, the marketing team want to update the "home" view in the following ways:

* Change the **Add to Cart** and **Like** buttons to a lighter shade of blue. This change should happen during page load because it involves changing components of the header.
* Change the **Latest Products for 2026** label to **Hottest Products for 2026** and change the text color to purple. 

To make these updates in the VEC, select **Compose** and apply those changes to the "home" view. 

![Visual Experience Composer sample page.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-home.png)

### Example 2: Change product labels

For the "products-page-2" [!UICONTROL View], the marketing team would like to change the **Price** label to **Sale Price** and change the label color to red. 

To make these updates in the VEC, the following steps are required:

1. Select **Browse** in the VEC.
2. Select **Products** in the top navigation of the site.
3. Select **Load More** once to view the second row of products. 
4. Select **Compose** in the VEC. 
5. Apply actions to change the text label to **Sale Price** and the color to red. 

![Visual Experience Composer sample page with product labels.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-products-page-2.png)

### Example 3: Personalize delivery preference styling

[!UICONTROL Views] can be defined at a granular level, such as a state or an option from a radio button. Earlier in this article [!UICONTROL Views] were defined for delivery preferences, "checkout-normal" and "checkout-express." The marketing team wants to change the button color to red for the "checkout-express" View. 

To make these updates in the VEC, the following steps are required: 

1. Select **Browse** in the VEC. 
2. Add products to the cart on the site. 
3. Select the cart icon in the top right corner of the site. 
4. Select **Checkout your Order**. 
5. Select the **Express Delivery** radio button under **Delivery Preferences**. 
6. Select **Compose** in the VEC. 
7. Change the **Pay** button color to red. 

>[!NOTE]
>
>The "checkout-express" [!UICONTROL View] does not appear in the [!UICONTROL Modifications] panel until the **Express Delivery** radio button is selected. This is because the `sendEvent()` function is executed when the **Express Delivery** radio button is selected, therefore the VEC is not aware of the "checkout-express" [!UICONTROL View] until the radio button is selected.

![Visual Experience Composer showing delivery preferences selector.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-delivery-preference.png)
