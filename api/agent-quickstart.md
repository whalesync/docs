---
description: >-
  How an AI agent gets a Whalesync API key and builds a sync end to end, and
  which steps need a person.
---

# Agent quickstart

This page is written for an AI agent driving the Whalesync API on someone's behalf, and for the person setting that agent up. Full endpoint documentation is in the [API reference](https://docs.whalesync.com/api/reference). Every error code is in the [Error reference](https://docs.whalesync.com/api/errors).

## The four things an agent needs

```
Base URL:  https://api.whalesync.com/v1
Spec:      https://api.whalesync.com/v1/openapi.json   (fetch this first; it describes every endpoint)
Auth:      Authorization: Bearer ws_tok_…
Scopes:    read (monitor) · readwrite (build and change)
```

Everything else can be read from the spec.

## Getting a key: ask, don't probe

**There is no endpoint that creates an API key, and there won't be.** Minting a credential is a person's decision, so it happens in the Whalesync app while signed in. An agent that goes looking for `POST /v1/keys` is wasting turns.

If you call the API without a usable key, you get a `401` that says this and includes a `required_action` with the link to hand over. The error is the onboarding. You can also ask up front:

> To set this up I need a Whalesync API key. I can't create one myself.
>
> 1. Open **https://app.whalesync.com/settings/api-keys**
> 2. Click **Create key**
> 3. Choose **Read and write** so I can build the sync (**Read only** is enough if you just want me to watch it)
> 4. Copy the key and paste it here. It's shown only once.
>
> Treat it like a password: it can read and change your syncs, including the contents of synced records.

Ask for the smaller scope when it is all you need. A `read` key can call every `GET` and `POST …/validate`. Everything that changes state needs `readwrite`. Scope is fixed at creation.

A key can be revoked at any time from the same page, and revocation is immediate.

## What you can and can't do alone

You can create a sync, read the tables and fields on both sides, write the mappings between them, validate before writing, pause, activate, delete, and read the operations log and open issues.

Two steps need a person. Neither is a limitation to work around; both are deliberate.

**Apps that sign in through a browser** (Airtable, HubSpot, Salesforce, Webflow, and others) can't have credentials sent over the API. You can still create the sync: name that side by connector alone and leave out `auth` and `base`. The sync comes back with that side `null` and a `pending_actions` entry linking a person to the step that connects it, where they also pick its base. Apps that take credentials inline (Postgres, Supabase, and others) you configure end to end.

{% hint style="info" %}
**A sync involving a browser sign-in app can still be created over the API.** Only sending credentials for such an app is unsupported. Don't conclude that these syncs must be built in the app; declare the side by connector, then hand the connection step to a person.
{% endhint %}

**Starting a sync** is a person's call. A sync runs only under mappings someone has reviewed and started in the app. Build it, then hand over the sync's `review_url`. Any later mappings edit returns the sync to `draft` and needs a fresh review. A sync never runs under a configuration no person has seen.

## How a person's step reaches you

Always the same object, whether it's sitting on a sync as `pending_actions` or attached to a `409` as `required_action`:

```json
{"type": "user_authorization", "audience": "end_user", "action": "open_in_browser",
 "side": "right", "connector": "airtable",
 "url": "https://app.whalesync.com/syncs/edit/9f2c…/connect-apps?connector=airtable&side=right",
 "instruction": "Give this link to a person. They sign in to Whalesync and connect airtable in the browser; the API and agents cannot complete this step."}
```

Relay `instruction` and `url`. **Don't fetch the URL.** It's a page for a person, behind their login, and fetching it accomplishes nothing. Then poll the sync until the thing it was waiting for has happened.

## A whole sync, start to finish

1. `GET /v1/connectors` to find your two apps and how each authenticates.
2. `POST /v1/syncs` with credentials inline for the app that takes them, and connector alone for the browser one.
3. Relay the sync's `user_authorization` pending action. Poll until both sides are non-null.
4. Follow `tables_url`, then each table's `fields_url`.
5. `POST …/validate` your mappings document, fix issues by `code` and `path`, then `PUT …/mappings`.
6. Relay the sync's `user_confirmation` pending action. Poll until `status` is `active`.
7. Watch it: `GET …/status`, `/v1/operations?sync=…`, `/v1/issues?sync=…`. Issues carry `remediation` written to be acted on; `POST /v1/issues/{id}/retry` once the cause is fixed.

## Habits that pay off

* **Follow the `*_url` fields** in responses instead of building URLs. They point at the next legal step from that resource's state, and they don't drift.
* **Send `Idempotency-Key`** on `POST /v1/syncs` and the mappings `PUT`, the two calls that create things.
* **Use `If-Match`** on the mappings `PUT` with the revision you read, so an edit someone made in the app during your handoff fails loudly instead of being overwritten.
* **Prefer `remote_id` over names** when referencing bases, tables, and fields. Names aren't unique and get renamed.
* **Read `code`, not `message`.** Messages are for people and will change.
