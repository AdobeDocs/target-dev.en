---
title: How to use asynchronous requests in the [!DNL Adobe Target] Python SDK
description: Learn how [!DNL Target] Python SDK supports asynchronous requests, which can reduce the effective target time to zero.
feature: APIs/SDKs
exl-id: 44ab74e5-3c1a-49cf-9fff-fe523b0c2592
---
# Asynchronous Requests (Python)

## Description

One benefit of server-side integration is that you can leverage the huge bandwidth and computing resources available on the server-side by using parallelism. [!DNL Target] Python SDK supports asynchronous requests, which can reduce the effective target time to zero.

## Supported Methods

### Python

```python {line-numbers="true"}
get_offers(options)
send_notifications(options)
get_attributes(mbox_names, options)
```

## Example

A sample application that uses the `asyncio` module's async/await in Python 3.9+ could look like this:

### Python

```python {line-numbers="true"}
async def execute_mboxes(self, mboxes):
    context = Context(channel=ChannelType.WEB)
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_offers_options = {
      "request": delivery_request
    }
    return await asyncio.to_thread(target_client.get_offers, get_offers_options)

async def get_target_delivery_response(mboxes):
    target_delivery_response = await execute_mboxes(mboxes)
    response = Response(target_delivery_response.get("response").to_str(), status=200, mimetype='application/json')
    return response

mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
return asyncio.run(get_target_delivery_response(mboxes)
```

This example assumes you you are using Python 3.9+. If using an older version of Python you can still send asynchronous requests by passing in `options.callback` to `get_offers`. Check out the sample Flask app for more details about asynchronous execution using either callbacks or async/await, [here](https://github.com/adobe/target-python-sdk/blob/main/samples/app.py).
