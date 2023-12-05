---
title: Fetch profiles
description: Learn how to use Adobe Target Profile APIs to fetch visitor data to use in [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
---
# Update profiles

A [!DNL Target] profile can be fetched in two ways: using a `tntid` or a `thirdPartyId`.

## Using a tntid

[!DNL Target] automatically assigns a `tntid` for every request.

The following example shows the request format to fetch a profile using a `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/your-tnt-id?client=<your-client-code>
```

Replace `<your-client-code>` and `your-tnt-id` and fire a GET request. Here is an example profile fetch call using a `tntid`;

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/111492025094307-353046?client=<your-client-code>
```

## Using a thirdPartyId

[!DNL Adobe Target] profiles can be augmented with your own identifier (for example: CRM id, `uuid`, membership number, and so forth). 

See [Update profiles](/help/dev/administer/profile-api/profile-api-overview.md) to learn how you can attach a `thirdPartyId` to your profile.

The following example shows the request format to fetch a profile using a `thirdPartyId`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/your-thirdpartyid?client=<your-client-code>
```

Replace `<your-client-code>` and `your-thirdpartyid` and fire a GET request. Here is an example profile fetch call using a [!UICONTROL thirdpartyid]:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/a1-mbox3rdPartyId?client=<your-client-code>
```

When this call is made, [!DNL Target] attempts to locate the profile first in the cluster noted in the edge request, or wherever the profile is located and return the content. The profile contents are returned in JSON format.

## Authentication

The [!DNL Target Profile API] can be secured by turning authentication on from the [!DNL Target] UI as described here. Once authentication is switched ON, all profile API requests must have the profile authentication token set in the request headers. The token itself can be generated using the [!DNL Target] UI or using the steps explained above in the [Profile Authentication Token](https://developers.adobetarget.com/api/#authentication-tokens){target=_blank} section.

## Metering

These calls do not count towards your mbox calls.

## Error handling

In the case of a call to `/thirdPartyId` with an invalid or an expired `thirdPartyId` specified:

```
{"status" : 404, "message" : "No profile found for client <client_code> with third party id=<third_party_id>"}
```

If the profile can not be located or has expired:

```
{"status" : 404, "message" : "No profile found for client <client_code> with mboxPC=<mbox_pc>"}
```