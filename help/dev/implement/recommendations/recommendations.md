---
keywords: Recommendations, settings, preferences, industry vertical, filter incompatible criteria, default host group, thumb base url, recommendations api token, $9
description: Learn how to implement [!UICONTROL Recommendations] activities in [!DNL Adobe Target].
title: How Do I Implement [!UICONTROL Recommendations] Activities?
feature: Recommendations
exl-id: af1e8b60-6dbb-451b-aa4f-e167d1800d1c
---
# Plan and implement [!UICONTROL Recommendations] 

Information to help you plan and implement [!DNL Adobe Target Recommendations].

>[!NOTE]
>
>In addition to this article, the [Adobe Target Business Practitioner Guide](https://experienceleague.adobe.com/docs/target/using/target-home.html){target=_blank} contains in-depth information about [Target Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html){target=_blank}.

Before setting up your first [!UICONTROL Recommendations] activity in [!DNL Adobe Target], complete the following steps:

1. [Implement [!UICONTROL Target]](#implement-target) on the web and mobile app surfaces that you want to use for capturing user behavior and delivering recommendations.
1. [Set up your [!UICONTROL Recommendations] catalog](#set-up-your-recommendations-catalog) of products or content that you want to recommend to your users.
1. [Pass behavioral information and context](#pass-behavioral-information-and-context) to [!DNL Target Recommendations] to allow it to deliver personalized recommendations.
1. [Configure global exclusions](#configure-global-exclusions).
1. [Configure [!UICONTROL Recommendations] settings](#configure-recommendations-settings).
1. (Optional) [Administer [!UICONTROL Recommendations] using Admin APIs](#administer-recommendations-using-admin-apis).

## 1. Implement [!UICONTROL Target]

[!DNL Target Recommendations] requires you to implement the Adobe Experience Platform Web SDK or at.js 0.9.2 (or later). See the [[!UICONTROL Target] client-side implementation guides](../client-side/overview.md) for more information.

## 2. Set up your [!UICONTROL Recommendations] catalog

To deliver high-quality recommendations, [!UICONTROL Target] must know about the products or content that you want to recommend. Catalogs typically include three types of information about recommended items. Suppose you are recommending movies. Include the following:

1. Data that you want to display to the user receiving the recommendation. For example, you can display the name of the movie and a URL for a thumbnail image of the movie poster.
1. Data that is useful for applying marketing and merchandising controls. For example, you can display the rating of the movie so that you do not recommend NC-17 movies.
1. Data that is useful for determining the similarity of items to other pieces of items. For example, you can display the genre of the movie and director of the movie.

[!UICONTROL Target] offers multiple integration options to populate your catalog. These options can be used in combination to update different items in the catalog or to update different item attributes on different frequencies.

|Method|What it is|When to use it|Additional information|
| --- | --- | --- | --- |
|Catalog feed|Schedule a feed (CSV, Google Product XML, or Analytics Product Classifications) to be uploaded and ingested on a daily basis.|For sending information about multiple items at a time. For sending information that changes infrequently.|See [Feeds](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html).|
|Entities API|Call an API to send to-the-minute updates for a single item.|For sending updates as they happen about one item at a time. For sending information that changes frequently (for example price, inventory/stock level).|See the [Entities API developer documentation](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities).|
|Pass updates on the page|Send to-the-minute updates for a single item using JavaScript on the page or using the Delivery API.|For sending updates as they happen about one item at a time. For sending information that changes frequently (for example price, inventory/stock level).|See [Item views/product pages](#item-views-or-product-pages) below.|

>[!IMPORTANT]
>
>Use caution when updating your [!DNL Recommendations] [!UICONTROL Catalog] via the [!DNL Delivery API]. The [!DNL Delivery API] is public, so avoid using it to populate clickable items in your recommendations catalog. Doing so can introduce invalidated content and pollute your catalog.
>
>**Best Practices**: Use the [!DNL Delivery API] only for updating catalog attributes that:
>
>* Change frequently (for example, price, stock level).
>
>* Follow a predefined format that can be easily validated on your website.
>
>* Do not use it for adding or modifying clickable items or other unverified content.
>
>* If needed, you can request customer support to disable catalog updates through the Delivery API.
>
>For more information, see the [[!UICONTROL Adobe Target Delivery API]](https://developer.adobe.com/target/implement/delivery-api/){target=_blank} documentation.

Most customers should implement at least one feed. You can then choose to complement your feed with updates for frequently changed attributes or items using either the Entities API or on-the-page method.

## 3. Pass behavioral information and context

The behavioral information and context you should pass to [!UICONTROL Target] depends on the action your visitor is taking, which is often associated with the type of page your visitor is interacting with.

### Item views or product pages

On pages where a visitor is viewing a single item, such as a product detail page, you should pass the identity of the item the visitor is viewing. You should also pass the most granular category of the item that the visitor is viewing, to allow filtering recommendations to the current category.

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

For more information about Cart-Based recommendations, see [Cart-Based](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based) in the *[!DNL Adobe Target] Business Practitioner Guide*.

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

When a purchase event occurs, pass the identity of the purchased item or items. See [Track Conversions](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions) in the the [How to Deploy at.js > Implement [!UICONTROL Target] without a tag manager](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md) article.

## 4. Configure global exclusions

Exclude any items on a global level that you never want recommended to a visitor. See [Exclusions](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/exclusions.html) in the *[!DNL Adobe Target] Business Practitioner Guide*. 
 
## 5. Configure [!UICONTROL Recommendations] settings

Use settings to manage your [!UICONTROL Recommendations] implementation.

To access the **[!UICONTROL Recommendations Settings]** options, open Target in the [!DNL Adobe Experience Cloud], then click **[!UICONTROL Recommendations]** > **[!UICONTROL Settings]**.

![Recommendations Settings page](/help/dev/implement/recommendations/assets/recs_settings.png)

The following options are available:

| Setting | Description |
|--- |--- |
|Custom Global Mbox|(Optional) Specify the custom global mbox used to serve [!UICONTROL Target] activities. By default, the global mbox used by [!UICONTROL Target] is used for [!UICONTROL Recommendations].<P>Note: This option is set on the [!UICONTROL Target] **[!UICONTROL Administration]** page. Open [!UICONTROL Target], then click **[!UICONTROL Administration]** > **[!UICONTROL Visual Experience Composer]**.|
|Industry Vertical|The industry vertical is used to help categorize your recommendations criteria. This information helps members of your team find criteria that make sense for a particular page, such as criteria that are best for the shopping cart page or for a media page.|
|Filter Incompatible Criteria|Enable this option to show only those criteria where the selected page passes the required data. Not every criteria runs correctly on every page. The page or mbox must pass in `entity.id` or `entity.categoryId` for the current item/current category recommendations to be compatible. In general, it is best to show only compatible criteria. However, if you want incompatible criteria to be available for the activity, uncheck this option.<P>It is recommended that you disable this option if using a tag management solution.<P>For more information about this option, see [[!UICONTROL Recommendations] FAQ](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html) in the *[!DNL Adobe Target] Business Practitioner Guide*.|
|Default Host Group|Select your default host group.<P>The host group can be used to separate the available items in your catalog for different uses. For example, you can use host groups for Development and Production environments, different brands, or different geographies. By default, preview results in Catalog Search, Collections, and Exclusions are based on the default host group. (You can also select a different host group to preview results, by using the Environment filter.) By default, newly added items are available in all host groups unless an environment ID is specified when creating or updating the item. Delivered recommendations depend on the host group specified in the request.<P>If you don't see your products, make sure that you are using the correct host group. For example, if you set up your recommendation to use a staging environment and you set your host group to Staging, you might need to re-create your collections in the staging environment for the products to show. To see which products are available in each environment, use Catalog Search with each environment. You can also preview the contents of [!UICONTROL Recommendations] collections and exclusions for a selected environment (host group).<P>**Note:** After changing the selected environment, you must click Search to update the returned results.<P> **[!UICONTROL The Environment]** filter is available from the following places in the Target UI:<ul><li>Catalog Search (**[!UICONTROL Recommendations]** > **[!UICONTROL Catalog Search]**)</li><li>Create Collection dialog box (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Create New]**)</li><li>Update Collection dialog box (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Edit]**)</li><li>Create Exclusion dialog box (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Create New]**)</li><li>Update Exclusion dialog box (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Edit]**)</li></ul>For more information, see [Hosts](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) in the *[!DNL Adobe Target] Business Practitioner Guide*.|
|Thumbnail Base URL|Setting a base URL for your product catalog makes it possible to use relative URLs when specifying thumbnails of your products when passing in your thumbnail URL.<P>For example:<P>`"entity.thumbnailURL=/Images/Homepage/product1.jpg"`<P>sets a URL relative to the thumbnail base URL.|
|[!UICONTROL Recommendations] API Token|Use this token in [!UICONTROL Recommendations] API calls, such as the Download API.|

## 6. (Optional) Administer [!UICONTROL Recommendations] using Admin APIs

See the [Use [!UICONTROL Recommendations] APIs](../../before-administer/recs-api/overview.md) hands-on guide to learn how to configure and use the [!UICONTROL Target] admin and delivery APIs for [!UICONTROL Recommendations].
