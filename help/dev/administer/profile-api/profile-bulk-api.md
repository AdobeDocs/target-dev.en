---
title: Adobe Target Bulk Profile Update API
description: Learn how to use [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] to send multiple visitors' profile data to [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
---
# [!DNL Adobe Target Bulk Profile Update API]

The [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] lets you update user profiles for multiple visitors to a website in bulk using a batch file.

Using the [!UICONTROL Bulk Profile Update API], you can conveniently send detailed visitor profile data in the form of profile parameters for many users to [!DNL Target] from any external source. External sources can include Customer Relationship Management (CRM) or Point of Sale (POS) systems, which are not usually available on a web page.

|Version|URL example|Features|
| --- | --- | --- |
|v1|`http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/profile/batchUpdate`|Support for bulk profile update only.|
|v2|`http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/v2/profile/batchUpdate`|<ul><li>Create profile if not found.</li><li>Per row status update.</li></ul>|

>[!NOTE]
>
>Version 2 (v2) of the [!UICONTROL Bulk Profile Update API] is the current version. However, [!DNL Target] still supports version 1 (v1).

## Benefits of the Bulk Profile Update API

* No limit on the number of profile attributes.
* Profile attributes sent via the site can be updated via the API and the opposite way.

## Caveats

* The size of the batch file must be less than 50 MB. In addition, the total number of rows should not exceed 500,000 rows per upload.
* There is no limit on the number or rows that you can upload over a period of 24 hours in subsequent batches. However, the ingestion process might be throttled during business hours to ensure that other processes run efficiently.
* Consecutive v2 batch update calls without mbox calls in between for the same thirdPartyIds override the properties updated in the first batch update call.
* [!DNL Adobe] does not guarantee that 100% of batch profile data will be onboarded and retained in Target and, thus, be available for use in targeting. In the current design, there is a possibility that a small percentage of data (up to 0.1% of large production batches) might not be onboarded or retained.

## Batch file

To update profile data in bulk, create a batch file. The batch file is a text file with values separated by commas similar to the following sample file.

``````
batch=pcId, param1, param2, param3, param4 123, value1 124, value1,,, value4 125,, value2 126, value1, value2, value3, value4
``````

You reference this file in the POST call to [!DNL Target] servers to process the file. When creating the batch file, consider the following:

* The first row of the file must specify column headers.
* The first header should either be a `pcId` or `thirdPartyId`. The [!UICONTROL Marketing Cloud visitor ID] is not supported. [!UICONTROL pcId] is a [!DNL Target]-generated visitorID. `thirdPartyId` is an ID specified by the client application, which is passed to [!DNL Target] through an mbox call as `mbox3rdPartyId`. It must be referred to here as `thirdPartyId`.
* Parameters and values you specify in the batch file must be URL-encoded using UTF-8 for security reasons. Parameters and values can be forwarded to other edge nodes for processing through HTTP requests.
* The parameters must be in the format `paramName` only. Parameters are displayed in [!DNL Target] as `profile.paramName`.
* If you are using [!UICONTROL Bulk Profile Update API] v2, you need not specify all parameter values for each `pcId`. Profiles are created for any `pcId` or `mbox3rdPartyId` that is not found in [!DNL Target]. If you are using v1, profiles are not created for missing pcIds or mbox3rdPartyIds.
* The size of the batch file must be less than 50 MB. In addition, the total number of rows should not exceed 500,000. This limit ensures that servers don't get flooded with too many requests.
* You can send multiple files. However, the sum total of the rows of all the files that you send in a day should not exceed one million for each client.
* There is no limit on number of attributes that you upload. However, the overall size of a profile, including system data, should not exceed 2000 KB. [!DNL Adobe] recommends that you use less than 1000 KB of storage for profile attributes.
* Parameters and values are case-sensitive.

## HTTP POST request

Make an HTTP POST request to [!DNL Target] edge servers to process the file. Here is a sample HTTP POST request for the file batch.txt using the curl command:

``````
curl -X POST --data-binary @BATCH.TXT http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate
``````

Where:

BATCH.TXT is the filename. CLIENTCODE is the [!DNL Target] client code.

If you don't know your client code, in the [!DNL Target] user interface click **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**. The client code is shown in the [!UICONTROL Account Details] section.

### Inspect the response

The Profiles API returns the submission status of the batch for processing along with a link under "batchStatus" to a different URL that shows the overall status of the particular batch job.

### Example API response

The following code snipped is an example of a Profiles API response:

```
<response>
    <success>true</success>
    <batchStatus>http://mboxedge45.tt.omtrdc.net/m2/demo/profile/batchStatus?batchId=demo-1701473848678-13029383</batchStatus>
    <message>Batch submitted for processing</message>
</response>
```

If there is an error, the response contains `success=false` and a detailed message for the error.

### Default batch status response

A successful default response when the above `batchStatus` URL link is clicked looks like the following:

```
<response><batchId>demo4-1701473848678-13029383</batchId><status>complete</status><batchSize>1</batchSize></response>
```

Expected values for the status fields are:

|Status|Details|
| --- | --- |
|[!UICONTROL complete]|The profile batch update request was completed successfully.|
|[!UICONTROL incomplete]|The profile batch update request is still being processed and not completed.|
|[!UICONTROL stuck]|The profile batch update request is stuck and was not able to complete.|

### Detailed batch status URL response

A more detailed response can be fetched by passing a parameter `showDetails=true` to the `batchStatus` url above.

For example:

```
http://mboxedge45.tt.omtrdc.net/m2/demo/profile/batchStatus?batchId=demo-1701473848678-13029383&showDetails=true
```

#### Detailed response

```
<response>
    <batchId>demo4-1701473848678-13029383</batchId>
    <status>complete</status>
    <batchSize>1</batchSize>
    <consumedCount>1</consumedCount>
    <successfulUpdates>1</successfulUpdates>
    <profilesNotFound>0</profilesNotFound>
    <failedUpdates>0</failedUpdates>
</response>
```