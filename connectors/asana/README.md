---
description: Two-way sync Asana tasks with Airtable, Notion, Google Sheets, and more.
cover: ../../.gitbook/assets/gitbook-cover_asana.jpg
coverY: 0
---

# Asana

## Asana Connector Guide

This guide covers how to connect Whalesync to [Asana](https://asana.com), how your projects and tasks appear in Whalesync, and which fields sync.

In Whalesync terms, an Asana **workspace** is the base you pick, each **project** in it is a table, and each **task** in the project is a record. Three more tables, **Users**, **Tags**, and **Projects**, list what the task fields can point at; they are read only.

### Connecting to Asana

Whalesync connects by signing in to Asana, or with a personal access token you paste in. See [Authorize Asana](authorize-asana.md) for both.

1. In Whalesync, choose Asana and sign in, or paste a token.
2. Pick the workspace to sync.
3. Pick the projects to sync. Archived projects are not listed.

### Syncing Data

Every project the connected account can see in Asana is available as a table. Its columns are the task fields Asana gives every task plus the custom fields added to that project, so two projects with different custom fields have different columns.

A task that belongs to several projects appears in each of those tables as the same task. Subtasks appear only when they are also in the project; a subtask that lives only under its parent task is not synced.

## Supported Fields

<table><thead><tr><th width="260">Asana field</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Name</td><td>✅ Supported</td><td>Required when creating a task from another app.</td></tr>
<tr><td>Description</td><td>✅ Supported</td><td>Synced as rich text. See <a href="#descriptions">Descriptions</a>.</td></tr>
<tr><td>Description (plain text)</td><td>➡️ Supported (1-Way)</td><td>Read only. The same description without formatting.</td></tr>
<tr><td>Completed</td><td>✅ Supported</td><td>A checkbox. Completed at is read only.</td></tr>
<tr><td>Due date</td><td>✅ Supported</td><td>A date, with a time when the task has one.</td></tr>
<tr><td>Start date</td><td>✅ Supported</td><td>Asana requires a due date before a start date, and both must be the same kind: both days, or both with a time.</td></tr>
<tr><td>Assignee</td><td>✅ Supported</td><td>A link to the Users table.</td></tr>
<tr><td>Section</td><td>✅ Supported</td><td>A select whose options are the project's sections. A section has to exist in Asana before a task can be moved into it.</td></tr>
<tr><td>Parent task</td><td>✅ Supported</td><td>A link to another task in the same project. Set it to make a task a subtask; clear it to make it top level.</td></tr>
<tr><td>Tags</td><td>✅ Supported</td><td>Links to the Tags table. Tags have to exist in Asana first.</td></tr>
<tr><td>Followers</td><td>✅ Supported</td><td>Links to the Users table. Asana adds the connected account as a follower of every task Whalesync creates, and that follower syncs back to the other app.</td></tr>
<tr><td>Type</td><td>✅ Supported</td><td>One of <code>default_task</code>, <code>milestone</code>, or <code>approval</code>. Set when a task is created; it cannot be changed afterwards.</td></tr>
<tr><td>Approval status</td><td>✅ Supported</td><td>Only approval tasks keep it. Approving a task also completes it.</td></tr>
<tr><td>Attachments</td><td>➡️ Supported (1-Way)</td><td>Read only. Files hosted by Asana are synced as files; links to Dropbox, Google Drive, Box, or Vimeo are left out.</td></tr>
<tr><td>Projects</td><td>➡️ Supported (1-Way)</td><td>Read only. Links to the Projects table for every project the task is in.</td></tr>
<tr><td>Dependencies</td><td>➡️ Supported (1-Way)</td><td>Read only. Links to the tasks this one depends on.</td></tr>
<tr><td>Subtask count, Link, Created at, Modified at</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
</tbody></table>

### Custom fields

Custom fields are an Asana paid feature. Each custom field added to a project is a column of that project's table.

<table><thead><tr><th width="260">Custom field type</th><th width="220">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Text</td><td>✅ Supported</td><td>Up to 1,024 characters.</td></tr>
<tr><td>Number</td><td>✅ Supported</td><td>Includes currency and other number formats. Asana rounds to the field's precision.</td></tr>
<tr><td>Single-select</td><td>✅ Supported</td><td>Synced by option name. A task holding an option that was later disabled still reads; writing a disabled option is refused by Asana.</td></tr>
<tr><td>Multi-select</td><td>✅ Supported</td><td>Synced by option names.</td></tr>
<tr><td>Date</td><td>✅ Supported</td><td>A date, with a time when the field has one.</td></tr>
<tr><td>People</td><td>✅ Supported</td><td>Links to the Users table.</td></tr>
<tr><td>Formula, ID, Reference</td><td>➡️ Supported (1-Way)</td><td>Read only, as the text Asana shows.</td></tr>
</tbody></table>

## Descriptions

A task's description is synced as rich text. Asana only accepts a small set of formatting: bold, italic, underline, strikethrough, code, links, bulleted and numbered lists, block quotes, preformatted text, two heading levels, and dividers. When a description comes from another app, Whalesync keeps the text and the formatting Asana has an equivalent for and drops the rest. Paragraphs become line breaks, tables become lines of text, and images become links to the image. A description longer than 30,000 characters after that is reported as a sync issue for the task rather than sent.

## Real-time updates

Whalesync registers a webhook on each project you map, so a change to a task in Asana reaches your other apps within seconds instead of waiting for the next poll. Asana removes a webhook after a day of failed deliveries; Whalesync puts it back on its next schema refresh. Turning the sync off removes the webhooks.

## Things to Keep in Mind

* **The Asana connector is in beta.** If something does not work as described here, [let us know](../../resources/support/).
* **Only projects the connected account can see are listed.** A private project it is not a member of is not. My Tasks lists are not projects and are not synced.
* **A task removed from a project is treated as deleted in that project's table.** The task still exists in Asana; it just no longer belongs to the table.
* **Whalesync does not create sections or tags.** A section name that does not exist in the project is reported as a sync issue for that task. A tag has to be one of the records in the Tags table.
* **Milestones cannot have a start date**, and approval status is ignored on tasks that are not approvals. Asana enforces both.
* **Comments and stories are not synced.**
* **Whalesync makes at most 150 requests a minute to Asana**, the limit Asana sets for free workspaces, whatever plan your workspace is on. A large first sync takes a while.
