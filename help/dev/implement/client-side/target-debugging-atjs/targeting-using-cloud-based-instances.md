---
keywords: cloud instances, public suffix list, public suffix, cookie, first-party cookie, 1st-party cookie, azurewebsites.net, cloudapp.net, amazonaws.com, cloudfront.net, herokuapp.com, firebaseapp.com, targetGlobalSettings, cookieDomain, cloud instances5, cloud instances6, cloud instances7, cloud instances8, cloud instances9, public suffix list0, public suffix list1, public suffix list2, public suffix list3, public suffix list4, public suffix list5
description: Explore issues (with solutions) customers face when using cloud-based instances to test [!DNL Adobe Target] or for proof-of-concept purposes.
title: Can I Use [!DNL Target] with Cloud-based Instances?
feature: at.js
exl-id: 4b24fdc0-6c74-4b29-bbf9-7a761d4564a2
---
# Use cloud-based instances with [!DNL Target]

Information about issues customers face when using cloud-based instances to test [!DNL Adobe Target].

[!DNL Target] customers sometimes use cloud-based instances with [!DNL Target] for testing or simple proof-of-concept purposes. These instances might include the following domains: 

`azurewebsites.net`, `cloudapp.net`, `amazonaws.com`, `cloudfront.net`, `herokuapp.com`, or `firebaseapp.com`

These domains, and many others, are part of the [Public Suffix List](https://publicsuffix.org/list/public_suffix_list.dat).

**Issue:** Modern browsers won't save cookies if you are using these domains.

The at.js JavaScript library uses cookies to track users to ensure that [!DNL [!DNL Target]] always presents a consistent experience. If the [!DNL Target] JavaScript library can't save cookies, Target requests are disabled.

**Solution:** As best practice, if you intend to use cloud-based instances with domains included on the Public Suffix List, make sure that you customize the `cookieDomain` setting. For more information, see [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).
