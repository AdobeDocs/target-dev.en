---
title: How to use asynchronous requests in the [!DNL Adobe Target] Java SDK
description: Learn how [!DNL Target] Java SDK supports asynchronous requests, which can reduce the effective target time to zero.
feature: APIs/SDKs
exl-id: e11f8d16-76f6-4d39-822a-34a1cf7f623f
---
# Asynchronous Requests (Java)

## Description

One benefit of server-side integration is that you can leverage the huge bandwidth and computing resources available on the server-side by using parallelism. [!DNL Target] Java SDK supports asynchronous requests, which can reduce the effective target time to zero.

## Supported Methods

### Methods

```javascript {line-numbers="true"}
CompletableFuture<TargetDeliveryResponse> getOffersAsync(TargetDeliveryRequest request);
CompletableFuture<ResponseStatus> sendNotificationsAsync(TargetDeliveryRequest request);
CompletableFuture<Attributes> getAttributesAsync(TargetDeliveryRequest targetRequest, String ...mboxes);
```

## Example

A sample `Spring` application Controller could look like this:

### Sample Controller

```javascript {line-numbers="true"}
@RestController
public class TargetRestController {

    @Autowired
    private TargetClient targetJavaClient;

    @GetMapping("/mboxTargetOnlyAsync")
        public TargetDeliveryResponse mboxTargetOnlyAsync(
                @RequestParam(name = "mbox", defaultValue = "server-side-mbox") String mbox,
                HttpServletRequest request, HttpServletResponse response) {
            ExecuteRequest executeRequest = new ExecuteRequest()
                    .mboxes(getMboxRequests(mbox));

            TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
                    .context(getContext(request))
                    .execute(executeRequest)
                    .cookies(getTargetCookies(request.getCookies()))
                    .build();
            CompletableFuture<TargetDeliveryResponse> targetResponseAsync =
                    targetJavaClient.getOffersAsync(targetDeliveryRequest);
            targetResponseAsync.thenAccept(tr -> setCookies(tr.getCookies(), response));
            simulateIO();
            TargetDeliveryResponse targetResponse = targetResponseAsync.join();
            return targetResponse;
        }

    /**
     * Function for simulating network calls like other microservices and database calls
     */
    private void simulateIO() {
        try {
            Thread.sleep(200L);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

}
```

This example assumes you have [initialized the SDK](initialize-sdk.md) as a spring bean and that you have [utility methods](utility-methods.md) available.

The [!DNL Target] request is fired before `simulateIO` and by the time it is executed target result should also be ready. Even if it is not, you will have significant savings in most cases.
