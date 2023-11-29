---
keywords: implement, implementing, setting up, setup, bulk profile update api
description: Get data into [!DNL Target] using the [!UICONTROL Bulk Profile Update API].
title: How Do I Get Data into [!DNL Target] Using the [!UICONTROL Bulk Profile Update API]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
---
# Bulk Profile Update API

Via API, send a .csv file to [!DNL Adobe Target] with visitor profile updates for many visitors. Each visitor profile can be updated with multiple in-page profile attributes in one call.

This option is similar to [!UICONTROL customer attributes] with a few differences:

* [!UICONTROL Customer attributes] use an FTP upload. The [!UICONTROL Target Bulk Profile Update API] uses an HTTP POST API.
* [!UICONTROL Customer attribute] data can be shared with [!DNL Analytics]. [!UICONTROL Bulk Profile Update] is useable only in [!DNL Target].
* [!UICONTROL Customer attributes] support creating a profile for a user [!DNL Target] has not yet seen.
  * [!UICONTROL Bulk Profile Update API] v2: You need not specify all parameter values for each `pcId`. Profiles are created for any `pcId` or `mbox3rdPartyId` that is not found in [!DNL Target].
  * [!UICONTROL Bulk Profile Update API] v1: The [!UICONTROL Bulk Profile Update API] updates existing [!DNL Target] profiles only. If you are using v1, profiles are not created for missing `pcIds` or `mbox3rdPartyIds`. 
* [!UICONTROL Customer attributes] require the use of the [!UICONTROL Experience Cloud ID] (ECID) and the use of a source ID, such as the CRM ID or the Loyalty ID.
* The [!UICONTROL Bulk Profile Update API] requires either the TNT ID or the `mbox3rdPartyId`.
* You cannot send the following characters in `mbox3rdPartyID`: plus sign (+) and forward slash (/).

## Format

The .csv file must refer to each visitor via their [!DNL Target] PCID or `mbox3rdPartyId`. The [!UICONTROL Experience Cloud ID] (ECID) is not supported. All profile attributes/values are created and updated via the API. Format details are available in the API documentation.

## Example use cases

Your CRM or other internal system stores valuable data about your visitors that you want to consistently update into [!DNL Target], without exposing the profile data in your page implementation.

## Benefits of method

* No limit on the number of profile attributes.
* Profile attributes sent via the site can be updated via the API and the opposite way.

## Caveats

* The size of the batch file must be less than 50 MB. In addition, the total number of rows should not exceed 500,000 rows per upload.
* Updates generally occur in under one hour, but might take as long as 24 hours to be reflected.
* There is no limit on the number or rows that you can upload over a period of 24 hours in subsequent batches. However, the ingestion process might be throttled during business hours to ensure that other processes run efficiently.
* Consecutive [V2 batch update calls](https://developers.adobetarget.com/api/#updating-profiles) without mbox calls in between for the same `thirdPartyIds` override the properties updated in the first batch update call.

## Code examples

See [Updating Profiles](https://developers.adobetarget.com/api/#updating-profiles).

### Links to relevant information

[Updating Profiles](https://developers.adobetarget.com/api/#updating-profiles)
