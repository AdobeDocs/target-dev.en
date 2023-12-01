---
keywords: implement, implementing, setting up, setup, single profile update
description: Get data into [!DNL Target] using the single profile update API.
title: How Do I Get Data into [!DNL Target] Using the [!UICONTROL Single Profile Update API]?
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
---
# [!UICONTROL Single Profile Update API]

The [!DNL Adobe Target] [!UICONTROL Single Profile Update API] lets you send a profile update for a single user. The [!UICONTROL Single Profile Update API] is almost identical to the [!UICONTROL Bulk Profile Update API], but one visitor profile is updated at a time, inline with the API call instead of with a .cvs file. 

The [!UICONTROL Single Profile Update API] and is generally used when an update must occur in relation to a transaction occurring in a channel that has not implemented [!DNL Target]. For example, you want to update the profile of a single visitor who performs some offline action. Actions can include reaching a call center, a loan is funded, using a loyalty card in store, accessing a kiosk, and so forth.

## Resources:

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)
