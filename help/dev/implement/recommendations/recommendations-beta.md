---
keywords: Recommendations, settings, preferences, industry vertical, filter incompatible criteria, default host group, thumb base url, recommendations api token,
description: Learn how to implement [!UICONTROL Recommendations] activities in [!DNL Adobe Target].
title: How Do I Implement [!UICONTROL Recommendations] Activities?
feature: Recommendations
hidefromtoc: yes
hide: yes
exl-id: 0a9c9649-195b-44e2-987e-d02eaf98cc54
---
# Plan and implement [!UICONTROL Recommendations] 

Information to help you plan and implement [!DNL Adobe Target Recommendations]. 

>[!NOTE]
>
>In addition to this article, the [Adobe Target Business Practitioner Guide](https://experienceleague.adobe.com/en/docs/target/using/target-home){target=_blank} contains in-depth information about [Target Recommendations](https://experienceleague.adobe.com/en/docs/target/using/recommendations/recommendations){target=_blank}.

Before setting up your first [!UICONTROL Recommendations] activity in [!DNL Adobe Target], complete the following steps:

1. [Implement [!UICONTROL Target]](#implement-target) on the web and mobile app surfaces that you want to use for capturing user behavior and delivering recommendations.
1. [Set up your [!UICONTROL Recommendations] catalog](#set-up-your-recommendations-catalog) of products or content that you want to recommend to your users.
1. [Pass behavioral information and context](#pass-behavioral-information-and-context) to [!DNL Target Recommendations] to allow it to deliver personalized recommendations.
1. [Configure global exclusions](#configure-global-exclusions).
1. [Configure [!UICONTROL Recommendations] settings](#configure-recommendations-settings).
1. (Optional) [Administer [!UICONTROL Recommendations] using Admin APIs](#administer-recommendations-using-admin-apis).

## 1. Implement [!UICONTROL Target]

[!DNL Target Recommendations] requires you to implement the [!DNL Adobe Experience Platform Web SDK] or at.js 0.9.2 (or later). See the [[!UICONTROL Target] client-side implementation guides](../client-side/overview.md) for more information. 

## 2. Set up your [!UICONTROL Recommendations] catalog

To deliver high-quality recommendations, [!UICONTROL Target] must know about the products or content that you want to recommend. Catalogs typically include three types of information about recommended items. Suppose you are recommending movies. Include the following:

1. Data that you want to display to the user receiving the recommendation. For example, you can display the name of the movie and a URL for a thumbnail image of the movie poster.
1. Data that is useful for applying marketing and merchandising controls. For example, you can display the rating of the movie so that you do not recommend NC-17 movies.
1. Data that is useful for determining the similarity of items to other pieces of items. For example, you can display the genre of the movie and director of the movie.

[!UICONTROL Target] offers multiple integration options to populate your catalog. These options can be used in combination to update different items in the catalog or to update different item attributes on different frequencies.

|Method|What it is|When to use it|Additional information|
| --- | --- | --- | --- |
|Catalog feed|Schedule a feed (CSV, [!DNL Google] Product XML, or [!UICONTROL Analytics Product Classifications]) to be uploaded and ingested on a daily basis.|For sending information about multiple items at a time. For sending information that changes infrequently.|See [Feeds](https://experienceleague.adobe.com/en/docs/target/using/recommendations/entities/feeds).|
|Entities API|Call an API to send to-the-minute updates for a single item.|For sending updates as they happen about one item at a time. For sending information that changes frequently (for example price, inventory/stock level).|See the [Entities API developer documentation](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities).|
|Pass updates on the page|Send to-the-minute updates for a single item using JavaScript on the page or using the Delivery API.|For sending updates as they happen about one item at a time. For sending information that changes frequently (for example price, inventory/stock level).|See [Item views/product pages](#item-views-or-product-pages) below.|

Most customers should implement at least one feed. You can then choose to complement your feed with updates for frequently changed attributes or items using either the Entities API or on-the-page method.

## 3. Pass behavioral information and context

The behavioral information and context you should pass to [!UICONTROL Target] depends on the action your visitor is taking, which is often associated with the type of page your visitor is interacting with.

### Item views or product pages

On pages where a visitor is viewing a single item, such as a product detail page, you should pass the identity of the item the visitor is viewing. Also pass the most granular category of the item that the visitor is viewing, to allow filtering recommendations to the current category.

You can also pass certain quickly changing attributes on the product page itself. For example, you can pass the price (`value`) and inventory/stock level.

#### Pass price and inventory

```js {line-numbers="true"}
<script type="text/javascript">
function targetPageParams() { 
   return { 
      "entity": { 
         "id": "32323", 
         "categoryId": "running-shoes", 
         "value": 119.99, 
         "inventory": 329 
      } 
   } 
}
</script>
```

### Category views/category pages

On a category page, you likely want to restrict your recommendations to products or content within that category. To do so, ensure you pass the identity of the currently viewed category.

#### Pass current category

```js {line-numbers="true"}
function targetPageParams() { 
   return { 
      "entity": { 
         "categoryId": "running-shoes" 
      } 
   } 
}
```

### Cart adds/cart views/checkout pages

On a cart page, you can recommend items based on the contents of the visitor's current cart. To do so, pass the IDs of all items in the visitor's current cart using the special parameter `cartIds`.

#### Pass items currently in cart

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "cartIds": "352,223,23432,432,553"
      }
}
```

For more information about Cart-Based recommendations, see [Cart-Based](https://experienceleague.adobe.com/en/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key#cart-based) in the *[!DNL Adobe Target] Business Practitioner Guide*.

### Exclude items already in the visitor's cart

On pages throughout your site, you can exclude some items from recommendations. For example, you might not want to recommend items that are already in the visitor's current cart. To do so, pass the IDs of all items you want to exclude using the special parameter `excludedIds`.

#### Pass items to exclude

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "excludedIds": "352,223,23432,432,553"
      }
}
```

### Purchases/order confirmation pages

When a purchase event occurs, pass the identity of the purchased item or items. See [Track Conversions](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions) in the [How to Deploy at.js > Implement [!UICONTROL Target] without a tag manager](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md) article.

## 4. Configure global exclusions

Exclude any items on a global level that you never want recommended to a visitor. See [Exclusions](https://experienceleague.adobe.com/en/docs/target/using/recommendations/entities/exclusions) in the *[!DNL Adobe Target] Business Practitioner Guide*. 
 
## 5. Configure [!UICONTROL Recommendations] settings

Use settings to manage your [!UICONTROL Recommendations] implementation.

To access the **[!UICONTROL Recommendations Settings]** options, open [!DNL Target] in the [!DNL Adobe Experience Cloud], then click **[!UICONTROL Administration]** > **[!UICONTROL Recommendations]**.

![Recommendations Settings page](/help/dev/implement/recommendations/assets/recs-settings-new.png)

Configure the following options:

### [!UICONTROL Recommendations API Token]

The following options are available in the [!UICONTROL Recommendations API Token] section:

#### [!UICONTROL Client code]

The [!DNL Target] [!UICONTROL client code].

If you don't know your [!UICONTROL client code], in the [!DNL Target] user interface, click **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**. The [!UICONTROL client code] is shown in the [!UICONTROL Account Details] section.

#### Authentication token

The [!DNL Adobe Target] Admin APIs, including [!DNL Recommendations Admin] APIs, are secured by authentication to ensure that only authorized users use them to access [!DNL Adobe Target]. Use the [Adobe Developer Console](https://developer.adobe.com/console/home) to manage this authentication for all [!DNL Adobe Experience Cloud solutions], including [!DNL Adobe Target].

For more information, see [Configure authentication for Adobe Target APIs](/help/dev/before-administer/configure-authentication.md).

>[!WARNING]
>
>Use caution when generating a new authentication token. Generating a new token causes API calls using the current token to fail. Update any scripts or applications with the new generated authentication token.

### Criteria

Knowing your site's industry vertical helps Target choose criteria for your recommendations.

Criteria in [!DNL Recommendations] are rules that determine which products or content to recommend based on a predetermined set of visitor behaviors. Criteria can be based on popular trends, a visitor's current and past behaviors, or similar products and content. You can test multiple recommendation types against each other by adding multiple criteria.

For more information, see [Criteria](https://experienceleague.adobe.com/en/docs/target/using/recommendations/criteria/algorithms){target=_blank} in the *Adobe Target Business Practitioner Guide.*

The following settings are available in the [!UICONTROL Criteria] section:

#### [!UICONTROL Industry/Vertical]

The industry vertical is used to help categorize your recommendations criteria. This information helps members of your team find criteria that make sense for a particular page, such as criteria that are best for the shopping cart page or for a media page.

The following categories are available from the drop-down list:

* No Personalization
* Retail/Ecommerce
* Lead Generation/B2B/Financial Services
* Media/Publishing

#### [!UICONTROL Filter Incompatible Criteria]

Enable this option to show only those criteria where the selected page passes the required data. Not every criteria runs correctly on every page. The page or mbox must pass in `entity.id` or `entity.categoryId` for the current item/current category recommendations to be compatible. 

In general, it is best to show only compatible criteria. However, if you want incompatible criteria to be available for the activity, do not enable this option.

Adobe recommends that you disable this option if using a tag management solution.

For more information about this option, see [[!UICONTROL Recommendations] FAQ](https://experienceleague.adobe.com/en/docs/target/using/recommendations/recommendations-faq/recommendations-faq){target=_blank} in the *[!DNL Adobe Target] Business Practitioner Guide*.

### [!UICONTROL Product Catalog]

The following options are available in the [!UICONTROL Product Catalog] section:

#### [!UICONTROL Default Host Group]

Select your default host group.

The host group can be used to separate the available items in your catalog for different uses. For example, you can use host groups for Development and Production environments, different brands, or different geographies. By default, preview results in Catalog Search, Collections, and Exclusions are based on the default host group. (You can also select a different host group to preview results, by using the Environment filter.) By default, newly added items are available in all host groups unless an environment ID is specified when creating or updating the item. Delivered recommendations depend on the host group specified in the request.

If you don't see your products, make sure that you are using the correct host group. For example, if you set up your recommendation to use a staging environment and you set your host group to Staging, you might need to re-create your collections in the staging environment for the products to show. To see which products are available in each environment, use Catalog Search with each environment. You can also preview the contents of [!UICONTROL Recommendations] collections and exclusions for a selected environment (host group).

>[!NOTE]
>
>After changing the selected environment, you must click **[!UICONTROL Search]** to update the returned results.

The **[!UICONTROL Environment]** filter is available from the following places in the Target UI:

* Catalog Search (**[!UICONTROL Recommendations]** > **[!UICONTROL Catalog Search]**)
* Collections (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]**)
* Create Collection dialog box (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Create collection]**)
* Update Collection dialog box (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Edit]**)
* Create Exclusion dialog box (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Create exclusion]**)
* Update Exclusion dialog box (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Edit]**)

For more information, see [Hosts](https://experienceleague.adobe.com/en/docs/target/using/administer/hosts){target=_blank} in the *[!DNL Adobe Target] Business Practitioner Guide*.

#### [!UICONTROL Thumbnail Base]

Setting a base URL for your product catalog makes it possible to use relative URLs when specifying thumbnails of your products when passing in your thumbnail URL.

For example:

`"entity.thumbnailURL=/Images/Homepage/product1.jpg"`

sets a URL relative to the thumbnail base URL.

### [!UICONTROL Custom Attribute Key Configuration]

Base your recommendations on an item stored in the visitor's profile. For example, 'last item added to cart', or 'last video watched viewed 90% or more'.

Click **[!UICONTROL Add]** to create a new configuration, specify a name for the configuration, select the desire profile attribute, then click **[!UICONTROL Save]**.

## 6. (Optional) Administer [!UICONTROL Recommendations] using Admin APIs

See the [Use [!UICONTROL Recommendations] APIs](../../before-administer/recs-api/overview.md) hands-on guide to learn how to configure and use the [!UICONTROL Target] admin and delivery APIs for [!UICONTROL Recommendations].
