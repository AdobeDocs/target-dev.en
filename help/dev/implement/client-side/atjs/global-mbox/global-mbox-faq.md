---
keywords: troubleshooting, frequently asked questions, FAQ, FAQs, global, global mbox
description: Read frequently asked questions (FAQs) and answers about Adobe [!DNL Target] global mboxes.
title: What Are Frequently Asked Questions About the Global mbox?
feature: at.js
exl-id: 7bcd1b67-809a-466a-b648-6e0e44386157
TQID: https://experienceleague.adobe.com/bxsjCqSQpp6M20StzZtMBrfxjJCKgPEPfS2OlBUP00A
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
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
---
# Global mbox Frequently Asked Questions

List of Frequently Asked Questions (FAQs) about global mboxes.

## Can I have more than one global mbox if my [!DNL Target] account is set across multiple domains?

Only one global mbox is supported across your account.

You can limit where your activities run by adding URL rules to your activities. For more information, see [Include the Same Experience on Similar Pages](https://experienceleague.adobe.com/docs/target/using/experiences/vec/temtest.html).

You could also pass a parameter on the page using [targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) and then select those parameters in the "configure URL" section in the [!UICONTROL Visual Experience Composer] (VEC) or by adding the parameters as "refinements" in the [!UICONTROL Form-Based Experience Composer].

## How do I pass revenue data on a [!DNL Target] global mbox?

To collect revenue and order information on the target-global-mbox, "mbox parameters" must be sent to [!DNL Target]. These parameters are name/value pairs used to send more information to [!DNL Target]. [!DNL Target] automatically looks for these parameters (reserved names) to populate revenue data.

For the `orderConfirmPage`, you should pass in `orderTotal`, `orderId`, and `productPurchasedId`.

These parameters must be sent to the target-global-mbox via `targetPageParams()`. For more information, see [Passing Parameters to a Global mbox](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).

You'll also want to add targeting to the conversion piece so that [!DNL Target] only counts conversions on the target-global-mbox when the order confirmation page has been viewed, as shown below:

![alt image](assets/revenue1.png)

The Site Pages section illustrated above contains the following selections: Current Page, URL, contains, orderconfirm.

![alt image](assets/revenue2.png)

The options in the above illustration include the following settings:

* **What do you want to measure with this activity:** Revenue 
* **Default View for Reporting:** Revenue Per Visitor (RPV) 
* **What action was taken by your audience to indicate your goal has been reached?** Viewed an mbox, target-global-mbox
