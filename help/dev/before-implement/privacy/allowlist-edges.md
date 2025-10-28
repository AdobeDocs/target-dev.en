---
keywords: implement, implementing, whitelist, white list, allowlist, allow list, edge, edges, $9
description: View a list of hosts to help you allowlist [!DNL Adobe Target] edges (geographically distributed serving nodes that ensure optimum response times end users).
title: How Do I Allowlist [!DNL Target] Edge Nodes?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
---
# Allowlist [!DNL Target] edge nodes

Information and an up-to-date list of hosts to help you allowlist [!DNL Adobe Target] edges.

An edge is a geographically distributed serving architecture that ensures optimum response times for end-users requesting content, regardless of where they are located. Each edge node has all the information required to respond to the user's content request and to track analytics data on that request. User requests are routed to the nearest edge node. For more information, see [The edge network](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934).

You can allowlist [!DNL Target] edge nodes, if desired.

>[!IMPORTANT]
>
>In addition to allowlisting the Network Address Translation (NAT) IP addresses of [!DNL Target] edges and [!DNL Target] edge IP addresses discussed in the article, you should also allowlist all [!DNL Adobe Analytics] IP address blocks.
>
>For more information, see [All Adobe Analytics IP address blocks](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=en#all-adobe-analytics-ip-address-blocks){target=_blank} in the *Adobe Analytics tech notes* documentation.
>
>[!DNL Adobe Target] infrastructure is being updated and customers who want to allowlist addresses must use both sets of IPs. Failing to do so will impact customers using server-side or hybrid implementations where Target API calls for fetching experiences are originated from within a network behind a firewall that is configured to use an allowlist.

To ensure uninterrupted access to [!DNL Target] through the [!DNL Experience Edge Connector], customers can update their network configurations to allow traffic to the proxy service.

## Proxy service overview

* **Service Endpoint**: `https://tnt-web-proxy.adobe.io`.
* **Infrastructure**: Hosted on the [!DNL Adobe] Ethos platform.
* **Note**: This service uses latency-based DNS routing and does not rely on static IP addresses.

## CNAME targets

The proxy service routes traffic dynamically across multiple regions using CNAME records. These are the current targets:

|Edge Location|Egress IP Addresses|
| --- | --- |
|Region|CNAME Target|
|Europe (eu-west-1)|`ethos.pub.ethos11-prod-nld2.ethos.adobe.net`|
|US East (us-east-2)|`ethos.pub.ethos11-prod-va7.ethos.adobe.net`|
|US East (us-east-1)|`ethos.pub.ethos11-prod-aus5.ethos.adobe.net`|

## Recommended allowlist entries

To ensure reliable connectivity, allowlist the following hostnames:

* `ethos.pub.ethos11-prod-nld2.ethos.adobe.net`
* `ethos.pub.ethos11-prod-va7.ethos.adobe.net`
* `ethos.pub.ethos11-prod-aus5.ethos.adobe.net`

## Optional: IP discovery

If your network policies require IP-based allowlisting, you can view the current public IP addresses associated with the proxy service using this tool:

* `DNSChecker – A Record Lookup for tnt-web-proxy.adobe.io`