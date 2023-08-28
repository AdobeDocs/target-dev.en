---
title: Getting Started with Target SDKs
description: How do I use the Adobe Target SDKs?
feature: APIs/SDKs
exl-id: a5ae9826-7bb5-41de-8796-76edc4f5b281
---
# Getting Started with [!DNL Target] SDKs

In order to get up and running, we encourage you to create your first [on-device decisioning](../on-device-decisioning/overview.md) feature flag activity in the language of your choice:

* Node.js
* Java
* .NET
* Python
  
## Summary of steps

1. Enable on-device decisioning for your organization
1. Install the SDK
1. Initialize the SDK
1. Set up the feature flags in an [!DNL Adobe Target] [!UICONTROL A/B Test] activity
1. Implement and render the feature in your application
1. Implement tracking for events in your application
1. Activate your [!UICONTROL A/B Test] activity

## 1. Enable on-device decisioning for your organization

Enabling on-device decisioning ensures an [!UICONTROL A/B Test] activity is executed at near-zero latency. To enable this feature, navigate to **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** and enable the **[!UICONTROL On-Device Decisioning]** toggle.

![alt image](assets/asset-odd-toggle.png)

>[!NOTE]
>
>You must have the **[!UICONTROL Admin]** or **[!UICONTROL Approver]** [user role](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) to enable or disable the **[!UICONTROL On-Device Decisioning]** toggle.

After enabling the **[!UICONTROL On-Device Decisioning]** toggle, [!DNL Adobe Target] begins generating [rule artifacts](../on-device-decisioning/rule-artifact-overview.md) for your client.

## 2. Install the SDK

For Node.js, Java, and Python, run the following command in your project directory in the terminal. For .NET, add it as a dependency by [installing from NuGet](https://www.nuget.org/packages/Adobe.Target.Client).

>[!BEGINTABS]

>[!TAB Node.js (NPM)]

```js {line-numbers="true"}
npm i @adobe/target-nodejs-sdk -P
```

>[!TAB Java (Maven)]

```javascript {line-numbers="true"}
<dependency>
   <groupId>com.adobe.target</groupId>
   <artifactId>java-sdk</artifactId>
   <version>2.0</version>
</dependency>
```

>[!TAB .NET (Bash)]

```bash {line-numbers="true"}
dotnet add package Adobe.Target.Client
```

>[!TAB Python (pip)]

```python {line-numbers="true"}
pip install target-python-sdk
```

>[!ENDTABS]

## 3. Initialize the SDK

The rule artifact is downloaded during the SDK initialization step. You can customize the initialization step to determine how the artifact is downloaded and used.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
   client: "<your target client code>",
   organizationId: "your EC org id",
   decisioningMethod: "on-device",
   events: {
      clientReady: targetClientReady
      }
};

const tClient = TargetClient.create(CONFIG);

