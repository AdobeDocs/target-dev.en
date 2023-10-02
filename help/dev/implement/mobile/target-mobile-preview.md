---
keywords: qa, preview, preview link, mobile, mobile preview
description: Use mobile preview links to perform end-to-end QA for mobile app activities.
title: How Do I Use Mobile Preview Links in [!DNL Adobe Target] Mobile?
feature: Implement Mobile
exl-id: c0c4237a-de1f-4231-b085-f8f1e96afc13
---
# [!DNL Target] mobile preview

Use mobile preview links to perform easy end-to-end QA for mobile app activities and enroll yourself into different experiences using your device without any special test devices.

The mobile preview functionality lets you fully test your mobile app activities before launching them live.

## Prerequisites

1. **Use a supported version of the SDK:** The mobile preview feature requires that you download and install the appropriate version of the [!DNL Adobe Mobile SDK] in your corresponding apps.

   For instructions to download the appropriate SDK, see [Current SDK versions](https://developer.adobe.com/client-sdks/documentation/current-sdk-versions/){target=_blank} in the *[!DNL Adobe Experience Platform Mobile SDK]* documentation.

1. **Set up a URL scheme:** The preview link uses a URL scheme to open your app. Specify a unique URL scheme for the preview.

   For more information, see [Visual preview](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} in *Configure the Target extension in the Data Connection UI* in the *[!DNL Mobile SDK]* documentation.

   The following links contain more information:

   * **iOs**: For more information about setting URL schemes for iOS, see [Defining a custom URL scheme for your app](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target=_blank} on the *Apple Developer* website.
   * **Android**: For more information about setting URL schemes for Android, see [Create Deep Links to App Content](https://developer.android.com/training/app-links/deep-linking){target=_blank} on the *Android Developers* website.

1. **Set up the `collectLaunchInfo` API (i0S only)**

    For more information, see [Visual preview](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} in *Configure the Target extension in the Data Connection UI* in the *[!DNL Mobile SDK]* documentation.

## Generating a Preview Link

1. In the [!DNL Target] UI, click the **[!UICONTROL More Options]** icon (the vertical ellipsis), then select **[!UICONTROL Create Mobile Preview Link]**.

   ![alt image](assets/mobile-preview-create.png)

1. Select the activities that you want to preview, then click **[!UICONTROL Generate Mobile Preview Link]**.

   >[!NOTE]
   >
   >You can select only Form-Based [!UICONTROL A/B Test] and [!UICONTROL Experience Targeting] (XT) activities.

   ![alt image](assets/mobile-preview-select-activities.png)

1. Specify your app's URL scheme.

   Thw URL scheme must be the same as what is present in your iOS or Android app. Repeat this process separately for iOS and Android, if necessary.

   ![alt image](assets/mobile-preview-enter-url-scheme.png)

1. Click **[!UICONTROL Generate Mobile Preview Link]**, then copy the link.

   ![alt image](assets/mobile-preview-generate-and-copy.png)

## Preview on Your Device

Open the link in a mobile browser on a device where you have your app installed. This app can be the production app that you downloaded from the [!DNL Apple App Store] or the [!DNL Google Play Store]. The app doesn't need to be a special build. If you have an active preview link, you can view the experiences on the device.

1. Open the link in your mobile browser.

    Share the link that you copied in the previous section from the [!DNL Target] UI to your mobile device in a convenient way, for example using text, email, or [!DNL Slack].

    |![preview deep link 1](assets/mobile-preview-open-deeplink.png)|![preview deep link 2](assets/mobile-preview-open-app.png)|

    Your app opens and starts the [!DNL Target] [!UICONTROL Mobile Preview Mode]. 

1. Select the combination of experiences that you want to see, then click **[!UICONTROL Launch Experiences]**.

   |![mobile preview 1](assets/mobile-preview-experience-selection-1.png)|![mobile preview 2](assets/mobile-preview-experience-result-1-france.png)|![mobile preview 3](assets/mobile-preview-experience-result-1-shipfree.png)|
   |![mobile preview 4](assets/mobile-preview-experience-selection-2.png)|![mobile preview 5](assets/mobile-preview-experience-result-2-aus.png)|![mobile preview 6](assets/mobile-preview-experience-result-2-10off.png)|

## Limitations

* The view must load again for the new content to display after the **[!UICONTROL Launch Experiences]** button is clicked. The easiest way is to switch to a different screen and then come back to the screen where you are expecting the change to happen. 
* Mobile preview is not supported for Android versions earlier than API-19 (KitKat).
