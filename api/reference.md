---
description: Paths, authentication, and conventions for the Whalesync API
---

# API reference

The Whalesync API creates and monitors syncs programmatically. It is a REST API with JSON request and response bodies, API-key authentication, cursor pagination, and stable machine-readable error codes. Responses include URLs for the next available operations, and anything that requires a human comes back as a structured action to relay.

* **Base URL:** `https://api.whalesync.com/v1`
* **Spec:** OpenAPI 3.1 at `https://api.whalesync.com/v1/openapi.json`
* **Discovery:** `https://api.whalesync.com/llms.txt`
* **Companion pages:** [Agent quickstart](https://docs.whalesync.com/api/agent-quickstart) walks through the typical sync creation flow · [Error reference](https://docs.whalesync.com/api/errors) documents every error code

All request and response fields are `snake_case`. The one exception is the keys *inside* a side's `auth`: those are the credential field ids each connector declares (for example Postgres's `connectionString`), passed through verbatim, so `GET /v1/connectors` and `auth` always agree and nothing is translated.

## Authentication

Authenticate every request with an API key in the `Authorization` header:

```
Authorization: Bearer ws_tok_XXXXXXXXXXXXXXXXXXXXXXXX
```

Create keys in **Settings → API keys** in the Whalesync app. You can have multiple named keys; each key's secret is shown **once** at creation. Keys can be revoked at any time in Settings, revocation is immediate, and each key shows its `last_used_at`.

{% hint style="warning" %}
**There is no endpoint that creates an API key.** API keys are created manually by a human in the app. A request without a key returns a `401` naming the smallest sufficient scope and carrying a key-creation link to give to a person.
{% endhint %}

Keys have one of two scopes:

* `readwrite`: full access.
* `read`: monitoring only. Anything that changes something fails with `403 insufficient_scope`. The one `POST` a `read` key may call is `…/validate`, which only checks a document and never writes. Note that `read` exposes the *contents* of synced records (before/after values in the operations log).

There is no OAuth for the API itself.

## Conventions

### Error responses

Every error has the same shape:

```json
{"error": {"type": "invalid_request_error", "code": "incompatible_field_types",
           "message": "…", "doc_url": "https://docs.whalesync.com/api/errors#…"}}
```

