---
description: >-
  Whalesync API reference for Live Export: create exports, map source tables,
  save, schedule, trigger runs, and monitor them.
---

# Live Export API reference

A live export copies tables from a source app into tables it creates in a destination app. It runs one way, on demand or on a schedule, and never writes to the source. Everything for Live Export lives under `/live-export/`. [Live Export](https://docs.whalesync.com/live-export/live-export) describes the feature itself, and [Live Export vs. sync](https://docs.whalesync.com/live-export/live-export/live-export-vs-sync) compares it with a sync.

Paths are relative to `https://api.whalesync.com/v1`, as on the [API reference](https://docs.whalesync.com/api/reference). Authentication, scopes, error responses, pending actions, pagination, and rate limits work as described there. This page covers what is specific to Live Export.

{% hint style="warning" %}
**Runs overwrite the destination tables the export manages.** Edits made in those tables are overwritten on the next run, and rows the export created are deleted when their source record disappears. Rows the export didn't create are left alone. Unlike a sync, nothing waits for a person to review: once an export is saved, the API can turn on its schedule and trigger runs directly. Point exports only at destinations whose data is replaceable.
{% endhint %}

## Availability

* Live Export is available on plans that include it. Reads never explain a missing feature: when Live Export isn't available to the account, `GET /live-export/live-exports` returns an empty list and any `lex_…` id returns `404`.
* `GET /live-export/connectors` returns `[]` when the feature isn't available. When the account is on a plan that doesn't include a connector, it lists the connector with `available: false` and `required_plan`.
* Writes (create, update, delete, mappings `PUT`, save, schedule `PATCH`, trigger, cancel) return `403 live_export_unavailable`, naming the plan when the plan is what's missing.
* Every Live Export endpoint refuses API keys limited to one sync with `403 sync_restricted_key`. See [Keys limited to one sync](https://docs.whalesync.com/api/reference#keys-limited-to-one-sync).

## Scopes

| Scope | Live Export operations |
| --- | --- |
| `read` | Every `GET`, plus `POST …/mappings/validate` |
| `operate` | `POST /live-export/live-exports/{id}/trigger`, `POST /live-export/runs/{id}/cancel` |
| `readwrite` | Create, `PATCH`, `DELETE`, mappings `PUT`, `POST …/save`, schedule `PATCH` |

## IDs

* Live exports are `lex_…` and runs are `run_…`. Both are opaque; only the prefix is guaranteed. Run ids contain a `.` (for example `run_5JjKXzKZqY.wMpkUYLMV0`) because a run id also identifies its export.
* Source table ids can contain commas (for example `transcripts,1299375510811165803`). Pass every id back exactly as you received it.

## Status

| `status` | Meaning |
| --- | --- |
| `draft` | Never saved. No runnable export exists yet. Connect both sides, map, and save. |
| `active` | Saved, and the schedule is on. Runs fire on the cadence. |
| `manual_only` | Saved, but the schedule is off or was never created. The export only runs when triggered. Nothing is stopped or broken. |

* There are no pause or activate endpoints. `PATCH …/schedule {"enabled": …}` turns the schedule on and off, and `trigger` works in every saved state.
* `unsaved_changes: true` means the mappings were edited over the API after the last save. A run still uses the last-saved mappings. Saving clears it, whether the save is made over the API or in the app.

## Endpoints

```
GET    /live-export/connectors                                          Connectors usable for Live Export, with roles and auth.
POST   /live-export/live-exports                                        Create a draft live export.
GET    /live-export/live-exports                                        List, newest first (limit 1–25, default 10).
GET    /live-export/live-exports/{id}                                   One live export.
PATCH  /live-export/live-exports/{id}                                   Rename, finish an API-key side's auth, set the destination location.
DELETE /live-export/live-exports/{id}                                   Delete the export and its schedule. Destination tables stay.
GET    /live-export/live-exports/{id}/source/tables                     Exportable source tables.
GET    /live-export/live-exports/{id}/source/tables/{table_id}/fields   One table's exportable fields, with planned destination name and type.
GET    /live-export/live-exports/{id}/destination/locations             Where created tables can live (?search=).
GET    /live-export/live-exports/{id}/mappings                          The mappings document (+ ETag).
PUT    /live-export/live-exports/{id}/mappings                          Full replace. Supports If-Match.
POST   /live-export/live-exports/{id}/mappings/validate                 Check a document without saving it.
POST   /live-export/live-exports/{id}/save                              Create destination tables and apply the mappings. 202.
GET    /live-export/live-exports/{id}/save                              Poll the save (?wait= up to 50 seconds).
GET    /live-export/live-exports/{id}/schedule                          Cadence, on/off, and the cadences your plan allows.
PATCH  /live-export/live-exports/{id}/schedule                          Turn it on or off, set cadence and timezone.
GET    /live-export/live-exports/{id}/status                             Whether a run is in progress, and when the next one is.
POST   /live-export/live-exports/{id}/trigger                           Run now. Needs operate.
GET    /live-export/runs?live_export=…                                  Run history, newest first (filter required).
GET    /live-export/runs/{id}                                           One run with its steps.
POST   /live-export/runs/{id}/cancel                                    Cancel a run in progress. Needs operate.
```

A live export, as returned by `GET /live-export/live-exports/{id}`:

```json
{"id": "lex_5JjKXzKZqY", "name": "Gong → Airtable", "status": "manual_only",
 "source": {"connector": "gong", "auth_status": "connected", "auth_error": null},
 "destination": {"connector": "airtable", "auth_status": "connected", "auth_error": null,
                 "location": {"id": "appC1moCoIyZ2V5wi", "name": "Sample Gong Export"}},
 "schedule": null,
 "last_run": {"id": "run_5JjKXzKZqY.wMpkUYLMV0", "status": "completed", "trigger": "manual",
              "started_at": "2026-09-08T20:11:59.662Z", "finished_at": "2026-09-08T20:12:25.982Z",
              "summary": "Published 22 changes", "warning": null, "error": null,
              "app_url": "https://app.whalesync.com/exports/…/runs/…"},
 "unsaved_changes": false, "created_at": "2026-09-08T20:09:57.755Z",
 "app_url": "https://app.whalesync.com/exports/…", "pending_actions": [],
 "url": "https://api.whalesync.com/v1/live-export/live-exports/lex_5JjKXzKZqY",
 "status_url": "…/status", "mappings_url": "…/mappings", "save_url": "…/save",
 "schedule_url": "…/schedule", "runs_url": "https://api.whalesync.com/v1/live-export/runs?live_export=lex_5JjKXzKZqY"}
```

* `source` and `destination` are `null` while waiting for a person to connect them in the browser.
* `auth_status` is `connected` or `error`. When it is `error`, `auth_error` holds the app's message.
* `schedule` is `null` until a schedule exists.
* `last_run` is the newest run, which may still be in progress.
* `app_url` is a convenience link for a person, never a required step. For a draft it opens the setup flow.

## Connectors

`GET /live-export/connectors` is a separate registry from `GET /sync/connectors`, because the same app can authenticate differently for each product. The `type` slugs share one namespace, so `hubspot` means HubSpot everywhere. The response is `{"data": […]}`, sorted by name and not paginated.

```json
{"type": "hubspot", "name": "HubSpot", "roles": {"source": true, "destination": false},
 "auth": {"method": "api_key", "fields": [{"id": "apiKey", "label": "Private App Access Token", "optional": false,
          "placeholder": "pat-na1-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}]},
 "available": true, "required_plan": null}
```

* `roles` says whether a connector can be a `source`, a `destination`, or both.
* `auth.method` is `oauth` or `api_key`. For `api_key`, `fields` lists the credential ids to send under `auth`. Unlike the sync registry, Live Export credential fields have no `help` or `options`.
* Which connectors appear depends on the account. Read the list rather than assuming a fixed set.

## Creating a live export

```json
POST /live-export/live-exports
{"name": "HubSpot to Airtable",
 "source": {"connector": "hubspot", "auth": {"apiKey": "pat-na1-…"}},
 "destination": {"connector": "airtable"}}
```

* The body is `name` (optional), `source`, and `destination`. Each side takes a `connector` and, for an `api_key` connector, optionally `auth`. `name` defaults to "<Source> to <Destination>".
* There is no `base`, unlike on a sync. Where the export creates its tables is the destination's `location`; see [Finishing a side and the destination location](#finishing-a-side-and-the-destination-location).
* Inline `auth` is validated during the create. If the app rejects it, nothing is kept and the call returns `400 connection_failed` with the app's message.
* Leave `auth` out to defer a side to a person. The side comes back `null` with a `user_authorization` pending action. This works for any side. OAuth sides can only be connected this way, and sending `auth` for one is `400 oauth_auth_not_allowed`.
* The create accepts an `Idempotency-Key` header.
* Credentials you send are never returned.

## Pending actions

Pending actions have the same shape as on a sync, except that `side` is `source` or `destination`. The URL opens `https://app.whalesync.com/exports/…/connect/{source|destination}?connector=…`. On the destination, the page also asks the person to pick where created tables will live.

Relay `instruction` and `url` to your user word for word, then poll `GET /live-export/live-exports/{id}` until the side is non-null. A call that needs a side that isn't connected yet returns `409 auth_required` (`requires_action`) with the same object as `required_action`.

## Finishing a side and the destination location

* `PATCH /live-export/live-exports/{id} {"source": {"auth": {…}}}` finishes an API-key side that was created without credentials. A side that is already connected returns `409 side_already_connected`. Reconnecting a side is done in the app.
* `location` is where the export creates its tables: an Airtable base, a Notion parent page, a Supabase or Postgres schema, or a Google Sheets spreadsheet. The person usually picks it on the connect page. If it is still unset, list the options with `GET …/destination/locations` (add `?search=` when `has_more` is `true`), then `PATCH {"destination": {"location": "<id>"}}`.
* The locations response is `{"data": [{"id", "name"}], "has_more": bool}`. With `?search=`, `has_more` is always `false`.
* A `location` that isn't in the list returns `400 invalid_location`. So does sending `location` on the source.
* On the export, `destination.location` is `{id, name}` or `null`. `null` means no pick was recorded and nothing has been created yet, or the destination uses its own default. It does not mean the destination is unconnected; an unconnected destination is `destination: null`.

## Source tables and fields

```
GET /live-export/live-exports/{id}/source/tables
GET /live-export/live-exports/{id}/source/tables/{table_id}/fields
```

* `source/tables` is read live from the source app, so it can be slow. It isn't paginated.
* `fields` returns each exportable field with the name and type it will get in the destination. Whalesync plans the types; you can't choose them. When the source and destination are the same kind of database, `type` is the exact column type (`text[]`, `numeric(12,2)`). Otherwise it is one of `text`, `longText`, `number`, `boolean`, `date`, `select`, `multiSelect`, `url`, `email`, `phone`, `currency`, or `json`, with ` list` appended for multi-value fields.
* `suggested_primary` marks the suggested title field.
* `source_record_id` marks the field that lets reruns update records instead of duplicating them. It is always included in created tables, even if you don't map it.
* Link (relationship) fields aren't offered over the API. Set those up in the app.
* `fields` needs both sides connected.

## Mappings

```
GET  /live-export/live-exports/{id}/mappings
PUT  /live-export/live-exports/{id}/mappings
POST /live-export/live-exports/{id}/mappings/validate
```

```json
{"tables": [{
   "source_table": "calls,1299375510811165803",
   "destination_table": {"create": {"name": "Calls"}},
   "fields": [
     {"source_field": "metaData.title", "destination_field": {"create": {"name": "Title", "primary": true}}},
     {"source_field": "metaData.started", "destination_field": {"create": {"name": "Started"}}}
   ]}]}
```

* The export always creates its destination tables and fields. You give names, never types. Mapping onto an existing destination table or column isn't supported over the API (`400 existing_field_not_supported`); use the app.
* Mark at most one field per table `primary` (`400 multiple_primary_fields`). If the destination needs a primary field and none is marked, the suggested one is used.
* Full-replace semantics: anything omitted is unmapped. Edit by fetching the document, modifying it, and putting it back.
* The response carries a `revision`, also sent as the `ETag` header. Send it as `If-Match` on the `PUT`; a stale value returns `412 revision_mismatch`. The mappings `PUT` does not accept `Idempotency-Key`.
* A `PUT` only edits the working copy. Nothing is created in the destination until you [save](#saving).

Once a table has been created in the destination, `GET` shows it and its fields as opaque string ids. Put those back unchanged:

```json
{"revision": "c3lkX2NoamN2a0I0dUg6MQ",
 "tables": [{"source_table": "calls,1299375510811165803", "destination_table": "dfd_yxh7jOl0DB",
             "fields": [{"source_field": "metaData.title", "destination_field": "fields.Title"},
                        {"source_field": "metaData.id", "destination_field": "fields.gong_record_id"}]}]}
```

Here `gong_record_id` is the `source_record_id` field, added automatically. Changing the fields of a table that has already been created returns `400 applied_table_not_editable`. Remove the whole table from the document, or edit it in the app.

`validate` returns `{"valid": bool, "issues": [{"code", "message", "path"}]}`, where `path` is `tables[N]` or `null`. This differs from sync validation: there is no `severity` or `side`, and `path` isn't a JSON pointer. `issues[].code` uses the same codes as the `400`s a `PUT` would return, plus `auth_required` when a side isn't connected and `internal` when validation itself failed.

## Saving

```
POST /live-export/live-exports/{id}/save
GET  /live-export/live-exports/{id}/save
```

`POST …/save` creates the mapped tables and fields in the destination, then makes the new mappings the ones runs use. It runs in the background and returns `202` with the save object. Poll `GET …/save`, passing `?wait=<seconds>` (at most 50) to hold the request until the save finishes or the wait runs out.

```json
{"state": "running", "phase": "create_tables", "progress": {"resolved": 3, "total": 7}, "errors": [],
 "message": "Creating tables and fields in the destination — 3 of 7 done.",
 "live_export_url": "https://api.whalesync.com/v1/live-export/live-exports/lex_…"}
```

* `state` is `pending`, `running`, `succeeded`, or `failed`.
* `phase` is `create_tables`, then `apply`.
* `progress` is `{resolved, total}`.
* `message` is one sentence to show a person.
* `errors` is `[{name, error}]`, one entry per table or field that failed.

Only one save runs at a time. If a save fails, fix the problem and `POST` again; anything already created is skipped. `succeeded` is only reported once no edits remain unsaved, so treat it, together with `unsaved_changes: false` on the export, as the confirmation. Saves report `succeeded` while runs report `completed`.

A save with no tables mapped returns `400 empty_mappings`. `GET …/save` on an export that was never saved returns `404`.

## Schedule

```
GET   /live-export/live-exports/{id}/schedule
PATCH /live-export/live-exports/{id}/schedule
```

`GET` returns `{enabled, cadence, cron, timezone, next_run_at, last_triggered_at, allowed_cadences}`.

* `cadence` is `every_10_minutes`, `every_30_minutes`, `hourly`, `daily`, or `custom`. `custom` is read-only: it is a schedule set in the app that doesn't match the others, and it survives a `PATCH` that changes only `enabled` or `timezone`.
* `cron` is read-only.
* `allowed_cadences` depends on the plan: `daily` only, `daily` and `hourly`, or all four. A cadence outside it returns `403 plan_required`.
* The first `PATCH` creates the schedule. A new schedule starts off, at `daily`. Fields you leave out keep their current values. `timezone` is an IANA name such as `America/New_York`.
* Before the first save, `GET` and `PATCH` return `409 not_provisioned`. After saving but before any `PATCH`, `GET` returns `404` and the export's `schedule` is `null`.

## Runs

```
POST /live-export/live-exports/{id}/trigger
GET  /live-export/live-exports/{id}/status
GET  /live-export/runs?live_export=…
GET  /live-export/runs/{id}
POST /live-export/runs/{id}/cancel
```

* `trigger` starts a run regardless of the schedule and returns `201` with the run. The body is optional.
* One run at a time. Triggering while a run is in progress returns `409 run_in_progress`, whose message names that run.
* With unsaved edits, `trigger` returns `409 unsaved_changes`, because the run would use the last-saved mappings. Save first, or send `{"force": true}` only when the person explicitly wants the last-saved version. Before the first save it returns `409 not_provisioned`.
* `cancel` stops a run in progress. A run that has already finished returns `409 run_not_active`.

`GET …/status` returns a live snapshot:

```json
{"live_export_id": "lex_…", "status": "active", "running": false, "current_run": null,
 "next_run_at": "…", "last_run": {…}, "fetched_at": "…"}
```

Here `last_run` is the latest *finished* run, unlike `last_run` on the export, which may still be running. `next_run_at` is `null` when the schedule is off.

`GET /live-export/runs?live_export=lex_…` lists runs, newest first. History covers recent runs only, so `has_more: false` means the end of what is kept, not every run ever. `GET /live-export/runs/{id}` adds `steps`:

```json
{"id": "run_5JjKXzKZqY.wMpkUYLMV0", "status": "completed", "trigger": "manual",
 "started_at": "…", "finished_at": "…", "summary": "Published 22 changes", "warning": null, "error": null,
 "app_url": "…", "live_export_id": "lex_5JjKXzKZqY",
 "steps": [{"action": "prepare", "name": "…", "status": "completed", "started_at": "…", "finished_at": "…", "error": null},
           {"action": "pull", …}, {"action": "pull", …}, {"action": "map", …}, {"action": "write", …}],
 "url": "https://api.whalesync.com/v1/live-export/runs/run_5JjKXzKZqY.wMpkUYLMV0"}
```

* Run `status` is `pending`, `running`, `completed`, `failed`, or `cancelled`. The wire value is spelled `cancelled`, with two l's.
* Run `trigger` is `manual` (from the API or a person) or `schedule`.
* Step `action` is `prepare`, `pull`, `map`, `write_plan`, or `write`. `write` is the step that changes the destination. Step `name` is a display label; branch on `action`.
* Step `status` is `pending`, `running`, `completed`, `failed`, or `skipped`.
* `summary` describes what the run is doing now, or how it ended.
* Live exports have runs, not issues. A failed run's `error`, and the failed step's `error`, are the diagnostics.
* The run list returns the same object without `live_export_id`, `steps`, and `url`.

## Deleting

`DELETE /live-export/live-exports/{id}` removes the export and its schedule and returns `{"id": "lex_…", "deleted": true}`. Tables already created in the destination are left in place.

## Not yet in the API

These are done in the app: mapping onto existing destination tables or columns, editing the fields of tables already created, link fields, reconnecting a connected side, and setting a custom cron schedule.
