---
description: What you need to do to avoid disruption when Webflow deprecates their v1 API
---

# Webflow deprecating v1 APIs

On January 1st 2025, Webflow is deprecating their v1 APIs. All new Whalesync syncs use Webflow's v2 APIs but if you're on an older sync it may still be using v1.

To avoid any disruption to syncing, **you'll need to reauthorize your Webflow connection in each of your syncs** that uses Webflow.

<figure><img src="../../.gitbook/assets/webflow reauth.png" alt=""><figcaption><p>How to reauthorize Webflow</p></figcaption></figure>

### How do I know if need to reauthorize?

Your connection status will say "Expiring Soon" (see above screenshot) if you need to reauthorize.

If not, you're good to go :white\_check\_mark:.