`code` values are stable. Branch on them, not on `message`. Some errors add a `details` object with machine-readable specifics, and `requires_action` errors add a `required_action` object for a human. Every code, and the `type` values that classify them, are documented in the [Error reference](https://docs.whalesync.com/api/errors).

### Pending actions

Some steps require a human signed in to Whalesync (connecting an app, starting a sync). A sync lists them in `pending_actions`:

```json
"pending_actions": [
  {"type": "user_authorization",
   "audience": "end_user",
   "action": "open_in_browser",
   "side": "right",
   "connector": "airtable",
   "url": "https://app.whalesync.com/syncs/9f2c…/connect-apps?connector=airtable&side=right",
   "instruction": "Give this link to a person. They sign in to Whalesync and connect airtable in the browser; the API and agents cannot complete this step."}
]
```

Calling an endpoint one of them is blocking returns a `409` with the *same object* as `required_action`:

```json
{"error": {"type": "requires_action", "code": "auth_required",
  "message": "Both sides have to be connected before mappings can be read or written.",
  "required_action": {"type": "user_authorization", "audience": "end_user", "action": "open_in_browser",
    "side": "right", "connector": "airtable", "url": "https://app.whalesync.com/syncs/9f2c…/connect-apps?connector=airtable&side=right",
    "instruction": "Give this link to a person. …"}}}
```

`type` is `user_authorization` (connect an app), `user_confirmation` (review and start the sync), or `user_api_key` (create the key itself, which only ever appears on a `401`). Relay `instruction` and `url` to your user; don't fetch the URL.

### Pagination

List endpoints take `limit` and `cursor`, and return `{"data": […], "has_more": true, "next_cursor": "…"}`.

### IDs

Whalesync IDs are prefixed (`sync_…`, `table_…`, `field_…`). Schema objects also carry the `remote_id` from the connected app (Airtable `tbl…`/`fld…`, Postgres table names, and so on), and **anywhere you reference a table or field you may use either form**.

### Links

Responses include `*_url` fields (`tables_url`, `fields_url`, `mappings_url`, and more) pointing at the next valid steps for that resource's current state. Follow them instead of constructing URLs.

### Idempotency

Send an `Idempotency-Key` header on `POST /v1/syncs` and on the mappings `PUT`, the two calls that create objects, to make retries safe. The other writes are already safe to repeat: pause, activate, and issue retry converge on the same state.

A retry with the same key and body replays the original response (marked with an `Idempotent-Replayed: true` header). The same key with a different body is a `400 idempotency_key_reused`, and a retry that lands while the first request is still running is a `409 idempotency_key_in_use`. Keys expire after 24 hours; a failed request releases its key so the retry runs fresh.

### Rate limits

Per-key limits; `429` with `Retry-After` when exceeded. `RateLimit-*` headers on every response show the budget.

### Credentials are not returned

Credentials you send (connection strings, connector API keys) are never included in any response.

## Connectors

```
GET /v1/connectors            All connectors: type slug, auth method, credential fields, capabilities.
```

`GET /v1/connectors` tells you how each connector authenticates: `"auth": {"method": "oauth"}` or `"auth": {"method": "api_key", "fields": [{"id": "connectionString", "label": "Postgres connection string", …}]}`. Each field's `id` is the key to send under a side's `auth`; send it exactly as given. Connectors your plan doesn't include are still listed, annotated with `"available": false` and the required plan.

## Credentials

Each sync side holds its own credentials: inline `auth` for API-key connectors, given when the sync is created, or a browser sign-in for OAuth connectors, done by a human in Whalesync. **Credentials are scoped to their sync.** There are no connection endpoints, nothing to reuse across syncs, and nothing to clean up.

* Anything the API exposes about a credential (auth status, error codes) appears nested on the side object in sync responses, for example `"left": {"auth_status": "error", "auth_error": "invalid_credentials", …}`.
* A broken credential also opens an issue (raising the sync's `open_issues` count) whose `remediation` explains how to fix it.
* To fix or rotate an **API-key** credential, PATCH the side with a new `auth`, same shape as at creation: `PATCH /v1/syncs/{sync_id} {"right": {"auth": {"connectionString": "…"}}}`.
* **OAuth** credentials can only be reconnected in the Whalesync app; the issue's `remediation` sends your user there.
* To see which remote bases or workspaces a side's credentials can reach (for example after an ambiguous `base` name):

```
GET /v1/syncs/{sync_id}/sides/{side}/bases
```

## Syncs

A sync connects two apps (its `left` and `right` sides) and keeps mapped tables in sync.

```
POST   /v1/syncs                       Create a sync with both sides declared.
GET    /v1/syncs                       List syncs with status + open_issues.
GET    /v1/syncs/{sync_id}             Full sync incl. per-side status and next-step URLs.
PATCH  /v1/syncs/{sync_id}             Rename, amend a side while draft, update a side's auth.
DELETE /v1/syncs/{sync_id}             Stops the sync and deletes it. Returns {"id": "sync_…", "deleted": true}.
```

### Creating a sync

```json
POST /v1/syncs
{"name": "CRM sync",
 "left":  {"connector": "airtable"},
 "right": {"connector": "postgres",
           "auth": {"connectionString": "postgres://…"},
           "base": "public"}}
```

An **API-key** side takes a `connector`, `auth` (inline credentials), and a `base`.

`base` is the ID of the base/workspace/schema **in the connected app**: an Airtable `app…` ID, a Postgres schema name, and so on. An exact display name is accepted as a fallback when it's unambiguous. It resolves during the create itself: if it can't be found (or matches more than one base) the create fails with `base_not_found` / `base_ambiguous`, and the error's `details.bases` lists what the credentials can reach. Fix the request and retry.

An **OAuth** side takes only its `connector`: no `auth`, no `base`. Its browser sign-in requires a human, so the API leaves that side unbuilt. It comes back `null` and the sync carries a `user_authorization` pending action naming the app you asked for. Relay it to your user; the link opens that app's sign-in directly, they pick the base, and you poll the sync until the side appears.

* That page requires a normal Whalesync login as the account's owner. It is not a capability link, so it can't be used to attach someone else's account to your sync.
* Until both sides exist, mappings, schema, and activate calls answer `409 requires_action` (`auth_required`) carrying the same action.
* When only one side is built, it takes the **left** slot; the side your user connects becomes the right. Read the sync back once both exist and write mappings against that shape.

{% hint style="info" %}
A sync involving a browser sign-in app **can** be created over the API. Only sending credentials for such an app is unsupported. Declare that side by connector alone; a human completes the connection.
{% endhint %}

Sync statuses: `draft → active ⇄ paused`. A sync is `draft` until your user starts it in Whalesync, and any mappings edit returns it to `draft`. There is no separate health field. A sync with problems has a nonzero `open_issues` count (and `auth_status: "error"` on the affected side); read `/v1/issues` for the details.

## Schema discovery

Table and field listings are fetched from the connected app on demand and cached. Each listing carries a top-level `fetched_at` saying when its cache was filled, and each table in the table listing also carries `fields_fetched_at`, null until you ask for that table's fields. Pass `?refresh=true` to refetch; like in the app, refreshing needs the sync to be off, since an active sync's schema is kept fresh automatically. A first fetch can take a few seconds; if another request is already loading the same schema the endpoint returns `202` with `{"loading": true}` and a `Retry-After` header. Retry the same GET.

```
GET /v1/syncs/{sync_id}/tables?side=left               Tables on one side.
GET /v1/syncs/{sync_id}/tables/{table_id}/fields       Fields with type metadata.
```

Fields look like:

```json
{"id": "field_7d…", "remote_id": "fldXYZ", "name": "Amount",
 "type": "currency", "read": true, "write": true, "required": false, "primary": false,
 "type_details": {"display_name": "Currency", "allows_multiple_values": false}}
```

`type_details` carries whatever extra the connector says about that field type, and is null when there's nothing to add.

`type` is the connector's own field type. Every connector has its own set, so there is no global type enum. Use the capability flags (`read`, `write`, `required`, `primary`) to plan mappings, and `POST …/validate` to check compatibility: it is the authoritative check, and incompatible pairs come back with a specific `code` and `message` explaining why.

### Views

Some connectors sync a table through one of its **views** (Airtable, Salesforce). Those tables come back with a `views` object saying both whether you have to pick one and what the choices are:

```json
"views": {"required": true,
          "options": [{"value": "ALL_RECORDS", "name": "All Records"},
                      {"value": "viwActive", "name": "Active"}]}
```

Put the `value` in that side's `view` in the mappings document. `views` is null when the connector has no such concept, in which case `view` must be omitted. Both `POST …/validate` and the mappings `PUT` check this and name the legal values back to you: `view_required` when one is missing, `view_not_found` for a value the table doesn't have, `view_not_supported` for a `view` on a table with none. The PUT rejects before writing anything and repeats the detail in `details.issues`. Note that `view` is part of the full-replace document: leave it out of a later PUT and the previous selection is cleared, which fails the same way.

## Mappings

The mappings document declares which tables and fields sync, and in which direction. It is read and written as a whole:

```
GET  /v1/syncs/{sync_id}/mappings      Current document (+ ETag).
PUT  /v1/syncs/{sync_id}/mappings      Full replace. Supports If-Match and Idempotency-Key.
POST /v1/syncs/{sync_id}/validate      Check a document (body optional; defaults to the stored one).
```

```json
{"tables": [{
   "left_table": "tblContacts",
   "right_table": {"create": {"name": "contacts"}},
   "direction": "left_to_right",
   "right": {"record_delete_behavior": "do_nothing"},
   "fields": [
     {"left_field": "fldName",  "right_field": {"create": {"name": "name"}}},
     {"left_field": "fldEmail", "right_field": {"create": {"name": "email"}}}
   ]}]}
```

* Table and field references are strings for existing objects (a `remote_id`, a Whalesync id, or an exact name when it's unique on that side) or `{"create": {"name": "…"}}` to have Whalesync create the table or field on that side, typed from its mapped counterpart. Creation happens when you `PUT`; the response returns the document with real ids filled in, and retries safely adopt already-created objects. Only one side of a pair may be a `create`.
* `direction` per table: `left_to_right | right_to_left | two_way`. Fields default to their table's direction.
* Full-replace semantics: anything omitted is unmapped, and omitted settings revert to defaults. Fetch-modify-put is the intended editing pattern.
* `validate` returns issues you can fix mechanically:

```json
{"issues": [{"severity": "error", "code": "incompatible_field_types",
             "path": "/tables/0/fields/1", "side": "right", "message": "…"}]}
```

Errors block activation (not saving a draft); warnings never block. There are two failure channels. A structurally malformed document (wrong types, an invalid `direction`, a create placeholder on both sides of a pair) is a `400 invalid_mappings` naming the path. Everything semantic about a well-formed document (unknown or orphaned references, incompatibilities, unmapped required fields) comes back as a `200` with issues.

## Starting and stopping

```
POST /v1/syncs/{sync_id}/activate      Turn a paused sync back on.
POST /v1/syncs/{sync_id}/pause         Turn an active sync off.
```

**A sync only runs under a configuration a human has started in the Whalesync app.** While a sync is `draft` (newly created, or edited since it last ran) there is nothing for the API to activate: the sync carries a `user_confirmation` pending action (and `review_url`, the same page). Relay it to your user; they review what was built (including record matching for tables that have data on both sides) and start the sync with a click. Poll the sync until `status` is `active`.

Calling `activate` on a `draft` sync returns the standard prerequisite error:

```json
{"error": {"type": "requires_action", "code": "confirmation_required",
  "message": "This sync's configuration hasn't been reviewed yet. Your user needs to review and start it in Whalesync.",
  "required_action": {"type": "user_confirmation", "audience": "end_user", "action": "open_in_browser",
    "side": null, "url": "https://app.whalesync.com/syncs/9f2c…",
    "instruction": "Give this link to a person. …"}}}
```

Once started, `pause` and `activate` toggle the sync freely from the API, until the mappings change, which returns it to `draft`.

## Monitoring

```
GET  /v1/syncs/{sync_id}/status                Live snapshot: pending pushes, polling state, change detection.
GET  /v1/operations?sync=…                     Record-level change log (also filter by table and since).
GET  /v1/operations/{id}
GET  /v1/issues?sync=…                         Open issues, with remediation guidance.
GET  /v1/issues/{id}
POST /v1/issues/{id}/retry                     Clear an issue and retry the failed work.
```

Operations and issues are top-level collections filtered by `?sync=`, with the filter param named after the resource. The `sync` filter is required: both collections are always read one sync at a time. Every sync response links to its own slices via `operations_url` and `issues_url`.

An operation, as returned by `GET /v1/operations/{id}`:

```json
{"id": "op_81…", "occurred_at": "…", "sync_id": "sync_9f…",
 "action": "updated", "trigger": "push",
 "table": {"id": "table_1d…", "name": "Contacts"},
 "record": {"remote_id": "recABC", "name": "Jane Doe", "url": "https://airtable.com/…"},
 "field_changes": [{"field": "Stage", "before": "Lead", "after": "Won"}]}
```

`trigger` is `push` (Whalesync wrote the change) or `poll` (Whalesync detected it). The **list** returns the same object without `field_changes` and with a null `record.url`; both need the full stored log for each row, which is too expensive per page. Fetch an operation on its own for them. The operation's `table` carries no `remote_id`: the log is stored denormalized, so only the Whalesync id and the display name at the time are on the row.

An issue (note `remediation`, written to be actionable by an agent):

```json
{"id": "iss_44…", "type": "connection", "code": "authentication_error",
 "sync_id": "sync_9f…", "connector": "airtable",
 "message": "Airtable authorization expired.",
 "remediation": {"explanation": "…", "suggested_action": "Reconnect Airtable…",
                 "links": [{"name": "Reconnecting an app", "url": "https://…"}]},
 "table": null,
 "first_seen_at": "…", "last_seen_at": "…", "occurrence_count": 14}
```

`code` is a broad category (`authentication_error`, `connection_error`, `record_error`, `webhook_error`, `validation_error`, `sync_error`), deliberately coarse: it does not reveal more about your credentials than that they failed. The specifics you should act on are in `remediation` and `message`. `type` is the area the issue is in (`connection`, `record`, `webhook`, `sync_preview`, or `other`) and is what `?type=` filters on.

## Planned additions

Not yet in the API: per-table record filters (`tables[].filter` string expressions) · per-side advanced settings (sync-gating column, debounce) · webhooks, both per-sync record-change deliveries (`webhook_url`) and API-level events (`/v1/webhook_endpoints`) · record read/write endpoints · org-scoped API keys.
