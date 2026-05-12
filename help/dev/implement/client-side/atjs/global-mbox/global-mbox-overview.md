---
keywords: global mbox, implement at.js
description: Learn about the global mbox in [!DNL Adobe Target], a name used to refer to the single server call made at the top of each web page in your [!DNL Target] implementation.
title: What Is a Global mbox?
feature: at.js
exl-id: 572c1dc6-5cdd-427a-9458-e5ec49990cf8
TQID: https://experienceleague.adobe.com/MXEGvHHY8tFMfS6bMHcZYaG9mZtOWEkuODKH24JifZI
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
# Understand the Global mbox

Information about the global mbox, a name used to refer to the single server call made at the top of each web page in your [!DNL Adobe Target] implementation.

 By default, the global mbox is named `target-global-mbox`. It can be renamed for your account, if necessary.

There are several differences between a regular mbox (non-global mbox) and the global mbox, including:

| Regular mbox | Global mbox |
|--- |--- |
|A regular mbox typically wraps around content with a `<DIV>` tag.|The global mbox is "empty" and does not wrap around any content.|
|Content from only one activity can be delivered in a regular mbox.|Content from multiple activities can be delivered in one response to a global mbox.|

If multiple activities are delivered via the global mbox or via multiple regular mboxes, Target [determines the priority](https://experienceleague.adobe.com/docs/target/using/activities/priority.html) by which the activity (or activities) are delivered to a web page.

Additional page-level data can be sent to [!DNL Target] along with the global mbox by using the `[!UICONTROL targetPageParams]` function. This is similar to the mbox parameter functionality. For more information, see [Passing Parameters to a Global mbox](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).
