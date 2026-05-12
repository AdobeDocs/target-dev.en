---
keywords: global mbox, target classic, use global mbox from target classic
description: Learn how to use a legacy global mbox for your [!DNL Adobe Target] activities if you have already created a global mbox on your pages for your legacy implementations.
title: Can I Use a Global mbox from a Legacy Implementation?
feature: at.js
exl-id: fe608b5e-ff66-4ba2-a622-d4f7307a9ca9
TQID: https://experienceleague.adobe.com/BCubNDwB8gxZ9bpuCNhxcnFnjB1xQK8ZRkLveinPj4w
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
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# Use a Global mbox from a legacy implementation

By default, [!DNL Target] creates a global mbox called target-global-mbox, which is used to run activities created in [!DNL Target]. However, if you have already created a global mbox on your pages for your legacy implementations, you can use that mbox for your [!DNL Target] activities.

>[!NOTE]
>
>You can have only one global mbox per account.

To use your existing global mbox for both [!DNL Target] and your legacy implementation, you must set a few parameters. 

1. Go to [!DNL Target], then click **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

   By default, **[!UICONTROL Page load enabled (Auto-create global mbox]** is enabled, and the custom global mbox is named `target-global-mbox`.

1. If you want to use an existing mbox, disable **[!UICONTROL Page load enabled (Auto-create global mbox]**, and specify the name of a previously created global mbox in the **[!UICONTROL Global Mbox]** field.

   The Global Mbox drop-down lists all mboxes in your account. If you want to use an mbox that does not yet exist, create the mbox.

1. Click **[!UICONTROL Save]**.

   The settings for your account are updated.

1. Download the new at.js file and reference it on your site.

   All existing activities update to use the specified global mbox, including activities that have previously been created and implemented.

## Troubleshooting global mbox implementation

The following FAQs can be used to troubleshoot your global mbox implementation:

### Why is the global mbox not loading, or why is there latency in loading the global mbox when the page loads?

Make sure the at.js reference is the first JavaScript call on the page. For other solutions to this problem, see [Global mbox Frequently Asked Questions](/help/dev/implement/client-side/atjs/global-mbox/global-mbox-faq.md).
