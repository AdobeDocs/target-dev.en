---
keywords: implement, implementing, setting up, setup, single profile update
description: Get data into [!DNL Target] using the single profile update API.
title: How Do I Get Data into [!DNL Target] Using the Single Profile Update API?
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
---
# Single profile update API

Almost identical to the [!UICONTROL Bulk Profile Update API] in [!DNL Adobe Target], but one visitor profile is updated at a time, in line in the API call instead of with a .csv file.

## Format

The visitor must be identified via the [!DNL Target] mboxPC value or `mbox3rdPartyId` value. The Experience Cloud ID (ECID) is not supported.

## Example Use Cases

You want to update the profile of a single visitor who performs some offline action. Actions can include reaching a call center, a loan is funded, using a loyalty card in store, accessing a kiosk, and so forth.

## Benefits of method

No limit on the number of profile attributes.

Profile attributes sent via the site can be updated via the API and vice versa.

## Caveats

Limit of 1,000,000 API calls (1 million) per 24-hour period

Updates profiles only. Cannot create a profile for a potential user [!DNL Target] has yet to see.

Updates generally occur in under one hour, but may take as long as 24 hours to be reflected.

## Code examples

GET and POST supported. 

```
https://CLIENT.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr1=0&profile.attr2=1...
```

## Resources

* [Updating Profiles](https://developers.adobetarget.com/api/#updating-profiles)
