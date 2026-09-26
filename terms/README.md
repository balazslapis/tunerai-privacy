# Terms & Conditions page

`index.html` is the public Terms & Conditions. The app links to it from the purchase screen (both
skins) and the tuner menu, via `TERMS_URL` in
`app/src/main/java/com/pianotuner/ai/presentation/subscription/PurchaseTerms.kt`.

Like the data deletion page it is versioned here, next to the code that has to keep it true, but it
is **not served from this repository**. It is published from
[`balazslapis/tunerai-privacy`](https://github.com/balazslapis/tunerai-privacy).

## Publishing

Copy `index.html` into the privacy repo under `terms/`, then commit and push:

```
tunerai-privacy/
  README.md            -> https://balazslapis.github.io/tunerai-privacy/
  terms/
    index.html         -> https://balazslapis.github.io/tunerai-privacy/terms/
```

Publish it **before** a build carrying the link reaches users, or the link opens a 404.

## Keep in step

The page makes promises the app has to keep:

- **Internet connection** and **Lifetime access**: summarised in
  `PURCHASE_TERMS_DISCLOSURE`, which is shown beside every purchase button. Change both together.
- **Lifetime access works without our servers**: that is `SubscriptionViewModel`'s device lifetime
  fallback, which reads Google Play's on-device purchase record when the backend gives no answer.
  Removing it breaks section 5.
- **Three devices, two removals per 30 days**: section 4a mirrors `MAX_AUTHORIZED_DEVICES`,
  `MAX_DEVICE_REMOVALS` and `DEVICE_REMOVAL_WINDOW_MILLIS` in `firebase/functions/src/deviceSeats.ts`
  and the "3 devices" in `PURCHASE_TERMS_DISCLOSURE`. Change all of them together.
- **Discontinuation**: section 6 commits to six months' notice and a final offline-capable release.
  If the service is ever wound down, that release has to let signed-out and fresh installs of lifetime
  owners reach the tuner too, since sign-in stops working with the backend.

Bump the effective date whenever the text changes.