function targetClientReady() {
   //Adobe Target SDK has now downloaded the JSON artifact locally, which contains the activity details.
   //We will see how to use the artifact here very soon.
}
```

>[!TAB Java (Maven)]

```javascript {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
   .client("testClient")
   .organizationId("ABCDEF012345677890ABCDEF0@AdobeOrg")
   .build();
TargetClient targetClient = TargetClient.create(config);
```

>[!TAB .NET (C#)]

```csharp {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("testClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
   .Build();
this.targetClient.Initialize(targetClientConfig);
```

>[!TAB Python]

```python {line-numbers="true"}
from target_python_sdk import TargetClient

def target_client_ready():
   # Adobe Target SDK has now downloaded the JSON artifact locally, which contains the activity details.
   # We will see how to use the artifact here very soon.

CONFIG = {
   "client": "<your target client code>",
   "organization_id": "your EC org id",
   "decisioning_method": "on-device",
   "events": {
      "client_ready": target_client_ready
   }
}

target_client = TargetClient.create(CONFIG)
```

>[!ENDTABS]

## 4. Set up the feature flags in an [!DNL Adobe Target] [!UICONTROL A/B Test] activity

1. In [!DNL Target], navigate to the **[!UICONTROL Activities]** page, then select **[!UICONTROL Create Activity]** > **[!UICONTROL A/B test]**. 

   ![alt image](assets/asset-ab.png)

1. In the **[!UICONTROL Create A/B Test Activity]** modal, leave the default Web option selected (1), select **[!UICONTROL Form]** as your experience composer (2), select **[!UICONTROL Default Workspace]** with **[!UICONTROL No Property Restrictions]**(3), then click **[!UICONTROL Next]** (4).

   ![alt image](assets/asset-form.png)

1. In the **[!UICONTROL Experiences]** step of activity creation, provide a name for your activity (1) and add a second experience, Experience B, by clicking **[!UICONTROL Add Experience]** (2). Enter the location name of your choice (3). For example, `ondevice-featureflag` or `homepage-addtocart-featureflag` are location names indicating the destinations for feature flag testing.  In the example shown below, `ondevice-featureflag` is the location defined for Experience B. Optionally, you may add Audience Refinements (4) to restrict qualification to the activity.

   ![alt image](assets/asset-location.png)

1. In the **[!UICONTROL CONTENT]** section on the same page, select **[!UICONTROL Create JSON Offer]** in the drop-down (1) as shown.

   ![alt image](assets/asset-offer.png)

1. In the **[!UICONTROL JSON Data]** text box that appears, type your feature flag variables for each experience (1), using a valid JSON object (2).

   Enter the feature flag variables for Experience A.

   ![alt image](assets/asset-json_a.png)
   
   **(Sample JSON for Experience A, above)**

   ```json {line-numbers="true"}
   {
      "enabled" : true,
      "flag" : "expA"
   }
   ```

   Enter the feature flag variables for Experience B.

   ![alt image](assets/asset-json_b.png)

   **(Sample JSON for Experience B, above)**

   ```json {line-numbers="true"}
   {
      "enabled" : true,
      "flag" : "expB"
   }
   ```

1. Click **[!UICONTROL Next]** (1) to advance to the **[!UICONTROL Targeting]** step of activity creation.

   ![alt image](assets/asset-next_2_t.png)

1. In the **[!UICONTROL Targeting]** step example shown below, Audience Targeting (2) remains on the default set of All Visitors, for simplicity. This means the activity is untargeted. However, note Adobe recommends you always target your audiences for production activities. Click **[!UICONTROL Next]** (3) to advance to the **[!UICONTROL Goals & Settings]** step of activity creation.

   ![alt image](assets/asset-next_2_g.png)

1. In the **[!UICONTROL Goals & Settings]** step, set **[!UICONTROL Reporting Source]** to **[!UICONTROL Adobe Target]** (1). Define the **[!UICONTROL Goal Metric]** as **[!UICONTROL Conversion]**, specifying the details based on your site's conversion metrics (2). Click **[!UICONTROL Save & Close]** (3) to save the activity.

   ![alt image](assets/asset-conv.png)

## 5. Implement and render the feature in your application

After setting up the feature flag variables in [!DNL Target], modify your application code to use them. For example, after getting the feature flag in the application, you can use it to enable features and render the experience for which the visitor qualified.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity
​
let featureFlags = {};
​
function targetClientReady() {
   tClient.getAttributes(["ondevice-featureflag"]).then(function(response) {
      const featureFlags = response.asObject("ondevice-featureflag");
      if(featureFlags.enabled && featureFlags.flag !== "expA") { //Assuming "expA" is control
         console.log("Render alternate experience" + featureFlags.flag);
      }
      else {
         console.log("Render default experience");
      }
   });
}
```

>[!TAB Java (Maven)]

```javascript {line-numbers="true"}
MboxRequest mbox = new MboxRequest().name("ondevice-featureflag").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
   .context(new Context().channel(ChannelType.WEB))
   .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
   .build();
Attributes attributes = targetClient.getAttributes(request, "ondevice-featureflag");
String flag = attributes.getString("ondevice-featureflag", "flag");
```

>[!TAB .NET (C#)]

```csharp {line-numbers="true"}
var mbox = new MboxRequest(index: 0, name: "ondevice-featureflag");
var deliveryRequest = new TargetDeliveryRequest.Builder()
   .SetContext(new Context(ChannelType.Web))
   .SetExecute(new ExecuteRequest(mboxes: new List<MboxRequest> { mbox }))
   .Build();
var attributes = targetClient.GetAttributes(request, "ondevice-featureflag");
var flag = attributes.GetString("ondevice-featureflag", "flag");
```

>[!TAB Python]

```python {line-numbers="true"}
# ... Code removed for brevity

feature_flags = {}

def target_client_ready():
   attribute_provider = target_client.get_attributes(["ondevice-featureflag"])
   feature_flags = attribute_provider.as_object(mbox_name="ondevice-featureflag")
   if feature_flags.get("enabled") and feature_flags.get("flag") != "expA": # Assuming "expA" is control
      print("Render alternate experience {}".format(feature_flags.get("flag")))
   else:
      print("Render default experience")
```

>[!ENDTABS]

## 6. Implement additional tracking for events in your application

Optionally, you can send additional events for tracking conversions using the sendNotification() function.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity
​
//When a conversion happens
TargetClient.sendNotifications({
   targetCookie,
   "request" : {
      "notifications" : [
      {
         type: "display",
         timestamp : Date.now(),
         id: "conversion",
         mbox : {
            name : "orderConfirm"
         },
         order : {
            id: "BR9389",
            total : 98.93,
            purchasedProductIds : ["J9393", "3DJJ3"]
         }
      }
      ]
   }
})
```

>[!TAB Java (Maven)]

```javascript {line-numbers="true"}
Notification notification = new Notification();
notification.setId("conversion");
notification.setImpressionId(UUID.randomUUID().toString());
notification.setType(MetricType.DISPLAY);
notification.setTimestamp(System.currentTimeMillis());
Order order = new Order("BR9389");
order.total(98.93);
order.purchasedProductIds(["J9393", "3DJJ3"]);
notification.setOrder(order);

TargetDeliveryRequest notificationRequest =
   TargetDeliveryRequest.builder()
      .context(new Context().channel(ChannelType.WEB))
      .notifications(Collections.singletonList(notification))
      .build();

NotificationDeliveryService notificationDeliveryService = new NotificationDeliveryService();
notificationDeliveryService.sendNotification(notificationRequest);
```

>[!TAB .NET (C#)]

```csharp {line-numbers="true"}
var order = new Order
{
   Id = "BR9389",
   Total = 98.93M,
   PurchasedProductIds = new List<string> { "J9393", "3DJJ3" },
};
​
var notification = new Notification
{
   Id = "conversion",
   ImpressionId = Guid.NewGuid().ToString(),
   Type = MetricType.Display,
   Timestamp = DateTimeOffset.UtcNow.ToUnixTimeMilliseconds(),
   Order = order,
};
​
var notificationRequest = new TargetDeliveryRequest.Builder()
   .SetContext(new Context(ChannelType.Web))
   .SetNotifications(new List<Notification> {notification})
   .Build();
​
targetClient.SendNotifications(notificationRequest);
```

>[!TAB Python]

```python {line-numbers="true"}
# ... Code removed for brevity

# When a conversion happens
notification_mbox = NotificationMbox(name="orderConfirm")
order = Order(id="BR9389, total=98.93, purchased_product_ids=["J9393", "3DJJ3"])
notification = Notification(
   id="conversion",
   type=MetricType.DISPLAY,
   timestamp=1621530726000,  # Epoch time in milliseconds
   mbox=notification_mbox,
   order=order
)
notification_request = DeliveryRequest(notifications=[notification])


target_client.send_notifications({
   "target_cookie": target_cookie,
   "request" : notification_request
})
```

>[!ENDTABS]

## 7. Activate your [!UICONTROL A/B Test] activity

1. Click **[!UICONTROL Activate]** (1) to activate your [!UICONTROL A/B Test] activity.

   >[!NOTE]
   >
   >You must have the **[!UICONTROL Approver]** or **[!UICONTROL Publisher]** [user role](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) to perform this step.

   ![alt image](assets/asset-activate.png)
