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

The API can create a sync, read the tables and fields on both sides, create tables and fields on a side where they don't exist yet, write and validate mappings, pause, activate, and delete syncs, and read the operations log and open issues.

Two steps require a human. Both are deliberate design decisions, so there is no API path around them.

**Connecting a side in the browser.** A person connects a side whenever its credentials aren't sent inline. That is always the case for apps that sign in through a browser — Airtable, HubSpot, Salesforce, Webflow, and similar OAuth connectors, whose credentials cannot be sent over the API at all. It is also a choice for connectors that take credentials inline (Postgres, Supabase, and others): if your user would rather not paste an app's credentials — a database password, a service API key — into the conversation, you can defer that side to a person too. Either way, declare that side with `connector` only and omit `auth` and `base`. The created sync has that side `null` and a `pending_actions` entry with a link for a human, who signs in, connects the app, and picks its base.

{% hint style="info" %}
Any side can be left for a person to connect in the browser: declare it by connector alone, omitting `auth` and `base`, and a human completes the connection. For OAuth apps this is the only way. For API-key apps it is a choice, so your user never has to paste an app's credentials into the conversation.
{% endhint %}

**Starting a sync.** A sync only runs under mappings a human has reviewed and started in the app. Build the sync, then hand over its `review_url`. Any later mappings edit returns the sync to `draft`, which requires a new review.

## How human steps appear in the API

The same object appears on the sync as `pending_actions` and on a blocked call's `409` as `required_action`:

```json
{"type": "user_authorization", "audience": "end_user", "action": "open_in_browser",
 "side": "right", "connector": "airtable",
 "url": "https://app.whalesync.com/syncs/edit/9f2c…/connect-apps?connector=airtable&side=right",
 "instruction": "Give this link to a person. They sign in to Whalesync and connect airtable in the browser — credentials entered there never pass through the API or an agent. Agents cannot complete this step."}
```

Relay `instruction` and `url` to your user. Do not fetch the URL; it is a login-protected page for a human. Poll the sync until the step is complete.

## Typical sync creation flow

1. `GET /v1/connectors` to find your two apps and how each authenticates.
2. `POST /v1/syncs` with credentials inline for the app that takes them, and connector alone for the browser one — or connector alone for any app whose credentials the user prefers to enter themselves.
3. Relay the sync's `user_authorization` pending action. Poll until both sides are non-null.
4. Follow `tables_url`, then each table's `fields_url`, to read the real tables and fields on both sides. Present these for your user to pick from; don't ask them to list tables and fields up front. Once a side is connected you can read its whole schema yourself.
5. `POST …/validate` your mappings document, fix issues by `code` and `path`, then `PUT …/mappings`. Map to existing tables and fields, or have Whalesync create them on a side with `{"create": {"name": "…"}}` (see [Creating tables and fields](#creating-tables-and-fields)).
6. Relay the sync's `user_confirmation` pending action. Poll until `status` is `active`.
7. Monitor with `GET …/status`, `/v1/operations?sync=…`, and `/v1/issues?sync=…`. Issues carry `remediation` written to be acted on; `POST /v1/issues/{id}/retry` once the cause is fixed.

## Creating tables and fields

You don't need a human to build the destination table or columns first. Whalesync can create them for you as part of writing mappings. In the mappings document, reference an existing object by string (a `remote_id`, a Whalesync id, or an exact name when it's unique on that side), or use `{"create": {"name": "…"}}` to have Whalesync create it on that side, typed from its mapped counterpart:

```json
{"tables": [{
   "left_table": "tblContacts",
   "right_table": {"create": {"name": "contacts"}},
   "direction": "left_to_right",
   "fields": [
     {"left_field": "fldName",  "right_field": {"create": {"name": "name"}}},
     {"left_field": "fldEmail", "right_field": {"create": {"name": "email"}}}
   ]}]}
```

Creation happens when you `PUT …/mappings`: the response returns the document with real ids filled in, and retries safely adopt already-created objects. Only one side of a pair may be a `create` — the other must be an existing table or field to copy the type from.

## Best practices

* Follow the `*_url` fields in responses instead of constructing URLs. They point at the next valid steps for the resource's current state.
* Read the schema; don't ask your user for it. Once a side is connected you can list its tables and fields yourself and present them to pick from. A destination table or field that doesn't exist yet doesn't have to be built by hand either — create it with `{"create": {"name": "…"}}`.
* Send `Idempotency-Key` on `POST /v1/syncs` and the mappings `PUT`, the two calls that create objects, so retries are safe.
* Use `If-Match` on the mappings `PUT` with the revision you read, so a concurrent edit made in the app fails with `412 revision_mismatch` instead of being overwritten.
* Prefer `remote_id` over names when referencing bases, tables, and fields. Names are not unique and can be renamed.
* Don't ask the user to paste an app's credentials into the conversation unless they offer — create that side without `auth` and hand over the connect link.
* Branch on `code`, not `message`. Messages are written for people and may change.
