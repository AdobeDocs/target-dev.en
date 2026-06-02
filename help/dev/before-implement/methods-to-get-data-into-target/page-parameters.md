---
keywords: implement, implementing, setting up, setup, page parameters
description: Get data into [!DNL Target] using page parameters.
title: How Do I Get Data into [!DNL Target] Using Page Parameters?
feature: Implementation
exl-id: 9bb7157e-a938-4150-8a15-c9bf0a0e2296
TQID: https://experienceleague.adobe.com/CYhZOFnli-DmREOOZGE2aGNn3x7BJ7uwGA2vfwUSnOk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
    internal-label: Audiences
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
---
# Page parameters

Page parameters (also called "mbox parameters") are name/value pairs passed in directly through page code that are not stored in the visitor's profile for future use.

Page parameters are useful to send page data to [!DNL Adobe Target] that does not need to be stored with the visitor's profile for future targeting use. These values are instead used to describe the page or the action the user took on the specific page.

## Format

Page parameters are passed into [!DNL Target] via a server call as a string name/value pair. Parameter names and values are customizable (although there are some "reserved names" for specific uses).

Here are some examples of page parameters

* `page=productPage`

* `categoryId=homeLoans`

## Example use cases

* **Product pages**: Send information about the specific product viewed (this method is how Recommendations works)
* **Order details**: Send order ID, orderTotal, and so forth, for order collection
* **Category affinity**: Send category-viewed information to [!DNL Target] to build knowledge of the user's affinity to particular site categories
* **3rd-party data**: Send information from 3rd-party data sources, such as weather targeting providers, account data (for example, DemandBase), demographic data (for example Experian), and more.

## Benefits of method

Data gets sent to [!DNL Target] in real time, and can be used on the same server call the data on which it comes in.

## Caveats

* Requires page code update (directly or via a tag management system).
* If the data must be used for targeting on a subsequent page/server call, it must be translated to a profile script.
* Query strings can contain only characters as per the [Internet Engineering Task Force (IETF) standard](https://www.ietf.org/rfc/rfc3986.txt) .

  In addition to those characters mentioned on the IETF site, [!DNL Target] allows the following characters in query strings:

  `< > # % " { } | \ ^ [ ] `
  
  Everything else must be url-encoded. The standard specifies the following format ( [https://www.ietf.org/rfc/rfc1738.txt](https://www.ietf.org/rfc/rfc1738.txt) ), as illustrated below:

  ![alt image](assets/ietf1.png)

  Or, the full list for simplicity:

  ![alt image](assets/ietf2.png)

## Code examples

targetPageParamsAll (appends the parameters to all mbox calls on the page):

`function targetPageParamsAll() { return "param1=value1&param2=value2&p3=hello%20world";`

targetPageParams (appends the parameters to the global mbox on the page):

`function targetPageParams() { return "param1=value1&param2=value2&p3=hello%20world";`

## Links to relevant information

Recommendations: [Implementation According to Page Type](https://experienceleague.adobe.com/docs/target/using/recommendations/plan-implement.html)

Order confirmation: [Track Conversions](../../implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions)

Category affinity: [Category Affinity](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/category-affinity.html)
