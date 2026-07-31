---
description: Get an HTTP notification every time Whalesync pushes a change
---

# Sync webhooks (Preview)

{% hint style="warning" %}
**PREVIEW**: Sync webhooks are in preview and details may change. Reach out with feedback or to request access at support@whalesync.com.
{% endhint %}

Sync webhooks notify your own endpoint every time Whalesync pushes a change to your data. Whenever a record is created, updated, or deleted by your sync, Whalesync sends an HTTP POST to a URL you choose. Use it to trigger cache rebuilds, audit logs, Slack alerts, or any downstream automation.

Every event corresponds to an operation you'd see in your sync's Operations feed.

### Setting it up

1. Open your sync and go to **Settings**
2. Find the **Webhooks** section
3. Enter your endpoint URL (must be HTTPS) and click **Save**

When you save, Whalesync shows you a signing secret (starting with `whsec_`). Copy it now: it's only shown once. You'll use it to verify that requests really came from Whalesync.

Use **Send test event** to fire a sample payload at your endpoint right away. The UI shows the response status your server returned, so you can confirm everything is wired up before real events flow.

By default, webhooks only fire for ongoing syncing. If you also want events for every record pushed during the initial sync, turn on **Send events during initial sync**. Careful: a large initial sync can generate thousands of events.

### The message structure

Events are delivered in batches. One POST contains up to 100 events, in the order the operations happened. Your endpoint receives JSON like this:

```json
{
  "deliveryId": "dl_01J8Z9KQ...",
  "sync": { "id": "9b1f...", "name": "Airtable ↔ Webflow" },
  "events": [
    {
      "id": "evt_01J8Z9KR...",
      "type": "record.updated",
      "occurredAt": "2026-07-31T18:02:11.532Z",
      "whalesyncRecordId": "cmr_7f3a...",
      "source": {
        "connector": "airtable",
        "tableId": "tblXXXXXXXX",
        "recordId": "recXXXXXXXX"
      },
      "destination": {
        "connector": "webflow",
        "tableId": "65f2ab...",
        "recordId": "66a1cd..."
      },
      "changedFields": ["Name", "Slug"]
    }
  ]
}
```

- `type` is one of `record.created`, `record.updated`, or `record.deleted`
- `source` and `destination` identify the record on each side of the sync, using the IDs from the connected apps
- `whalesyncRecordId` is Whalesync's own ID for the record. It stays the same across the record's lifetime, on both sides of the sync
- `changedFields` lists the destination fields that were pushed. For creates it lists all pushed fields; for deletes it's empty

Payloads contain IDs and field names, not field values. If you need the data itself, fetch the record from your app using the IDs in the event.

### Delivery guarantees

- **Ordered.** Whalesync keeps a cursor into your sync's operation history and delivers events in order. A new batch isn't sent until the previous one succeeds.
- **At least once.** Rarely, the same event can be delivered twice. Deduplicate by the event `id` if that matters for your use case.
- **Respond fast.** Reply with any 2xx status within 10 seconds. Do slow processing after responding, not before.

### Verifying signatures

Each request includes a signature header:

```
Whalesync-Signature: t=1722448800,v1=5257a869e7...
```

`v1` is an HMAC-SHA256 of `{t}.{raw request body}` using your `whsec_` secret. Verify it before trusting the payload, and reject requests where `t` is more than 5 minutes old. For example, in Node.js:

```javascript
const crypto = require('crypto');

function verify(secret, header, rawBody) {
  const { t, v1 } = Object.fromEntries(header.split(',').map((p) => p.split('=')));
  const expected = crypto.createHmac('sha256', secret).update(`${t}.${rawBody}`).digest('hex');
  return crypto.timingSafeEqual(Buffer.from(expected), Buffer.from(v1));
}
```

You can regenerate the secret at any time from the Webhooks section.

### Retries and automatic disabling

If your endpoint fails (a non-2xx response, or no response within 10 seconds), Whalesync retries the same batch with increasing delays, up to once per hour. Because delivery is ordered, later events wait until the failing batch goes through.

If your endpoint keeps failing:

- After **24 hours** of continuous failures, Whalesync emails you a warning
- After **72 hours**, the webhook is disabled and you get a final email

The Webhooks section in your sync settings always shows the current health: **Active**, **Failing** (with the latest error), or **Disabled** (with the reason).

To turn a disabled webhook back on, fix your endpoint and click **Re-enable**. Delivery resumes from that moment. Events that occurred while the webhook was disabled are skipped, and the UI tells you how many were missed.
