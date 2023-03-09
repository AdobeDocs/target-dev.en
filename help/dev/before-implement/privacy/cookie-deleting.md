---
keywords: cookie, cookies, delete cookie, delete [!DNL Target] cookie, google chrome, chrome, mozilla firefox, firefox, microsoft edge, safari, cookie1
description: Learn how to delete your [!DNL Target] browser cookies so that you can validate your experiences.
title: How Do I Delete the [!DNL Target] Cookie?
feature: Privacy & Security
role: Developer
---
# Delete the [!DNL Target] cookie

You can delete your [!DNL Adobe Target] browser cookie (mbox) so that you can validate all of your experiences during testing.

If there is no [!DNL Target] cookie (mbox), you are considered a new visitor and shown a new experience. There are several ways to delete your mbox without deleting all of your browser cookies.

>[!NOTE]
>
>The following instructions are correct for the browsers and versions listed. Search the internet for instructions for your specific browser or version.

## Delete the [!DNL Target] cookie from Google Chrome

Version 84.0.4147.105

1. Click the **[!UICONTROL Chrome]** menu > **[!UICONTROL Preferences]**.
1. Click the **[!UICONTROL Privacy and Security]** tab.
1. Click **[!UICONTROL Cookies and other site data]**.
1. Click **[!UICONTROL See all cookies and site data]**.
1. Expand the `adobe.com` section, select the **mbox** cookie, then click the delete icon (X).

## Delete the [!DNL Target] cookie from Mozilla Firefox

Version 79.0

### Delete all cookies associated with `adobe.com`

1. Click the **[!UICONTROL Firefox]** menu > **[!UICONTROL Preferences]**.
1. Click the **[!UICONTROL Privacy and Security]** tab. 
1. Under **Cookies and Site Data*, click **[!UICONTROL Manage Data]**.
1. Select the `adobe.com` site, then click **[!UICONTROL Remove Selected]**.

>[!WARNING]
>
>This deletes all cookies associated with the `adobe.com` site. If you want to delete an individual cookie for a site, follow the instructions below.

### Delete an individual cookie (mbox)

1. In Firefo, click **[!UICONTROL Tools]** > **[!UICONTROL Web Developer]** > **[!UICONTROL Storage Inspector]**.
1. Click the **[!UICONTROL Advanced]** tab.
1. Navigate to the webpage that holds the cookie you want to delete.
1. Expand the **[!UICONTROL Cookies]** section, then click `https://experience.adobe.com`.
1. Right-click the **[!UICONTROL mbox]** cookie, then click **[!UICONTROL Delete]**.

## Delete the [!DNL Target] cookie from Microsoft Edge

Version 84.0.522.52

1. Click the **[!UICONTROL Microsoft Edge]** menu > **[!UICONTROL Preferences]**.
1. Click the **[!UICONTROL Site Permissions]** tab.
1. Click **[!UICONTROL Cookies and site data]**.
1. Click **[!UICONTROL See all cookies and site data]**.
1. Expand the `adobe.com` section, select the **mbox** cookie, then click the delete icon (X).

## Delete the [!DNL Target] cookie from Apple Safari

Version 13.1.2

### Delete all cookies associated with `adobe.com`

1. Click the **[!UICONTROL Safari]** menu > **[!UICONTROL Preferences]**.
1. Click the **[!UICONTROL Privacy]** tab.
1. Click **[!UICONTROL Manage Website Data]**.
1. Select the sites for the cookies you want to delete, then click **[!UICONTROL Remove]**.

>[!WARNING]
>
>This deletes all cookies associated with the `adobe.com` site. If you want to delete an individual cookie for a site, follow the instructions below.

### Delete an individual cookie (mbox)

1. Click the **[!UICONTROL Safari]** menu > **[!UICONTROL Preferences]**.
1. Click the **[!UICONTROL Advanced]** tab.
1. Select the **[!UICONTROL Show Develop menu in menu bar]** option.
1. Navigate to the webpage that holds the cookie you want to delete.
1. Click the **[!UICONTROL Develop]** menu > **[!UICONTROL Show Web Inspector]**.
1. Click the **[!UICONTROL Storage]** tab.
1. Expand the **[!UICONTROL Cookies]** section, then click `www.adobe.com`.
1. Right-click the **mbox** cookie, then click **[!UICONTROL Delete]**.
