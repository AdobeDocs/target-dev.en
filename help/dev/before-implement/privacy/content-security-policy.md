---
keywords: content security policy, csp, at.js, whitelist, allowlist, flicker, pre-hide, pre-hiding, prehiding, content security policy0
description: Learn about the Content Security Policy (CSP) directives you should add when using [!DNL Adobe Target].
title: How Does [!DNL Target] Handle Content Security Policies (CSP)?
feature: Privacy & Security
exl-id: ec6942e5-36d8-4f88-b3d6-47f9eaca03a8
---
# Content Security Policy (CSP) directives

If you are using [Content Security Policy](https://en.wikipedia.org/wiki/Content_Security_Policy) (CSP) for your [!DNL Adobe Target] implementation, you should add the following CSP directives when using [at.js 2.1 or later](../../implement/client-side/atjs/target-atjs-versions.md):

* `connect-src` with `*.tt.omtrdc.net` allowlisted. Necessary to allow the network request to the [!DNL Target] edge.
* `style-src unsafe-inline`. Required for pre-hiding and flicker control.
* `script-src unsafe-inline`.  Required to allow JavaScript execution that might be part of an HTML offer.

## Frequently Asked Questions (FAQs)

Consult the following FAQs about security policies:

### Do Cross Origin Resource Sharing (CORS) and Flash Cross-domain policies present security issues?

The recommended way of implementing the CORS policy is to permit access to only trusted origins that require it via an allowlist of trusted domains. The same can be said for the Flash Cross-domain policy. Some [!DNL Target] customers are concerned about the use of wildcard characters for domains in Target. The concern is that If a user is logged in to an application, and visits a domain allowed by the policy, any malicious content running on that domain can potentially retrieve sensitive content from the application and carry out actions within the security context of the logged in user. This is commonly referred to as Cross-Site Request Forgery (CSRF).

In a [!DNL Target] implementation, however, these policies should not represent a security issue.

"adobe.tt.omtrdc.net" is an Adobe-owned domain. [!DNL Adobe Target] is a testing and personalization tool and it is expected that [!DNL Target] can receive and process requests from anywhere without requiring any authentication. These requests contain key/value pairs that are used for A/B testing, recommendations, or content personalization.

Adobe does not store Personally Identifiable Information (PII) or other sensitive information on [!DNL Adobe Target] edge servers, to which "adobe.tt.omtrdc.net" points.

It is expected that [!DNL Target] can be accessed from any domain via JavaScript calls. The only way to allow this access is by leveraging "Access-Control-Allow-Origin" with a wildcard.

### How do I allow or prevent my site from being embedded as an iFrame under foreign domains?

To allow the [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank} (VEC) to embed your website in an iFrame, the CSP (if set) must be changed on your web server setting. [!DNL Adobe] domains must be whitelisted and configured.

For security reasons, you might want to prevent your site from being embedded as an iFrame under foreign domains. 

The following sections explain how to allow or prevent the VEC from embedding your site in an iFrame.

#### Allow the VEC to embed your site in an iFrame

The easiest solution to enable the VEC to embed your website in an iFrame is to allow `*.adobe.com`, which is the broadest wildcard. 

For example: 

`Content-Security-Policy: frame-ancestors 'self' *.adobe.com`

As in the following illustration (click to enlarge):


![CSP with broadest wildcard](/help/dev/before-implement/privacy/assets/csp-adobe.png){width="600" zoomable="yes"}

You might want to allow only the actual [!DNL Adobe] service. This could be achieved by using `*.experiencecloud.adobe.com + https://experiencecloud.adobe.com`. 

For example:

`Content-Security-Policy: frame-ancestors 'self' https://*.experiencecloud.adobe.com https://experiencecloud.adobe.com https://experience.adobe.com`

As in the following illustration (click to enlarge):

![CSP with ExperienceCloud scoped](/help/dev/before-implement/privacy/assets/csp-experiencecloud.png){width="600" zoomable="yes"}

The most restrictive access to a company's account can be achieved by using `https://<Client Code>.experiencecloud.adobe.com https://experience.adobe.com`, where `<Client Code>` represents your specific client code. 

For example:

`Content-Security-Policy: frame-ancestors 'self'  https://ags118.experiencecloud.adobe.com https://experience.adobe.com`

As in the following illustration (click to enlarge):

![CSP with clientcode scoped](/help/dev/before-implement/privacy/assets/csp-experiencecloud.png){width="600" zoomable="yes"}

>[!NOTE]
>
>If you have [Launch/Tag](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) implemented, it must be unlocked as well. 

For example:
>
> `Content-Security-Policy: frame-ancestors 'self' *.adobe.com *.assets.adobedtm.com;`

#### Prevent the VEC from embedding your site in a iFrame

To prevent the VEC from embedding your site in an iFrame, you can restrict to "self" only.

For example:

`Content-Security-Policy: frame-ancestors 'self'`

As shown in the following illustration (click to enlarge):

![CSP error](/help/dev/before-implement/privacy/assets/csp-error.png){width="600" zoomable="yes"}

The following error message is displayed:

`Refused to frame 'https://kuehl.local/' because an ancestor violates the following Content Security Policy directive: "frame-ancestors 'self'".`

