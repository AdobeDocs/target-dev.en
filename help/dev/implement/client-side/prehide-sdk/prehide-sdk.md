---
keywords: prehide SDK, flicker, anti-flicker, prehiding, pre-hiding, alloy, at.js, implementation, consent, CMP, script placement, inline, external, SDK selection
description: Learn how to integrate the [!DNL Adobe Target] Prehide SDK to eliminate the flash of un-personalized content (flicker) during page load. The SDK works with both Adobe Alloy (Web SDK) and at.js.
title: Prehide SDK Integration Guide
feature: Implementation
hide: true
---

# Prehide SDK integration guide
 
A tiny synchronous JavaScript library that prevents the visual flicker caused by [!DNL Adobe Target] personalization rewriting a page mid-render. Add one inline `<script>` tag at the top of `<head>` and the page is revealed only after personalized content is ready, or the safety timer fires.

## Integration steps {#integration-steps}

1. Download the bundle.

   Use the Flicker Manager UI to download `prehide.min.js`. The file is pre-configured with your client code and guard timeout, so no `PrehideConfig` block is needed.

1. Embed it inline at the very top of `<head>`.

   Paste the contents of `prehide.min.js` directly inside an inline `<script>` tag as the first child of `<head>`. See [Inline vs external](#inline-vs-external) for why inline is preferred.

   ```html
   <!-- 1. Prehide SDK: must be FIRST in <head> and BEFORE any Adobe SDK -->
   <script>
     // paste the contents of prehide.min.js here
   </script>

   <!-- 2. Then load Alloy.js OR at.js -->
   <script src="https://your-cdn/alloy.min.js"></script>
   ```

1. (Optional) Add a runtime config block.

   Only required if you self-host the bundle without downloading via the UI, or if you need to override the SDK choice. Place the config block before the prehide script:

   ```html
   <script>
     window.PrehideConfig = {
       org: "your-client-code",
       sdk: "alloy"            // or "atjs" (defaults to "alloy")
     };
   </script>
   <script> /* prehide.min.js inline contents */ </script>
   <script src="https://your-cdn/alloy.min.js"></script>
   ```

1. (Optional) Wire up consent.

   If your implementation uses a Consent Management Platform (CMP), call `window.Prehide.setConsent(...)` as soon as the consent state is known. See [Consent management](#consent-management).

1. Verify.

   Open DevTools and confirm that `<style id="alloy-prehiding">` (or `at-body-style` for at.js) appears in `<head>` on first paint and is removed once the SDK finishes. Run `window.Prehide.getState()` in the console to inspect the runtime state.

## Where to place the script {#script-placement}

>[!IMPORTANT]
>
>The Prehide SDK must run before Alloy/at.js. If Alloy loads first, the page renders un-personalized content and then re-renders. That is the exact flicker this SDK is designed to prevent.
></br>
>Do not add `async` or `defer` to the Prehide SDK script tag. Synchronous execution is required so that the hiding rule is injected before the browser begins laying out the page.

The Prehide SDK must appear earlier in the document than the [!DNL Adobe Target] SDK that cleans up after it. The load order is non-negotiable:

```html
<!doctype html>
<html>
<head>
  <!-- ① Prehide SDK FIRST. Inline. Synchronous. No async/defer. -->
  <script> /* prehide.min.js inline contents */ </script>

  <!-- ② Alloy or at.js loads next -->
  <script src="https://cdn.alloy.adobe.com/alloy.min.js"></script>

  <!-- ③ Then everything else: meta, css, third-party tags, ... -->
  <link rel="stylesheet" href="main.css">
</head>
<body> ... your page ... </body>
</html>
```

## Inline vs external {#inline-vs-external}

There are two ways to include `prehide.min.js`:

| Method | Example | Notes |
| --- | --- | --- |
| Inline (preferred) | `<script>/* full contents of prehide.min.js pasted directly into the page */</script>` | Zero network round-trip. The SDK executes before anything else is rendered. |
| External (only if inlining is impossible) | `<script src="/static/prehide.min.js"></script>` | Introduces a blocking network request before first render. Even with HTTP/2 and edge caching, this typically costs 30-80 ms. |

### Why inline is preferred

>[!TIP]
>
>Inline the bundle directly inside `<script>...</script>` in your HTML template. Treat it like a critical CSS block: small, in-line, and always at the very top.

* No render-blocking fetch. The purpose of the Prehide SDK is to inject hiding rules *before* the first render. An external `<script src>` adds a network round-trip in exactly that critical window.
* No new failure mode. An external file can 404, time out, or be blocked by an ad-blocker. An inline copy cannot.
* Bundle is tiny (~6 KB). Inlining costs less than a typical favicon, and no caching benefit is large enough to outweigh the extra round-trip at first render.
* Cache-friendly. When inlined in the HTML response, the SDK is cached alongside the rest of the document by your existing caching layer (CDN or browser HTTP cache).
* Customer-specific bundle. The downloaded file has your client code baked in at download time. Inlining ensures every visitor receives the correct customized bundle without an additional request.

## Configuration {#configuration}

The SDK accepts configuration from two sources, in priority order. It reads whichever is available first.

### A: Download-time placeholders (no runtime config)

When you download `prehide.min.js` from the Flicker Manager UI, the server substitutes three placeholders inside the bundle:

| Placeholder | Replaced with | Fallback if unreplaced |
| --- | --- | --- |
| `__FM_CLIENT_CODE__` | Your client code (for example, `"acmecorp"`) | Reads `window.PrehideConfig.org` |
| `__FM_TIMEOUT__` | Guard timer duration in ms (for example, `"3000"`) | `5000` ms |
| `__FM_VERSION__` | SDK version (for example, `"1.0.0"`) | `"0.0.0-dev"` |

If you use the UI-downloaded bundle, no `PrehideConfig` block is needed. Just inline the script.

### B: Runtime `window.PrehideConfig` (manual integration)

For self-hosted or unmodified bundles, declare a config object before the prehide script runs:

```html
<script>
  window.PrehideConfig = {
    org: "acmecorp",        // required (or rely on baked-in __FM_CLIENT_CODE__)
    sdk: "alloy"             // optional: "alloy" (default) or "atjs"
  };
</script>
```

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `org` | string | Yes (unless baked in) | Your customer client code. Used as the org segment of the CDN URL from which prehide rules are fetched. |
| `sdk` | `"alloy"` \| `"atjs"` | No | The Adobe SDK loaded on the page. See [SDK selection](#sdk-selection). |

## SDK selection {#sdk-selection}

[!DNL Adobe Target] offers two delivery SDKs: Alloy (the modern Web SDK) and at.js (the classic library). Each looks for a *different* `<style>` element `id` when personalization completes, and removes it to reveal the page. The Prehide SDK must inject the matching `id`; otherwise the page remains hidden until the safety timer fires.

| `sdk` value | Style tag id injected | Removed by | When to use |
| --- | --- | --- | --- |
| `"alloy"` *(default)* | `<style id="alloy-prehiding">` | Alloy SDK on personalize-complete | You're loading Alloy / Adobe Web SDK on this page. |
| `"atjs"` | `<style id="at-body-style">` | at.js on personalize-complete | You're loading the classic at.js library on this page. |

### How to set it

```html
<!-- For at.js -->
<script>
  window.PrehideConfig = { org: "acmecorp", sdk: "atjs" };
</script>
<script> /* prehide.min.js inline */ </script>
<script src="https://cdn.adobe.com/.../at.js"></script>
```

>[!WARNING]
>
>Mismatch warning. Setting `sdk: "alloy"` while loading at.js (or vice-versa) means the SDK will not find the prehide element to remove. The guard timer will eventually reveal the page, but visitors will experience a longer hidden window. Always set `sdk` to match the library you are loading.

Unknown or missing values fall back to `"alloy"`, so existing Alloy integrations continue to work without any configuration change.

## Consent management {#consent-management}

>[!NOTE]
>
>* The consent value is never stored on `window`. Only the function is exposed; internal state remains private to the SDK.
>* Transitions from `"out"` to `"in"` do not re-hide the page, as re-hiding fully-rendered content would be visually disruptive.
>* `setConsent` can be called multiple times within a single page view. Each call replaces the previous state.

The Prehide SDK includes a consent-aware API for coordinating with your CMP. Using it is optional. If `setConsent` is never called, the SDK behaves like a standard non-consent integration.

### API surface

```js
// Single function call. Pass a status string.
window.Prehide.setConsent("pending");  // banner shown, awaiting decision
window.Prehide.setConsent("in");       // user accepted personalization
window.Prehide.setConsent("out");      // user declined personalization

// Read-only debug snapshot.
window.Prehide.getState();
// → { sdk, version, consentStatus, consentApiUsed,
//      rulesResolved, hasSelectorsToGuard, guardTimeout }
```

### What each status does

| Call | Effect on guard timer | Effect on hidden content |
| --- | --- | --- |
| `setConsent("pending")` | Active timer is cleared. No safety unhide fires until consent is resolved. | Selectors stay hidden indefinitely. |
| `setConsent("in")` | Cleared, then restarted with the configured timeout. Waits for rules to resolve if they have not yet done so. | Content remains hidden until the SDK personalizes or the guard timer fires. |
| `setConsent("out")` | Cleared. The page is unhidden immediately. | Page is shown right away. Rules that resolve later do *not* re-hide the content. |
| *(never called)* | Default timer runs from `init()` for the configured duration. | Content remains hidden until the SDK personalizes or the guard timer fires. (Backwards-compatible legacy mode.) |

### Recommended pattern: explicit pending phase

1. As soon as your CMP displays the consent UI, call `setConsent("pending")`. This clears the safety timer so the page stays hidden while the visitor is deciding, preventing a flash of un-personalized content behind the banner.

   ```js
   window.Prehide.setConsent("pending");
   ```

1. When the visitor accepts personalization, call `setConsent("in")`. The guard timer restarts and Alloy/at.js takes over, revealing the page once personalization is applied.

   ```js
   window.Prehide.setConsent("in");
   ```

1. When the visitor declines personalization, call `setConsent("out")`. The page reveals immediately and remains visible. CDN rules that resolve later will not re-hide it.

   ```js
   window.Prehide.setConsent("out");
   ```

### Example: OneTrust-style integration

```js
// Called once OneTrust has rendered its banner.
function onOneTrustReady() {
  // Pause the guard timer while the banner is visible.
  window.Prehide.setConsent("pending");

  OneTrust.OnConsentChanged(function (event) {
    if (event.consentedToTargeting) {
      window.Prehide.setConsent("in");
    } else {
      window.Prehide.setConsent("out");
    }
  });
}
```

### Example: TCF / IAB-style

```js
// Optional: pause the guard while UI is up.
window.Prehide.setConsent("pending");

// Your CMP eventually emits the final TC string.
function onTcData(tcData) {
  const hasTargetConsent = /* derive from tcData */;
  window.Prehide.setConsent(hasTargetConsent ? "in" : "out");
}
```

