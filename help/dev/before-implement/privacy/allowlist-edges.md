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
>This update is being made according to the following schedule:
>
>* May 22-26: Europe, Middle East, and Africa (EMEA) region
>* May 22-26: Asia-Pacific (APAC) region
>* June 6-10: Americas region

## Network Address Translation (NAT) IP addresses of [!DNL Target] edges

List of egress IP addresses of [!DNL Target] edges. Allowlist these IPs if you plan to have [!DNL Target] reach out to your services.

|Edge Location|Egress IP Addresses|
| --- | --- |
|Edge31 (Mumbai)|13.126.131.246<br />13.234.229.8|
|Edge32 (Tokyo)|3.115.154.28<br />3.115.227.146|
|Edge34 (East Coast US)|34.232.149.249<br />52.21.139.93|
|Edge35 (West Coast US)|52.10.11.139<br />44.231.171.161|
|Edge36 (Sydney)|13.237.227.20<br />13.210.93.142|
|Edge37 (Ireland)|54.72.21.68<br />52.208.139.19|
|Edge38 (Singapore)|18.141.132.96<br />54.179.187.167|
|Edge41 (Mumbai)|3.6.2.221<br />13.235.112.4 <br />52.66.66.192|
|Edge42 (Tokyo)|52.69.55.232<br />43.206.61.43 <br />13.113.73.214|
|Edge44 (East Coast US)|54.164.192.223<br />52.86.86.203 <br />54.88.167.98|
|Edge45 (West Coast US)|52.40.124.129<br />54.148.219.69 <br />54.189.208.212|
|Edge46 (Sydney)|54.253.144.4<br />54.66.198.142 <br />13.211.218.51|
|Edge47 (Ireland)|52.208.136.136<br />54.170.28.19 <br />99.80.111.82|
|Edge48 (Singapore)|3.1.141.36<br />18.143.112.116 <br />52.76.61.44|

## [!DNL Target] edge IP addresses

List of IP addresses of [!DNL Target] edges. Allowlist these IPs if you want to make API calls to [!DNL Target] edges.

This list will change often, as the load balancers scale up and down based on traffic profiles.

|Edge Location|Domain|IP Addresses|
| --- | --- | --- |
||`CLIENTCODE.tt.omtrdc.net`<br />(where CLIENTCODE is your [!DNL Target] client ID)||
|Edge31 (Mumbai)|`mboxedge31.tt.omtrdc.net`|13.235.211.15<br />35.154.193.2<br />35.154.53.50<br />15.206.4.195<br />13.234.45.112<br />3.7.14.31<br />3.7.182.1<br />52.66.52.225<br />3.6.64.110<br />65.0.222.85<br />65.1.67.35<br />43.205.52.220|
|Edge32 (Tokyo)|`mboxedge32.tt.omtrdc.net`|3.112.121.190<br />54.65.158.134<br />52.199.9.11<br />54.95.35.22<br />52.68.152.188<br />52.196.181.152<br />54.150.112.230<br />52.198.235.210|
|Edge34 (East Coast US)|`mboxedge34.tt.omtrdc.net`|44.195.255.231<br />52.207.142.243<br />52.54.50.225<br />35.169.35.160<br />52.71.135.138<br />35.169.227.120<br />23.22.33.42<br />52.54.152.40<br />54.243.116.94<br />3.233.250.116<br />50.16.29.53<br />54.86.98.238<br />44.210.41.177<br />3.211.200.163<br />54.210.15.1<br />34.199.251.113|
|Edge35 (West Coast US)|`mboxedge35.tt.omtrdc.net`|44.238.17.94<br />52.27.37.224<br />52.89.178.205<br />52.24.182.215<br />44.241.83.238<br />52.24.177.17<br />35.165.241.91<br />52.36.84.148<br />52.40.70.235<br />52.11.244.25<br />35.83.17.210<br />52.42.219.24<br />54.218.0.208<br />34.218.165.70<br />44.239.131.209<br />52.37.121.114<br />35.164.96.150<br />52.40.11.173<br />52.32.91.22<br />35.82.102.174<br />50.112.233.80<br />44.241.57.139<br />44.233.4.154<br />54.69.42.127<br />34.211.73.73<br />54.148.130.206<br />44.238.29.100<br />44.228.116.36<br />52.40.119.218<br />52.25.253.33|
|Edge36 (Sydney)|`mboxedge36.tt.omtrdc.net`|54.206.232.103<br />54.206.183.241<br />3.24.158.129<br />54.253.0.242|
|Edge37 (Ireland)|`mboxedge37.tt.omtrdc.net`|54.77.63.43<br />63.35.113.29<br />63.34.224.124<br />54.246.171.67<br />99.80.163.253<br />34.253.167.75<br />52.211.90.101<br />54.246.201.164<br />34.249.148.170<br />54.76.19.168<br />52.209.9.253|
|Edge38 (Singapore)|`mboxedge38.tt.omtrdc.net`|52.220.75.199<br />52.221.116.71|
|Edge41 (Mumbai)|`mboxedge41.tt.omtrdc.net`|15.206.104.6<br />3.109.14.178 <br />13.234.139.131|
|Edge42 (Tokyo)|`mboxedge42.tt.omtrdc.net`|52.194.84.34<br />3.115.158.39 <br />18.180.123.21|
|Edge44 (East Coast US)|`mboxedge44.tt.omtrdc.net`|54.205.210.54<br />23.20.189.8 <br />35.169.173.155|
|Edge45 (West Coast US)|`mboxedge45.tt.omtrdc.net`|35.161.163.45<br />44.230.114.101 <br />35.161.120.22|
|Edge46 (Sydney)|`mboxedge46.tt.omtrdc.net`|3.104.142.61<br />52.62.4.152 <br />54.253.105.140|
|Edge47 (Ireland)|`mboxedge47.tt.omtrdc.net`|18.203.168.186<br />54.228.83.91 <br />54.217.181.83|
|Edge48 (Singapore)|`mboxedge48.tt.omtrdc.net`|54.179.6.70<br />13.215.150.94 <br />18.136.47.70|

As the load balancers detect changes in the traffic profile, it will scale up or down. The time required for Elastic Load Balancing to scale can range from 1 to 7 minutes, depending on the changes detected. When the load balancers scale, they update the DNS record with the new list of IP addresses. To ensure you are taking advantage of the increased capacity, Elastic Load Balancing uses a TTL setting on the DNS record of 60 seconds.
