---
title: Adobe Target Single Profile Update API
description: Learn how to use [!DNL Adobe Target] [!UICONTROL Single Profile Update API] to send a single visitor's profile data to [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 4e022db3-215f-461b-9222-38ce2f2dbc28
---
# [!DNL Adobe Target Single Profile Update API]

The [!DNL Adobe Target] [!UICONTROL Single Profile Update API] lets you send a profile update for a single user. The [!UICONTROL Single Profile Update API] is almost identical to the [!UICONTROL Bulk Profile Update API], but one visitor profile is updated at a time, inline with the API call instead of with a .cvs file. 

The [!UICONTROL Single Profile Update API] and is generally used when an update must occur in relation to a transaction occurring in a channel that has not implemented [!DNL Target]. For example, you want to update the profile of a single visitor who performs some offline action. Actions can include reaching a call center, a loan is funded, using a loyalty card in store, accessing a kiosk, and so forth.

Benefits of the [!UICONTROL Single Profile Update API] include:

* No limit on the number of profile attributes.
* Profile attributes sent via the site can be updated via the API and the opposite way.

## Caveats

* The [!UICONTROL Single Profile Update API] is limited to performing 1 million updates in any rolling 24-hour period. 
* Updates generally occur in under one hour, but might take as long as 24 hours to be reflected. 

  If you must send more updates, or require updates to be processed in shorter time frames, consider sending transactional profile updates via client-side update (preferred), or via the [!DNL Adobe Target] server-side [Delivery API](/help/dev/implement/delivery-api/overview.md).

* The [!UICONTROL Single Profile Update API] is a server-to-server API and is not designed to work within a webpage. To update a visitor profile from within your webpage, you can use the [trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) function or the [Delivery API](/help/dev/implement/delivery-api/overview.md).

## Format

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
