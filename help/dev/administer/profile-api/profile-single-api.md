---
title: Adobe Target Single Profile Update API
description: Learn how to use [!DNL Adobe Target] [!UICONTROL Single Profile Update API] to send a single visitor's profile data to [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
---
# [!DNL Adobe Target Single Profile Update API]

The [!DNL Adobe Target] [!UICONTROL Single Profile Update API] lets you send a profile update for a single user. The [!UICONTROL Single Profile Update API] and is generally used when an update must occur in relation to a transaction occurring in a channel that has not implemented [!DNL Target].

The [!UICONTROL Single Profile Update API] is limited to performing 1 million updates in any rolling 24-hour period. Updates generally occur in under one hour, but might take as long as 24 hours to be reflected. If you must send more updates, or require updates to be processed in shorter time frames, consider sending transactional profile updates via client-side update (preferred), or via the [!DNL Adobe Target] server-side [Delivery API](/help/dev/implement/delivery-api/overview.md).

Specify the profile parameters in the format `profile.paramName=value`. 

To update the profile for a `pcId`, use:

``````
https://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr=0&profile.attr2=1...
``````

To update the profile for an `mbox3rdPartyId`, use:

``````
shell http://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mbox3rdPartyId=123456&profile.attr=0&profile.attr2=1...
``````

The [!UICONTROL Single Profile Update API] is for updates only. If nothing is found, a profile is not created.

## Notes

* Parameters and values must be URL-encoded using UTF-8.
* Parameter format is `profile.paramName`.
* Not all parameter values must exist for all pcIds and mbox3rdPartyIds.
* Parameters and values are case-sensitive.
* Both GET and POST are supported.
* The current size limitations for limit is 8 KB for GET and 60 KB for POST.

## Response

A sample response for the above requests looks like this: 

`trueRequest successfully submitted`

This response indicates that the response has been submitted and will be processed soon.