---
description: Guide for AI agents building syncs with the Whalesync API
---

# Agent quickstart

This page is for AI agents driving the Whalesync API on someone's behalf, and for the people setting them up. Full endpoint documentation is in the [API reference](https://docs.whalesync.com/api/reference). Every error code is in the [Error reference](https://docs.whalesync.com/api/errors).

## Connection details

```
Base URL:  https://api.whalesync.com/v1
Spec:      https://api.whalesync.com/v1/openapi.json   (describes every endpoint)
Auth:      Authorization: Bearer ws_tok_…
Scopes:    read (monitor) · readwrite (build and change)
```

Fetch the OpenAPI spec first. Everything else can be read from it.

## Ask a human for an API key

There is no endpoint that creates an API key. API keys are created manually by a human in the Whalesync app. Do not probe for `POST /v1/keys` or similar; no such endpoint exists.

A request without a usable key returns a `401` with a `required_action` containing the key-creation link to give to your user. You can also ask before starting:

> To set this up I need a Whalesync API key. I can't create one myself.
>
> 1. Open **https://app.whalesync.com/settings/api-keys**
> 2. Click **Create key**
> 3. Choose **Read and write** so I can build the sync (**Read only** is enough if you just want me to watch it)
> 4. Copy the key and paste it here. It's shown only once.
>
> Treat it like a password: it can read and change your syncs, including the contents of synced records.

Request the `read` scope if you only need monitoring. A `read` key can call every `GET` and `POST …/validate`; anything that changes state needs `readwrite`. Scope is fixed at creation.

Keys can be revoked at any time from the same page. Revocation is immediate.

## Steps requiring human intervention

The API can create a sync, read the tables and fields on both sides, write and validate mappings, pause, activate, and delete syncs, and read the operations log and open issues.

Two steps require a human. Both are deliberate design decisions, so there is no API path around them.

**Connecting an app that signs in through a browser.** Airtable, HubSpot, Salesforce, Webflow, and similar connectors authenticate with OAuth in a browser, so their credentials cannot be sent over the API. The sync can still be created over the API: declare that side with `connector` only and omit `auth` and `base`. The created sync has that side `null` and a `pending_actions` entry with a link for a human, who signs in, connects the app, and picks its base. Connectors that accept credentials inline (Postgres, Supabase, and others) can be configured entirely over the API.

{% hint style="info" %}
A sync involving a browser sign-in app **can** be created over the API. Only sending credentials for such an app is unsupported. Declare that side by connector alone; a human completes the connection.
{% endhint %}

**Starting a sync.** A sync only runs under mappings a human has reviewed and started in the app. Build the sync, then hand over its `review_url`. Any later mappings edit returns the sync to `draft`, which requires a new review.

## How human steps appear in the API

The same object appears on the sync as `pending_actions` and on a blocked call's `409` as `required_action`:

```json
{"type": "user_authorization", "audience": "end_user", "action": "open_in_browser",
 "side": "right", "connector": "airtable",
 "url": "https://app.whalesync.com/syncs/edit/9f2c…/connect-apps?connector=airtable&side=right",
 "instruction": "Give this link to a person. They sign in to Whalesync and connect airtable in the browser; the API and agents cannot complete this step."}
```

Relay `instruction` and `url` to your user. Do not fetch the URL; it is a login-protected page for a human. Poll the sync until the step is complete.

## Typical sync creation flow

1. `GET /v1/connectors` to find your two apps and how each authenticates.
2. `POST /v1/syncs` with credentials inline for the app that takes them, and connector alone for the browser one.
3. Relay the sync's `user_authorization` pending action. Poll until both sides are non-null.
4. Follow `tables_url`, then each table's `fields_url`.
5. `POST …/validate` your mappings document, fix issues by `code` and `path`, then `PUT …/mappings`.
6. Relay the sync's `user_confirmation` pending action. Poll until `status` is `active`.
7. Monitor with `GET …/status`, `/v1/operations?sync=…`, and `/v1/issues?sync=…`. Issues carry `remediation` written to be acted on; `POST /v1/issues/{id}/retry` once the cause is fixed.

## Best practices

* Follow the `*_url` fields in responses instead of constructing URLs. They point at the next valid steps for the resource's current state.
* Send `Idempotency-Key` on `POST /v1/syncs` and the mappings `PUT`, the two calls that create objects, so retries are safe.
* Use `If-Match` on the mappings `PUT` with the revision you read, so a concurrent edit made in the app fails with `412 revision_mismatch` instead of being overwritten.
* Prefer `remote_id` over names when referencing bases, tables, and fields. Names are not unique and can be renamed.
* Branch on `code`, not `message`. Messages are written for people and may change.
