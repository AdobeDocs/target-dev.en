---
keywords: mobile app,aep sdk,native app,web views,native;swift,adobe experience platform mobile sdk,mobile sdk,native code
description: Learn how to implement [!DNL Adobe Target] with the [!DNL AEP Mobile SDK] in a native app with web views.
title: Implement [!DNL Adobe Target] in a mobile app that uses native code with web views
feature: Implement Mobile
role: Developer
---

# Implement [!DNL Target] with the [!DNL AEP Mobile SDK] in a native app with web views

This article shares best practices for implementing [!DNL Adobe Target] in a mobile app that uses native code with web views using the [!DNL Adobe Experience Platform Mobile SDK]. 

This article uses a sample iOS app using the [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/getting-started/){target=_blank} and a [!DNL Target] integration written in [Swift from the GitHub repository](https://github.com/adobe/aep-sdk-app/){target=_blank}.

In the real world, your enterprise app is likely using web views in your mobile app. A web view is a container that loads a web page using a URL. The container is similar to a browser window without controls. In iOS, the web view container works as a Safari browser when processing web pages.

## Prerequisites

To get started with the [!DNL Adobe Experience Platform Mobile SDK], you must perform some prerequisite tasks. 

For more information, see [Adobe Target](https://developer.adobe.com/client-sdks/documentation/adobe-target/){target=_blank} in the [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/){target=_blank} documentation.

## Sync native code with web views

The challenge when implementing [!DNL Target] in a native app with web views is that the [!DNL Adobe Experience Platform Mobile SDK] has already generated all necessary identifiers required for [!DNL Adobe] solutions to work seamlessly. However, the identifies are not yet visible to the web views because those identifiers are not on the native platform environment. Therefore, you must create a bridge to pass some SDK identifiers to the web views so that the visitor identity persists into the web environment. The failure to do this properly results in duplicate visits, which affects your reporting.

Fortunately, the [!DNL Adobe Experience Platform Mobile SDK] provides a convenient method to generate [!DNL Adobe] parameters required for web views to consume and persist for the same visitor, shown in the following sample code:

```swift
Identity.appendTo(url: URL(string: url), completion: {appendedURL, error in
  print("appendedURL \(String(describing: appendedURL))")
  // load the url with ECID on the main thread
  DispatchQueue.main.async {
    let request = NSMutableURLRequest(url: appendedURL!)
    self.webView.load(request as URLRequest)
  }
});
```

For more information about the `Identity.appendTo` method, and to see an example of how to use the method, see [Swift > Example](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/tabs/api-reference/){target=_blank} in the *Mobile SDK Documentation*.

Using `Identity.appendTo`, this URL:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2
```

transforms to:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg
```

As you can see, there is `adobe_mc` parameter appended to the URL. This parameter contains encoded values for:

* TS=1660667205: The current timestamp. This timestamp ensures that the web view does not receive expired values.
* MCMID=69624092487065093697422606480535692677: The [!UICONTROL Experience Cloud ID] (ECID). Also known as MID or [!UICONTROL Marketing Cloud ID] required for [!DNL Adobe] cross-solution visitor identification.
* MCORGID=EB9CAE8B56E003697F000101@AdobeOrg: The [!UICONTROL Adobe Organization ID].

The `Identity.getUrlVariables` is an alternative [!DNL Adobe Experience Platform Mobile SDK] method that returns an appropriately formed string that contains the [!DNL Experience Cloud Identity Service] URL variables. For more information, see [getUrlVariables](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#geturlvariables){target=_blank} in the *Identity API reference*.

## Pass the [!DNL Target] Session ID for same-session experience

One extra step is needed to make the [!DNL Target] user journey work seamlessly across the native and web views. This step includes extracting and passing the [!DNL Target] Session ID from the [!DNL Adobe Experience Platform Mobile SDK] to the web views of the mobile app.

The `Target.getSessionId` extracts the Session ID that can be passed to the web view URL as an `mboxSession` parameter:

```swift
Target.getSessionId { (id, err) in
    // read Target sessionId
}
```

## Test in the web views

Web preview links are generated on the [!UICONTROL Activity detail] page by clicking the [[!UICONTROL Adobe QA] link](/help/dev/implement/mobile/target-mobile-preview.md) to display a pop-up to copy each experience preview link, similar to the following:

```
?at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Web preview links contain additional `at_preview_index` and `at_preview_listed_activities_only` parameters. Copy these parameters to construct mobile-friendly preview links with web link parameters. 

For example:

```
com.adobe.targetmobile://?at_preview_token=mhFIzJSF7JWb-RsnakpBqhBwj-TiIlZsRTx_1QQuiXLIJFdpSLeEZwKGPUyy57O_&at_preview_index=1_1&at_preview_listed_activities_only=true
```

After opening the link in an iOS Safari browser, your app captures the URL in your `AppDelegate` class similar to the following example:

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
  print("url= \(String(describing: url.absoluteString))")
  //...
```

Now that you have captured all necessary parameters in the app, you can pass them to the web when necessary:

```swift
Identity.appendTo(url: URL(string: url), completion: {appendedURL, error in
  let urlWithWebPreviewLink = appendedURL + "&" + myPreviewLinkFromAppDelegate
```

The final output for the web view link might look like this:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg&at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```
