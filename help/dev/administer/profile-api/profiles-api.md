---
title: Adobe Target Profiles API
description: Learn how to use Adobe Target Profile APIs to send visitor data to [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
---
# [!DNL Adobe Target Profiles API] overview

[!DNL Adobe Target] creates and maintains a profile for every individual user. This profile is stored on the [!DNL Target] edge cluster and is updated in real time after every visit.

## Structure of a [!DNL Target] profile

A Target profile consists of the following objects:

|Object|Details|
| --- | --- |
|`clientcode`|The [!DNL Target] client code to which the profile is associated.|
|`visitorId`|The identifier for the profile. This can be a `tntid`, `thirdpartyid`, or `marketingcloudvisitorid`.|
|`modifiedAt`|The timestamp of when the profile was last updated.|
|`profileAttributes`|List of all the profile attributes stored as key-value pairs on that the individual profile.|

### Sample profile structure

```
{
    "client": "<your-tenant-name>",
    "visitorId": "a1-mbox3rdPartyId",
    "modifiedAt": "2017-08-18T17:53:39.003-04:00",
    "profileAttributes": {
        "insurance": {
            "value": "false",
            "modifiedAt": "2017-07-31T20:34:55.625-04:00"
        },
        "country": {
            "value": "france",
            "modifiedAt": "2017-07-31T14:26:30.879-04:00"
        },
        "checking": {
            "value": "true",
            "modifiedAt": "2017-07-31T20:34:55.625-04:00"
        },
        "user.memberlevel": {
            "value": "0.0",
            "modifiedAt": "2017-08-09T18:18:04.661-04:00"
        },
        "param1": {
            "value": "value1",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "param2": {
            "value": "value2",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "firstSessionStart": {
            "value": "1500648715286",
            "modifiedAt": "2017-07-21T10:51:55.286-04:00"
        },
        "entity.name": {
            "value": "my-entityName",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "entity.id": {
            "value": "my-entityId",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        }
    }
}
```