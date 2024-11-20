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
>
>All Edge4*x* addresses listed in both tables below are scheduled to be updated on August 9, 2023.

## Network Address Translation (NAT) IP addresses of [!DNL Target] edges

List of egress IP addresses of [!DNL Target] edges. Allowlist these IPs if you plan to have [!DNL Target] reach out to your services.

|Edge Location|Egress IP Addresses|
| --- | --- |
|Edge41 (Mumbai)|3.6.2.221<P>13.235.112.4 <P>52.66.66.192|
|Edge42 (Tokyo)|52.69.55.232<P>43.206.61.43 <P>13.113.73.214|
|Edge44 (East Coast US)|54.164.192.223<P>52.86.86.203 <P>54.88.167.98|
|Edge45 (West Coast US)|52.40.124.129<P>54.148.219.69 <P>54.189.208.212|
|Edge46 (Sydney)|54.253.144.4<P>54.66.198.142 <P>13.211.218.51|
|Edge47 (Ireland)|52.208.136.136<P>54.170.28.19 <P>99.80.111.82|
|Edge48 (Singapore)|3.1.141.36<P>18.143.112.116 <P>52.76.61.44|

## [!DNL Target] edge IP addresses

List of IP addresses of [!DNL Target] edges. Allowlist these IPs if you want to make API calls to [!DNL Target] edges.

This list will change often, as the load balancers scale up and down based on traffic profiles.

|Edge Location|Domain|IP Addresses|
| --- | --- | --- |
||`CLIENTCODE.tt.omtrdc.net`<br />(where CLIENTCODE is your [!DNL Target] client ID)||
|Edge41 (Mumbai)|`mboxedge41.tt.omtrdc.net`|3.6.2.221<P>52.66.66.192<P>13.235.112.4|
|Edge42 (Tokyo)|`mboxedge42.tt.omtrdc.net`|43.206.61.43<P>13.113.73.214<P>52.69.55.232|
|Edge44 (East Coast US)|`mboxedge44.tt.omtrdc.net`|54.88.167.98<P>54.164.192.223<P>52.86.86.203|
|Edge45 (West Coast US)|`mboxedge45.tt.omtrdc.net`|52.40.124.129<P>54.148.219.69<P>54.189.208.212|
|Edge46 (Sydney)|`mboxedge46.tt.omtrdc.net`|54.66.198.142<P>54.253.144.4<P>13.211.218.51|
|Edge47 (Ireland)|`mboxedge47.tt.omtrdc.net`|54.170.28.19<P>52.208.136.136<P>99.80.111.82|
|Edge48 (Singapore)|`mboxedge48.tt.omtrdc.net`|52.76.61.44<P>3.1.141.36<P>18.143.112.116|

As the load balancers detect changes in the traffic profile, it will scale up or down. The time required for Elastic Load Balancing to scale can range from 1 to 7 minutes, depending on the changes detected. When the load balancers scale, they update the DNS record with the new list of IP addresses. To ensure you are taking advantage of the increased capacity, Elastic Load Balancing uses a TTL setting on the DNS record of 60 seconds.
