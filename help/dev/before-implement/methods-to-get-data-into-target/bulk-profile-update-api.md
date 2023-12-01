---
keywords: implement, implementing, setting up, setup, bulk profile update api
description: Get data into [!DNL Target] using the [!UICONTROL Bulk Profile Update API].
title: How Do I Get Data into [!DNL Target] Using the [!UICONTROL Bulk Profile Update API]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
---
# Bulk Profile Update API

The [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] lets you update user profiles for multiple visitors to a website in bulk using a batch file.

Using the [!UICONTROL Bulk Profile Update API], you can conveniently send detailed visitor profile data in the form of profile parameters for many users to [!DNL Target] from any external source. External sources can include Customer Relationship Management (CRM) or Point of Sale (POS) systems, which are not usually available on a web page.

Contrast the [!UICONTROL Bulk Profile Update API] with the [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## [!UICONTROL Customer attributes] versus the [!UICONTROL Bulk Profile Update API]

This option is similar to [[!UICONTROL customer attributes]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md) with a few differences:

* [!UICONTROL Customer attributes] use an FTP upload. The [!UICONTROL Target Bulk Profile Update API] uses an HTTP POST API.
* [!UICONTROL Customer attribute] data can be shared with [!DNL Analytics]. The [!UICONTROL Bulk Profile Update] is useable only in [!DNL Target].
* [!UICONTROL Customer attributes] support creating a profile for a user [!DNL Target] has not yet seen.
  * [!UICONTROL Bulk Profile Update API] v2: You need not specify all parameter values for each `pcId`. Profiles are created for any `pcId` or `mbox3rdPartyId` that is not found in [!DNL Target].
  * [!UICONTROL Bulk Profile Update API] v1: The [!UICONTROL Bulk Profile Update API] updates existing [!DNL Target] profiles only. If you are using v1, profiles are not created for missing `pcIds` or `mbox3rdPartyIds`. 
* [!UICONTROL Customer attributes] require the use of the [!UICONTROL Experience Cloud ID] (ECID) and the use of a source ID, such as the CRM ID or the Loyalty ID.
* The [!UICONTROL Bulk Profile Update API] requires either the TNT ID or the `mbox3rdPartyId`.
* You cannot send the following characters in `mbox3rdPartyID`: plus sign (+) and forward slash (/).

## Resources

For more information, see:

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)