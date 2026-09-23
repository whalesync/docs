---
description: Sync Attio tasks as a table in Whalesync
---

# Attio tasks

### About Attio tasks

[Attio tasks](https://attio.com/help/reference/attio-101/productivity/introduction-to-tasks) are to-dos with a deadline that you can assign to teammates and attach to people and companies. Whalesync shows all the tasks in your workspace as one **Tasks** table, and it syncs in both directions. You can create, complete, and reschedule tasks from your other app, and tasks created in Attio show up on the other side.

### How to sync tasks

When mapping tables, choose **Tasks** alongside People, Companies, and your other Attio tables. Each row is one task, with these columns:

<table><thead><tr><th width="220">Column</th><th width="200">Status</th><th>Notes</th></tr></thead><tbody>
<tr><td>Content</td><td>✅ Supported</td><td>The text of the task. Set it when the task is created; it cannot be changed afterward. See below.</td></tr>
<tr><td>Deadline</td><td>✅ Supported</td><td>A date and time.</td></tr>
<tr><td>Completed</td><td>✅ Supported</td><td>A checkbox.</td></tr>
<tr><td>Completed at</td><td>➡️ Supported (1-Way)</td><td>Read only. Set by Attio when the task is completed.</td></tr>
<tr><td>Created at</td><td>➡️ Supported (1-Way)</td><td>Read only.</td></tr>
<tr><td>Assignees</td><td>✅ Supported</td><td>Links to the Workspace Members table.</td></tr>
<tr><td>Linked people</td><td>✅ Supported</td><td>Links to the People table.</td></tr>
<tr><td>Linked companies</td><td>✅ Supported</td><td>Links to the Companies table.</td></tr>
</tbody></table>

To link tasks to teammates, people, or companies from your other app, add the Workspace Members, People, or Companies table to your sync as well.

### Things to keep in mind

{% hint style="warning" %}
**A task's text cannot be changed after it is created.** Attio lets you set the Content when you create a task but does not allow it to be edited afterward. If you edit the text in your other app, Whalesync does not write the change back, and the column returns to the text in Attio on the next sync. To change what a task says, create a new task.
{% endhint %}

{% hint style="info" %}
**Tasks can only link to people and companies.** Attio does not allow a task to link to a deal, a custom object record, or a list entry, so the Tasks table has no columns for those.
{% endhint %}

* **Assignees that are automations are left blank.** Attio can assign a task to an automation rather than a teammate. Those assignees have no Workspace Members record, so the Assignees column shows only real teammates.
* **Completed at and Created at are set by Attio.** Check the Completed box to complete a task; Attio fills in the completion time.

### Limitations

* **One table for the whole workspace.** Tasks are not split by object or list. Filter on Linked people or Linked companies in your other app if you only want some of them.
* **Content is required.** A row created in your other app without any text cannot be created in Attio and is reported as a sync issue for that row.
